# Probabilistic Optimization of System Wide Performance Characteristics in WindowsOS using PowerShell.

> The most important aspect of the final script would be that the user doesn’t even need to specify what type of error he/she is facing, the script will auto-’magically’ pull data from logs, determine the type of error and try to fix that. A realistic and useful aim would be solve a problem for which there is no troubleshooter available.

- To automate system file integrity checking, SFC and DISM can be used.
    - Additional rules can be applied, for eg. using task scheduler to trigger the script when a critical warning has lead to a sudden reboot. This can be looked by event viewer.
    - Another thing, after running SFC, if problems were found and fixed, them system needs to restart, but upon restart, either the script should continue to run or TS should run another     script based on the restart event.
        - This should be the first in script even before SFC and DISM, that would optimize later processes.

- To automate storage optimization across all drives, disk defragmenter can be used.

- `ExecutionPolicy` should be set to unrestricted for the instance in which the script will run. `ExecutionPolicy` will be set to default before exiting.

- The script might check when passwords were last changed, checks if Windows Updates are pending, checks if the user has a local or cloud backup. Thus, they can come under security recommendations.

- Script can record itself into the event log. If it was run in the past 14 days (or a custom/any other time period), then it can inform the user about this, put up a choice, if they want to run it or not.

- Script can perform security functions by recognizing suspicious processes and kill them.

- Most importantly, the script will collect logs, there will be functions for determining problems that the system might be facing. Those functions should calculate probabilities to determine (with best possible confidence) possible problem(s), and based on that probability, it should trigger specific remediation methods (specific to the determined problem). Specifically, critical or warning logs can be looked into, for better determination.

- **Windows Updates**: Even windows updates can be based on the EventLog. The logs can be searched for the last time the system was updated and based upon that (for eg., if the last time the system was updated was more than 40 days ago, chances are, that the system is not updated. Also the script may attempt to turn on automatic updates after updating. Moreover, even before checking for updates manually the script can straightaway check if automatic updates are enabled, if they are, then it can skip to checking for updates), the function should decide whether to check for updates or not.

- **Network Optimization**: Script can renew DHCP lease, configure DNS to CloudFlare (More rules can be added!)

- **Disk Optimization**: Script can check when the disk was last optimized

- Each of the mentioned Sub-Sections can later be converted into structures containing functions. But this is a speculation.

- This being a custom script. The usual naming conventions were not strictly followed because of the following reasons:
    - To make more functions more descriptive, their type is mentioned after the function that it performs. And that function not being normal, is written in a way to be descriptive.
    - To avoid conflict with existing functions and cmdlets within PowerShell.
    - Some functions names are esoteric, meaning, they are unique to this script.
    - Moreover, these functions are defined inside script, they are not called directly in a command-line.

- [Guide to optimize PowerShell scripts](https://www.itprotoday.com/powershell/tips-optimizing-powershell-scripts)

- There should be extensive focus on reducing restarts.

- Various functional tests are implemented, in-line with the best practices of unit testing. Best example being the `$MasterInputDispatchCenterFunctionStatus` **variable without which being set to true the script cannot perform maintenance tasks and all the sub-sections will not run.

- An important thing to keep in mind while determining the cause of a particular problem, is to analyse what was going on when the problem happened or in other words, what was the state?

- Maybe the script should put more focus on security