## Metasploit crate a task:
```
shell

schtasks /create /tn "SystemCleanUp" /tr "C:\users\tcm\downloads\malware.exe" /sc daily /st 09:00 /ru SYSTEM
```

## Analysis

go to TaskScheduler -> Active Tasks

-------------

`schtasks /query /fo LIST` // list of all scheduled tasks

`schtasks /query /tn "SystemCleanup"` // specific scheduled tasks

`schtasks /query /tn "SystemCleanup /v /fo LIST"` // specific scheduled tasks with detailed mode

![[Pasted image 20250127131932.png]]

## Use Autoruns Sysinternals!

![[Pasted image 20250127132030.png]]
## PowerShell

- [https://github.com/p0w3rsh3ll/AutoRuns](https://github.com/p0w3rsh3ll/AutoRuns)