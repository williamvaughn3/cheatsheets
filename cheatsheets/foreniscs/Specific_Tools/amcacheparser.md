AmcacheParser version 1.4.0.0
Author: Eric Zimmerman (saericzimmerman@gmail.com)
https://github.com/EricZimmerman/AmcacheParser
#
```
- b               Path to file containing SHA-1 hashes to *include* from the results. Blacklisting overrideswhitelisting
- f               Amcache.hve file to parse. Required
- i               Include file entries for Programs entries
- w               Path to file containing SHA-1 hashes to *exclude* from the results. Blacklisting overrideswhitelisting
- csv             Directory where CSV results will be saved to. Required
- csvf            File name to save CSV formatted results to. When present, overrides default name
- dt              The custom date/time format to use when displaying timestamps. See https://goo.gl/CNVq0k foroptions.Default is: yyyy-MM-dd HH:mm:ss
- mp              When true, display higher precision for timestamps. Default is FALSE
- nl              When true, ignore transaction log files for dirty hives. Default is FALSE
- debug           Show debug information during processing
- trace           Show trace information during processing
```
#
### Examples: 
```
AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" --csv C:\temp
AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" -i on --csv C:\temp --csvf foo.csv
AmcacheParser.exe -f "C:\Temp\amcache\AmcacheWin10.hve" -w "c:\temp\whitelist.txt" --csv C:\temp
```
### Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes