# <b><b>Tool-list / CheatSheet for windows forensics stuff</b></b>
## WMI CLI:
##### Syntax uses: `wmic /node:\<remote-IP> /user:\<admin acct>`
- Get auto-start processes
`wmic /node:10.1.1.1 startup list full`
- Remote process list:
`wmic /node:10.1.1.1 process get`
- Network configuration
`wmic /node:10.1.1.1 nicconfig get`
- Spot executables running from strange locations:
`wmic PROCESS WHERE "NOT ExecutablePath LIKE '%Windows%'" GET ExecutablePath`

##### Possible WMIC recon
```
wmic process get CSName,Description,ExecutablePath,ProcessId
 wmic useraccount list full; wmic group list full; wmic netuse list full;
 wmic qfe get Caption,Description,HotFixID,InstalledOn
 wmic startup get Caption,COmmand,Location,User
```
##### WMIC Priv Esc (from powerup.ps1)
```
#find unquoted services set to auto‐start
wmic service get name,displayname,pathname,startmode | findstr /i "Auto" | findstr /i /v "C:\Windows\\" |findstr /i/v"""
#find highly privileged processes that can be attacked
$Owners=@{}Get‐WmiObject ‐Classwin32_process|Where‐Object{$_}|ForEach‐Object{$Owners[$_.handle]=$_.getowner().user}
#find all paths to service.exe's that have a space in the path and aren't quoted
$VulnServices=Get‐WmiObject ‐Classwin32_service|Where‐Object{$_} | Where‐Object {($_.pathname ‐ne$null) ‐and ($_.pathname.trim() ‐ne"")} | Where‐Object {‐not $_.pathname.StartsWith("`"")} |Where‐Object{ ‐not $_.pathname.StartsWith("'")} |Where‐Object
```
### process call
> wmic.exe PROCESS CALL CREATE \"C:\\Windows\\System32\\rundll32.exe  "C:\\Windows\\files.dat\\\" 
# <b>autorunsc </b>
### Syntax examples
```
autorunsc -accepteula -a * -s -c -h -vr > \\siftworksation\cases\Response\10.1.1.1-arun.csv
 autorunsc.exe /accepteula -a * -c -h -s '*' -nobanner
```
*Validate if code/file is signed by valid/known publisher; May need to reset columns in timeline explorer (under tools)*
# <b>Kansa </b>
Syntax examples:

> .\kansa.ps1 -TargetList .\hostlist -Pushbin
> .\kansa.ps1 -OutputPath .\Output\ -TargetList .\hostlist -TargetCount 250 -Verbose -Pushbin

Kansa project uses this capability to scale collection.  Entire event logs can be collected using commands like the following:
> (Get-WmiObject -Class Win32_NTEventlogFile | Where-Object LogfileName -EQ 'System').BackupEventlog(‘G:\System.evtx')

Enumerate autorun files in a directory - Kansa Script:
```
 Get-ASEPImagePathLaunchStringMD5UnsignedStack.ps1 > output.csv
  Select-String "<process name>"  *Autorunsc.csv
  Select-String "perfmonsvc64.exe" *Autorunsc.csv
```
*Use timeline explorer to view results - filter by least occurance count and use powershell select-string to find which system*

<b>Example Below:</b>
Find stuff in files matching *SvcAll.csv - Kansa Script
>.\Get-LogparserStack.ps1 -FilePattern *SvcAll.csv -Delimiter "," -Direction asc -OutFile SvcAll-workstation-stack.csv

##### Output and optional sort / selection criterea:

>  Enter the field to pass to COUNT():  Name

>  Enter the fields you want to GROUP BY, one per line.
>  Enter "quit" when finished:  Name

>  Enter the fields you want to GROUP BY, one per line.
>  Enter "quit" when finished:  DisplayName

>  Enter the fields you want to GROUP BY, one per line.
>  Enter "quit" when finished:  PathName
<br><b>** Once finding something interesting, use timeline explorer to view the results **</b><br><br>
<b> Use select-string to find which system it is on in the csv file, pipe out to gridview or tableview </b>
> Select-String "string" *SvcAll.csv
> .\Disk\Get-TempDirListing.ps1 | Out-GridView
> .\Log\Get-LogWinEvent.ps1 security | Out-GridView
# <b>Amacheparser </b>
### Syntax Examples
```
AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" --csv C:\temp
 AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" -i on --csv C:\temp --csvf foo.csv
 AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" -w "c:\temp\whitelist.txt" --csv C:\temp
