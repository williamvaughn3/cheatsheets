#

## EvtxECmd 

### Author: Eric Zimmerman (saericzimmerman@gmail.com)
### https://github.com/EricZimmerman/evtx

Description: EvtxECmd is a command line tool for parsing Windows Event Log (EVTX) files. It can be used to extract events from a single file or a directory of files. It can also be used to export events to CSV, JSON, or HTML.


** options **
```
    - d               Directory to process that contains evtx files. This or -f is required
    - f               File to process. This or -d is required
    - csv             Directory to save CSV formatted results to.
    - csvf            File name to save CSV formatted results to. When present, overrides default name
    - json            Directory to save JSON formatted results to.
    - jsonf           File name to save JSON formatted results to. When present, overrides default name
    - xml             Directory to save XML formatted results to.
    - xmlf            File name to save XML formatted results to. When present, overrides default name
    - dt              The custom date/time format to use when displaying time stamps. Default is: yyyy-MM-dd HH:mm:ss.fffffff
    - inc             List of Event IDs to process. All others are ignored. Overrides --exc Format is 4624,4625,5410
    - exc             List of Event IDs to IGNORE. All others are included. Format is 4624,4625,5410
    - sd              Start date for including events (UTC). Anything OLDER than this is dropped. Format should match --dt
    - ed              End date for including events (UTC). Anything NEWER than this is dropped. Format should match --dt
    - fj              When true, export all available data when using --json. Default is FALSE.
    - tdt             The number of seconds to use for time discrepancy detection. Default is 1 second
    - met             When true, show metrics about processed event log. Default is TRUE.
    - maps            The path where event maps are located. Defaults to 'Maps' folder where program was executed
    - vss             Process all Volume Shadow Copies that exist on drive specified by -f or -d . Default is FALSE
    - dedupe          Deduplicate -f or -d & VSCs based on SHA-1. First file found wins. Default is TRUE
    - sync            If true, the latest maps from https://github.com/EricZimmerman/evtx/tree/master/evtx/Maps are downloaded and local maps updated. Default is FALSE
    - debug           Show debug information during processing
    - trace           Show trace information during processing
```

Examples Syntax:
```        
    EvtxECmd.exe -f "C:\Temp\Application.evtx" --csv "c:\temp\out" --csvf MyOutputFile.csv
    EvtxECmd.exe -f "C:\Temp\Application.evtx" --csv "c:\temp\out"
    EvtxECmd.exe -f "C:\Temp\Application.evtx" --json "c:\temp\jsonout"
```
##### Short options (single letter) are prefixed with a single dash. Long commands are prefixed with two dashes

# Event Log Maps
### Opensource / Crowd Sourced maps
### https://github.com/EricZimmerman/evtx/tree/master/evtx/Maps

#### Example of a Map:
```
---- START MAP HERE ----

Author: Eric Zimmerman saericzimmerman@gmail.com
Description: Security 4624 event
EventId: 4624
Channel: Security
Maps:
  -
    Property: UserName
    PropertyValue: "%domain%\\%user%"
    Values:
      -
        Name: domain
        Value: "/Event/EventData/Data[@Name=\"SubjectDomainName\"]"
      -
        Name: user
        Value: "/Event/EventData/Data[@Name=\"SubjectUserName\"]"
  -
    Property: RemoteHost
    PropertyValue: "%workstation% (%ipAddress%)"
    Values:
      -
        Name: ipAddress
        Value: "/Event/EventData/Data[@Name=\"IpAddress\"]"
      -
        Name: workstation
        Value: "/Event/EventData/Data[@Name=\"WorkstationName\"]"
  -
    Property: PayloadData1
    PropertyValue: LogonType %LogonType%
    Values:
      -
        Name: LogonType
        Value: "/Event/EventData/Data[@Name=\"LogonType\"]"

# Valid values for the Property field include:
# UserName
# RemoteHost
# ExecutableInfo --> used for things like process command line, scheduled task, info from service install, etc.
# PayloadData1 through PayloadData6
---- END MAP HERE ----
```

Map files are read in order, alphabetically. This means you can create your own alternative Maps to the default by doing the following:

make a copy of the Map you want to modify
name it the same as the Map you are interested in, but prepend 1_ to the front of the filename.
edit the new Map to meet your needs

Example:

    Security_Microsoft-Windows-Security-Auditing_4624.Map is copied and renamed to:
    1_Security_Microsoft-Windows-Security-Auditing_4624.Map
    Edit 1_Security_Microsoft-Windows-Security-Auditing_4624.Map and make your changes
    When the Maps are loaded, since 1_Security_Microsoft-Windows-Security-Auditing_4624.Map comes before Security_Microsoft-Windows-Security-Auditing_4624.Map, only the one with your changes will be loaded.
    This also allows you to update default Maps without having your customizations blown away every time there is an update.

TIPS:

    If you are looking to make an Application.evtx Map, please include a Provider as they are many instances where the same event ID number is used for multiple providers. I've personally observed 4 Providers use Event ID 1 which without a Provider being listed for that Map it made all 4 events, regardless of Provider, be Mapped incorrectly. When in doubt, add a Provider to your Map. Follow a template from a previously created Map to ensure it's made correctly.

    