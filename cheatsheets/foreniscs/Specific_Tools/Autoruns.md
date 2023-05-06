#

### Autorunsc 
##### A command line version of Autoruns. Its syntax is:

Usage: 
```
autorunsc [-a <*|bdeghiklmoprsw>] [-c|-ct] [-h] [-m] [-s] [-u] [-vt] [[-z <systemroot> <userprofile>] | 
[user]]]
    -a   Autostart entry selection:  * All.
    -b    Boot execute.
    -c    Codecs.
    -d    Appinit DLLs.
    -e    Explorer add-ons.
    -g    Sidebar gadgets (Vista and higher)
    -h    Image hijacks.
    -i    Internet Explorer add-ons.
    -k    Known DLLs.
    -l Logon startups (this is the default).
    -m    WMI entries Winsock protocol and network providers.
    -o Office add-ins.
    -p    Printer monitor DLLs.
    -r    LSA security providers.
    -s    Autostart services and non-disabled drivers.
    -t    Scheduled tasks.
    -w    Winlogon entries.
    -c     Print output as CSV.
    -ct    Print output as tab-delimited values.
    -h     Show file hashes.
    -m     Hide Microsoft entries (signed entries if used with -s).
    -s     Verify digital signatures.
    -t     Show timestamps in normalized UTC (YYYYMMDD-hhmmss).
    -u     If VirusTotal check is enabled, show files that are unknown by VirusTotal or have non-zero detection; otherwise, show only unsigned files.
    -x     Print output as XML.

    -v[rs]   Query VirusTotal (www.virustotal.com) for malware based on file hash. Add 'r' to open reports for files with non-zero detection. Files reported as not previously scanned will be uploaded to VirusTotal if the 's' option is specified. Note scan results may not be available for five or more minutes.

    -vt    Before using VirusTotal features, you must accept VirusTotal terms of service.
    See: https://www.virustotal.com/en/about/terms-of-service/If you haven't accepted the terms and you omit this option, you will be interactively prompted.    

    -z      Specifies the offline Windows system to scan.
    -user   Specifies the name of the user account for which autorun items will be shown. Specify '*' to scan all use  profiles.
    -nobanner   Do not display the startup banner and copyright message.
    