```
# <b>Appcompatprocessor.py </b>
### Syntax Examples

- <b>stacking by file path and file name</b>
>./AppCompatProcessor.py ./database.db stack "filePath" "fileName like '%servicehost.exe'"

- <b>stacking by filepath</b>
>./appcompatprocessor.py ./database.db stack fsearch Filepath -f "ProgramData"

- <b>Will search the FileName field for anything that contains 'cmd.exe'</b>
>./AppCompatProcessor.py ./database.db fsearch FileName -F "cmd.exe"

- <b>Will search the FileName field for anything that exactly matches 'cmd.exe'</b>
>./AppCompatProcessor.py ./database.db fsearch FileName -F "=cmd.exe"

- <b>Will find files whose size contains "4096"</b>
>./AppCompatProcessor.py ./database.db fsearch Size -F "4096"

- <b>Will find files whose size _is_ "4096"</b>
>./AppCompatProcessor.py ./database.db fsearch Size -F "=4096"

- <b>Will find files whose size is bigger than 4096 bytes (and has Size data of course: XP appcompat or AmCache data)
>./AppCompatProcessor.py ./database.db fsearch Size -F ">4096"

- <b>Will find files for some attackers that regularly screwed the trademark symbol on the versioning information on their tools.</b>
> ./AppCompatProcessor.py ./test-AmCache.db fsearch Product -F "Microsoft@"

- <b>Find by producet</b>
>./AppCompatProcessor.py ./test-AmCache.db fsearch Product -F "Microsoft@"
##### also see the regex options and other modules

# <b>Evtxcmd</b>

> yet another awesome tool by Eric Zimmerman.  A command line tool for parsing Windows Event Log (EVTX) files. It can be used to extract events from a single file or a directory of files. Can use to export events to CSV, JSON, or HTML.  Leverages the xpath with open/crowd sourced map files to make parsing much simplier.
### Examples Syntax:
```
 evtxecmd -f "C:\Temp\Application.evtx" --csv "c:\temp\out" --csvf MyOutputFile.csv
  evtxecmd -f "C:\Temp\Application.evtx" --csv "c:\temp\out"
  evtxecmd -f "C:\Temp\Application.evtx" --json "c:\temp\jsonout"
  evtxecmd -f C:\Windows\system32\winevt\logs\Security.evtx --csv C:\Temp\event-logs --csvf security.csv
