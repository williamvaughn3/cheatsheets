#

# appcompatprocessor.py 
"Evolving AppCompat/AmCache data analysis beyond grep"

AppCompatProcessor has been designed to extract additional value from enterprise-wide AppCompat / AmCache data beyond the classic stacking and grepping techniques.
Written by  Matias Bevilacqua
https://github.com/mbevilacqua/appcompatprocessor

# Useful Modules:
```
search:
  Search the database for regular expression matches.  The tool comes with over one hundred pre-built regular expressions and can be easily extended via a text file
fsearch:
     Search using a single database field (FileName, FilePath, Size, LastModified, ExecFlag, etc.) 
filehitcount: 
    Simple stack of frequency of each executable found
tcorr: 
    Temporal correlation of execution, finding files that regularly execute either before or after each other to identify patterns and additional files of interest
reconscan: 
    Search for a collection of common recon tools executed in close proximity to one another and create a score for how likely it is each host experienced recon activity (list shows results)
leven: 
    Find slight file name deviations to identify files trying to hide in plain sight with similar names (i.e., svchos.exe, lssass.exe, cssrs.exe, etc.)
stack: 
    Perform least frequency of occurrence using specific database fields
rndsearch: 
    Attempt to identify randomly named files28© 2021 Rob Lee© SANS Institute 2021
```
### From authors github:

```
load 'path': Load (or add new) AppCompat/AmCache data from 'path'
Check [Ingestion Modules](#Ingestion Modules) for a list of supported formats
`./AppCompatProcessor.py ./database.db load ./path/to/load`
Load will recurse down any available folders to identify files to load.
`./AppCompatProcessor.py ./database.db load ./path/to/file.zip`
Load will do in-memory processing of the zip file and load its contents.
```


`./AppCompatProcessor.py ./database.db fsearch list`
['rowid', 'hostid', 'entrytype', 'rownumber', 'lastmodified', 'lastupdate', 'filepath', 'filename', 'size', 'execflag', 'sha1', 'filedescription', 'firstrun', 'created', 'modified1', 'modified2', 'linkerts', 'product', 'company', 'pe_sizeofimage', 'version_number', 'version', 'language', 'header_hash', 'pe_checksum', 'switchbackcontext', 'recon', 'reconsession']

`./AppCompatProcessor.py ./database.db fsearch FileName -F "cmd.exe"`
    Will search the FileName field for anything that contains 'cmd.exe' 

`./AppCompatProcessor.py ./database.db fsearch FileName -F "=cmd.exe"`
    Will search the FileName field for anything that exactly matches 'cmd.exe' 

`./AppCompatProcessor.py ./database.db fsearch Size -F "4096"`
    Will find files whose size contains "4096" 

`./AppCompatProcessor.py ./database.db fsearch Size -F "=4096"`
    Will find files whose size _is_ "4096" 

`./AppCompatProcessor.py ./database.db fsearch Size -F ">4096"`
    Will find files whose size is bigger than 4096 bytes (and has Size data of course: XP appcompat or AmCache data)

`./AppCompatProcessor.py ./test-AmCache.db fsearch Product -F "Microsoft@"`
    Will find files for some attackers that regularly screwed the trademark symbol on the versioning information on their tools.

`./AppCompatProcessor.py ./delete.db fsearch FirstRun -F ">2015-01-18<2015-01-21"`
    (nope sorry, just use sqlite if you want to get that fancy!: "SELECT * FROM Csv_Dump WHERE LastModified BETWEEN '2015-01-18' and '2015-01-21'")

`./AppCompatProcessor.py ./database.db fsearch FileName -f "=cm[ad].exe"`
Will search the FileName field for anything that exactly matches against the regular expression '^cmd[ad].exe$' 

`./AppCompatProcessor.py ./database.db fsearch --sql "(FilePath || '\\' || FileName)" -f "Windows\\hkcmd.exe"`
    Will search for entries who's fullpath contains Windows\hkcmd.exe. This sql tweak is exactly what happens by default with the Search module BTW.
    *Note: The weird syntax there is what SQL expect you to use to concatenate two fields with a backslash separator. You can use this as an example of how to build custom search spaces.*