#

#  Prefetch Explorer Command Line 
Aurthor: Eric Zimmerman
https://github.com/EricZimmerman/PECmd

### To audit or disable Prefetch:

```
Key: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory `

Management\PrefetchParameters
Value: EnablePrefetcher
Type: REG_DWORD
Value: 0
```

```
The EnablePrefetcher value has the following settings:
0 = Disabled
1 = Application launch prefetching enabled
2 = Boot prefetching enabled
3 = Application launch and boot enabled
```
To disable Prefetch, set the value to 0.
```
-d          Directory to recursively process. Either this or -f is required
-f          File to process. Either this or -d is required
-k          Comma-separated list of keywords to highlight in output. By default, 'temp' and 'tmp' are highlighted. Any additional keywords will be added to these
-q          Do not dump full details about each file processed. Speeds up processing when using --json or –-csv
-json       Directory to save json representation to. Use --pretty for a more human-readable layout
-csv        Directory to save CSV (tab separated) results to. Be sure to include the full path in double quotes
-html       Directory to save xhtml formatted results to. Be sure to include the full path in double quotes
-pretty     When exporting to json, use a more human-readable layout
-dt         The custom date/time format to use when displaying timestamps. 
-mp         When true, display higher precision for timestamps. Default is false
```
Syntax Examples: 
```
PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf"
PECmd.exe -f "C:\Temp\CALC.EXE-3FBEF7FD.pf" --json "D:\jsonOutput" --jsonpretty
PECmd.exe -d "C:\Temp" -k "system32, fonts"
PECmd.exe -d "C:\Temp" --csv "c:\temp" --local --json c:\temp\json
PECmd.exe -d "C:\Temp" --csv "c:\temp" --csvf foo.csv
PECmd.exe -d "C:\Windows\Prefetch"
```
Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes