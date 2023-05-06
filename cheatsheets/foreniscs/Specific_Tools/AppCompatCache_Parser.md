#

### AppCompatCacheParser

<i> AppCompatCache Parser version 0.9.7.0
Author: Eric Zimmerman (saericzimmerman@gmail.com)
Supports Windows 7 (x86 and x64), Windows 8.x, and Windows 10
</i>
#
<b> Used to parse an offline SYSTEM hive or to collect data on a live, running system.  It currently parses data from Windows 7 and above systems.    </b>

`*** If a SYSTEM hive is not given the -f switch, the running computer’s AppCompatCache value is processed. `

##### All ControlSets in the SYSTEM hive are queried and processed by default.  This can be benificial and ensures older control set data is included in results.  
#
### USAGE: 

```
Options:
- c       The ControlSet to parse. Default is to extract all control sets
- d       Debug mode
- f       Full path to SYSTEM hive to process. If this option is not specified, the live Registry will be used
- t       Sorts last modified timestamps in descending order
- csv     Directory to save results. Required
- dt      The custom date/time format to use when displaying timestamps
```

### Alternative Option:
### ShimCacheParser.py
written and maintained as a PoC by Mandiant A.K.A now googlecloud.
https://github.com/mandiant/ShimCacheParser

#####  ShimCacheParser.py is utilized on exported .reg files at scale. 
#
##### Example syntax: 
```
    shimcacheparser.py --hive SYSTEM --csv shimcache.csv
    shimcacheparser.py --reg shimcache.reg --csv shimcache.csv
```

<b> Several types of inputs are currently supported:</b>

```
    -Extracted Registry Hives (-i, --hive)
    -Exported .reg registry files (-r, --reg) 
    -MIR XML  (-m, --mir)
    -Mass MIR registry acquisitions ZIP archives (-z, --zip)
    -The current Windows system (-l, --local)
    -Exported AppComatCache data from binary file (-b, --bin) 
```