```
# <b>Get-WinEvent</b>
### PowerShell can be used to collect and filter logs
```
Get-WinEvent -ComputerName for remote collection
Get-WinEvent -Logname for local events
Get-WinEvent -Path for archived log files
Get-WinEvent -FilterHashtable @{Logname=“Security";id=4624} | Where {$_.Message -match “spsql"}
Get-WinEvent -FilterHashtable @{Path="C:\Path-To-Exported\Security*.evtx“ ;id=5140} | Where {$_.Message -match "\\Admin\$"}
```
# <b>KAPE</b>
https://ericzimmerman.github.io/KapeDocs

> Kroll Artifact Parser and Extractor (KAPE) is primarily a triage program that will target a device or storage location, find the most forensically relevant artifacts (based on your needs), and parse them within a few minutes. Because of its speed, KAPE allows investigators to find and prioritize the more critical systems to their case. Additionally, KAPE can be used to collect the most critical artifacts prior to the start of the imaging process. While the imaging completes, the data generated by KAPE can be reviewed for leads, building timelines, etc.
```
tsource
 The drive letter or directory to search. This should be formatted as C, D:, or F:\.

target
 The target configuration to run, without the extension. Get a list of all available targets with the --tlist switch.

tdest
 The directory where files should be copied to. This directory will be created if it does not exist. This can be a regular directory or a UNC path.Other important options:vssFind, mount, and search all available Volume Shadow Copies on --tsource.
vhdx and vhd
 Creates a VHDX virtual hard drive from the contents of --tdest. debugWhen true, enables debug messages.
```
# <b>Windows Memory Aquisition Tools</b>
<li> WinPMEM:  https://github.com/Velocidex/c-aff4/releases
<li> DumpIt:  http://www.comae.io
<li> F-Response and SANS SIFT  www.f-response.com
<li> Belkasoft Live RAM Capturer  forensic.belkasoft.com/en/am-capturer
<li> MagnetForensics Ram Capture  magnetforensics.com/free-tool-magnet-ram-capture

# <b>Volatility</b>
## https://code.google.com/p/volatility/wiki/CommandReference23
## Powerful Memory Analysis Framework with crowd source plugins
`vol.py -f [image] --profile=[profile] [plugin]`
```
# <b>Set an envviroment Variable to replace `-f [image]`</b>
function SetVsrc(){
 export VOLATILITY_LOCATION=$1
 }

 SetVsrc Myfile.mem
 vol.py --profile=Win10x64 pslist

 unset VOLATILITY_LOCATION
```
##### Options:

 `-h with plugin to get details`
```
vol.py malfind -h
 -D Dump_Dir, --dump-dir=DUMP_DIR, (dir in which to dump exe files)
 -Y Yara_Rules, --yara-rules=YARA_RLES (use rules as well as finding injected code)
 -K, --Kernal scan kernal modules
```
<i>
see profiles and registered objects, use `--info`
</i><b>
<br>
<br>
View availabile plugins located in:</b>

> /usr/local/src/Volatility/volatility/plugins/</b><br>

More Examples:  
--------------
<br>

- <b>pstree</b> plugin- Output Processes to dot file viewer or image file
`vol.py -f <memory.img> --profile=<profile> pstree --output=dot --output-file=pstree.dot`

- <b> dlllist </b> plugin
`vol.py -f memory.img --profile=Win10x64_16299 dlllist -p 6000`

- <b>modscan/modules</b> plugins 
`vol.py -f memory.img --profile=Win10x64_16299 modscan `
`vol.py -f memory.img modules`

- <b>dlldump</b> output, dump the dll for process at PID 6000, base offset 01234567, also can use regex; (-r [string])
`vol.py -f memory.img dlldump -p 6000 [-b 0x01234567 | -r string] --dump-dir=/dir/to/output2`

- <b>moddump </b> use -r regex, base offset -b, or dump all by omitting
`vol.py -f memory.img moddump [-r string | -b 0x01234567] --dump-dir=/dir/to/dump/to`

- <b> getsids </b> plugin
`vol.py -f memory.img --profile=Win10x64_16299 getsids -p 6000`

- <b> Handles </b> Plugin - Supress and look at Type File and Key(reg)
`vol.py -f memory.img --profile=Win10x64_16299 handles -s -t File,Key -p 6000`

- <b> ssdt</b> plugin - find rootkit hooks
`vol.py -f memory.img ssdt \| egrep -v '(ntoskrnl\|win32k) `

- <b> apihooks</b> plugin - more rootkit fun
`vol.py -f memory.img apihooks`

- <b> malfind </b> plugin -page_execute_readwrite, look for Executable PE codes
`vol.py -f memory.mig --profile=Win10x64_16299 malfind | grep -B4 -A2 -ei 'MZ|ELF|NE|OMF' | grep process`
<br><br>
- <b> procdump</b> plugin, 

```
vol.py -f memory.img procdump --dump-dir=/dir/to/dump/to

Options:
-p PID
-o memory offset
-n regex, used to find process name
```

- <b> memdump</b> plugin,
> contains every mem section owned by process, strings analysis can proof useful.

```
vol.py -f memory.img memdump -p 6000 --dump-dir=/dir/to/dump/to
strings -t d -e l /dir/to/dump/to/*.dmp

Options:
-p PID
-n regex, used to find process name
```

- <b> filescan</b>

>plugin, compliments dumpfiles

`vol.py -f memory.img filescan`
<br>

- <b> dumpfiles</b> plugin 
`vol.py -f memory.img dumpfiles -n -i -r \\.dat -D .`

```
Options:

-D / --dump-dir=path
-Q phys. offset of File_Object
-r regular expression (-r) 
-i case insensitive
-n original filename in output
```

 MemProcFS
=========
<b>Author: Ulf Frisk</b>
https://github.com/ufrisk/MemProcFS<br>
> MemProcFS is an easy and convenient way of viewing physical memory as files in a virtual file system.  
>
> Easy trivial point and click memory analysis without the need for complicated commandline arguments! Access memory content and artifacts via files in a mounted virtual file system or via a feature rich application library to include in your own projects!

<b>Usage:</b>
> Start MemProcFS from the command line - possibly by using one of the examples below.
> Or register the memory dump file extension with MemProcFS.exe so that the file system is automatically mounted when double-clicking on a memory dump file!

<b> Examples: </b>
- mount the memory dump file as default M: <br>`memprocfs.exe -device c:\temp\win10x64-dump.raw`
- mount the memory dump file as default M: with extra verbosity: <br>`memprocfs.exe -device c:\temp\win10x64-dump.raw -v`
- mount the memory dump file as default M: and start forensics mode: <br>`memprocfs.exe -device c:\temp\win10x64-dump.raw -forensic 1`
- mount the memory dump file as /home/pi/mnt/ on Linux: <br>`./memprocfs -mount /home/pi/linux -device /dumps/win10x64-dump.raw`
- mount the memory dump file as S: <br>`memprocfs.exe -mount s -device c:\temp\win10x64-dump.raw`
- mount live target memory, in verbose read-only mode, with DumpIt in /LIVEKD mode: <br>`DumpIt.exe /LIVEKD /A memprocfs.exe /C "-v"`
- mount live target memory, in read-only mode, with WinPMEM driver: <br>`memprocfs.exe -device pmem`
- mount live target memory, in read/write mode, with PCILeech FPGA memory acquisition device: <br>`memprocfs.exe -device fpga -memmap auto`
- mount a memory dump with a corresponding page files: <br>`memprocfs.exe -device unknown-x64-dump.raw -pagefile0 pagefile.sys -pagefile1 swapfile.sys`

YARA 
-----
Originaly created by VirusTotal to classify malware samples.
Syntax
<br>

- Preconfigured Rules file
> yara64.exe -C compiled-rules-file <file or directory>

- Options
```
yara64.exe -[C|c|f|r|p] rules <file/dir>
 
 [Useful Options]
 -C:Load pre-compiled rules
 -c:Print only number of matches
 -f:Fast matching mode-w:Disable warnings
 -r:Recursively search directories
 -p <threads>:Use specified number of threads during scanning
```
</br>

> To use a rules file, you can only specify one static file.  
Must utilize an index file if utilizing signatures from multilpe files.
</br>

<b> Index file example:</b>
 
 Common_APT1_Custom.rules
```
 #Source sig files to include
 include "<dir>\000_common_rules.yar"
 include "<dir>\APT_APT1.yar"
 include "<dir>\custom_signatures.yar"
```
<br>
<b>Many precompiled rules exist already:</b>

> Yara Rules Github:
> https://github.com/Yara-Rules/rules

Density Scout
-------------
> Author: Christian Wojner @Cert Aus.
> https://www.cert.at/en/downloads/software/software-densityscout

<b>Purpose</b>: Find Suspicous Files

<br>
<b>Syntax:</b>

```

densityscout -pe -r -p 0.1 -o results.txt <directory-of-exe>

 [Useful Options]
 -a:Show errors and empties, too
 -d:Just output data
 -l:Lower than the given density
 -n:Print number lines
 -m:Mode ABS (default) or CHI (for filesize > 100 Kb)
 -o file:File to write output to
 -p density:Immediately print if lower than the given density
 -r: Walk recursively
 -s suffix(es): Filetype(s) (i.e., dll or exe,...)
 -S suffix(es): Filetype(s) to ignore (i.e., dll or dll,exe)
 -pe: Include all portable executables by magic number
 -PE: Ignore all portable executables by magic number

```




sigcheck.exe
------------
> Sysinternals Tool
> find unsigned binaries

<b>Syntax and Options:</b>

```
sigcheck.exesigcheck [options] file or directory

[Useful Options]
-a Show extended version information
-c csv output
-e Scan executable images only
-h Show file hashes
-s Recurse subdirectories
-u Show files that are unknown if VirusTotal check is enabled; otherwise, show only unsigned files.-v[rs] Query VirusTotal for malware based on file hash. Add 'r' to open reports for files with non-zero detection. Files reported as not previously scanned will be uploaded to VirusTotal if the 's' option is specified. 
-t[u][v] Dump contents of specified certificate store ('*' for all stores). Specify -tu to query the user store (machine store is the default).  Append '-v' to have Sigcheck download the trusted Microsoft root certificate list and only output valid certificates not rooted to a certificate on that list. If the site is not accessible, authrootstl.cab or authroot.stl in the current directory are used instead, if present.

```

Capa
----
> Realesed by FireEye FLARE 
> Rules written in yamls to do triage & detection; inspects fileheaders, APIs, strings, and disassmbled components

```
capa.exe -f pe -v <file>

capa [options] <file>

[Useful Options]
 -v:Enable verbose results
 -vv:Enable very verbose results
 -f <format>:Choose between PE or shellcode analysis (pe,sc32,sc64)
 -r RULES:Specify alternative rules directory
 -t TAG:Filter on a specific rule meta field value
 -j:Output JSON instead of text 

```

MFTECmd
-------

> Master File Table, Filesystem Journals and NTFS System Files tool to extract data
> author: E.Zimmerman
> https://github.com/EricZimmerman/MFTECmd


```

```

```
MFTECmd.exe -f "<file>" --body "<dir>" --bodyf mft.body --blf --bdl C:

-f "<filename>" = $MFT|$J|$Boot|$SDS to process
--csv "<dir>"= Dir to save CSV (tab separated)--csvf name= Filename to save CSV
--body "<dir>"  = Dir to save CSV
--bodyf name  = Filename to save CSV--bdl name = Drive letter (C, D, etc.) to use with bodyfile
--blf = When true, use LF vs CRLF for newlines. Default is FALSE
```



<b>Examples: </b> 

```
MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out" --csvf MyOutputFile.csv 
MFTECmd.exe -f "C:\Temp\SomeMFT" --csv "c:\temp\out"MFTECmd.exe -f "C:\Temp\SomeMFT" --json "c:\temp\jsonout"
MFTECmd.exe -f "C:\Temp\SomeMFT" --body "c:\temp\bout" --bdl cMFTECmd.exe -f "C:\Temp\SomeMFT" --de 5-5
```

TSK (the Slueth Kit tools)
-----

- <b>fls</b> 
>fls tool within the TSK (the slueth kit) suite is designed to extract filename and metadata information for files

```
Usage: fls [options] image [inode]

Useful Options for fls

-d:  Display deleted entries only
-r:  Recurse on directorie
-p:  Display full path when recursing
-m:  Display in timeline bodyfile format
-s <sec>: Timeskew correction for system in seconds
```

- <b>MacTime</b>
> tool that tases a file and parses it to present it to a readable format

```
mactime [options] -d -b bodyfile -z timezone > timeline.csv

[Useful Options for mactime]
-b: Bodyfile location (data file) 
-y: Dates are displayed in ISO 8601 format
-z: Specify the time zone (see time zone chart)
-d: Comma-delimited format Optional: Date Range (yyyy-mm-dd..yyyy-mm-dd)Example: 2020-01-01..2020-6-01

```
- <b>istat</b> 
> Displays statistics about metadata structure aka inode supports multiple image types and file systems
```
istat [options] image inode

-z zone:  Time zone of original machine (i.e. EST5EDT or GMT)
-s seconds:  Time skew of original machine (in seconds)
```

- <b>icat</b>
> extracts file or attribute contents from MFT inodes; useful to retrieve metadata from inodes marked delete and Alt. Data streams

```
icat [options] image inode > new.file
-r:      Recover deleted file
-s:      Display slack space at end of file
``` 

Plaso / log2timeline.py 
---------------
> Author: Kristinn Guðjónsson
> Artifact Extraction to create timelines from multiple sources
> https://github.com/log2timeline/plaso/tree/main/data
> https://plaso.readthedocs.io/en/latest/

<i>log2timeline.py [STORAGE FILE] [SOURCE]</i>

<b>Examples:</b>
- <b>Raw file </b></br>            `log2timeline.py /dir/file.dump /dir/file.dd`
- <b>EWF file </b></br>            `log2timeline.py /dir/file.dump /dir/file.E01`
- <b>Virtual Disk file</b></br>    `log2timeline.py /dir/file.dump /dir/triage.vhdx`
- <b>Physical Device </b></br>     `log2timeline.py /dir/file.dump /dev/sdd`
- <b>Volume(partitoin)</b></br>    `log2timeline.py --partition 2 /dir/file.dump /dir/file.dd`
- <b>Triage Folder </b></br>       `log2timeline.py /dir/file.dump /triage-output/`
- <b>Parser Presets</b></br>       `log2timeline.py --parsers "win7,!filestat" plaso.dump <target>`
- <b>Filter Files </b></br>        `log2timeline.py  -f filter_windows.txt  plaso.dump  <target>`

> -f FILTER_FILE, --file_filter FILTER_FILE, --file-filter FILTER_FILE
 Filters and output are in Yaml or Text based 
> 
> https://plaso.readthedocs.io/en/latest/sources/user/Collection-Filters.html

<b>pinfo.py -v plaso.dump</b>
> Will provide you information on the plaso db file, inc. internal metadata, what was parsed how it was parsed (plugins/filters), preproc. info, ect.

<b>psort.py</b>
> psort.py --output-time-zone 'UTC' -o [l2tcsv|elastic] -w [filename] plaso.dump FILTER date [ < or > ] datetime('2000-01-01T00:00:00')


libvshadow
----------
> Author: Joachim Metz
> VSS Inspection
> https://github.com/libyal/libvshadow

- <b>Vsshadowinfo</b> VSS list
> vsshadowinfo -o <offset> raw_disk_source_file


- <b>vshadowmount</b> Mount the vss as a disk
> vshadowmount [ -o offset ] raw_disk_source_file /mnt/VSS
>
> Do a list of the DIR and then mount the VSS file desired
> mount -o ro,loop,show_sys_files,streams_interface=windows <vss> /mnt/dir/<vss>
