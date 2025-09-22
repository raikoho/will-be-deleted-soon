## .lnk

When user delete a file, even from the trash, the .lnk (ярлик) wll be stored anyway in the Recent Docs folder and still point to the original location file. Use exiftool to this .lnk to view even more detail about time:

![[Pasted image 20250130111843.png]]

`C:\Users\tcm\AppData\Roaming\Microsoft\Windows\Recent Items\`
use this path to the .lnk

-----
## Prefetch Files

Prefetch files (.pf) are Windows system files that help speed up the loading of frequently used applications. They are stored in:

`C:\Windows\Prefetch`

### **How to Use in Forensics?**

1. **Find Execution History** 🕵️‍♂️
    
    - Prefetch files record when and how often a program was run.
    - Useful for detecting malware execution or suspicious activity.
2. **Check Timestamps** ⏳
    
    - Shows the last time an application was executed.
    - Helps establish a timeline of attacker activity.
3. **Identify Malicious Programs** 🚨
    
    - If an unknown or suspicious `.pf` file exists, it may indicate malware.

### **How to Analyze?**

📌 Use tools like:

- `PECmd.exe` (part of Kroll’s free EZ Tools)
- `WinPrefetchView` (GUI-based)
- `Forensic Suite Tools` (e.g., Autopsy, X-Ways)

### PECmd

use program Prefetch Parcer: `PECmd` : - [https://ericzimmerman.github.io/#!index.md](https://ericzimmerman.github.io/#!index.md)

This program can tell us where it is on the disk:

![[Pasted image 20250130112547.png]]

------

## Jump Lists

Jump Lists are Windows artifacts that track recently accessed files, folders, and applications. They are stored in:  
📂 `C:\Users\{User}\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations\`  
📂 `C:\Users\{User}\AppData\Roaming\Microsoft\Windows\Recent\CustomDestinations\`

- [https://github.com/EricZimmerman/JumpList/blob/master/JumpList/Resources/AppIDs.txt](https://github.com/EricZimmerman/JumpList/blob/master/JumpList/Resources/AppIDs.txt)
### **How to Use in Forensics?**

1. **Find User Activity** 🕵️‍♂️
    
    - Shows which files, documents, or apps were accessed.
    - Helps track what an attacker did on the system.
    
1. **Recover Deleted Evidence** 🗑️
    
    - Even if a file was deleted, its reference may still be in a Jump List.
3. **Detect Suspicious Activity** 🚨
    
    - If an attacker opened hacking tools or sensitive documents, Jump Lists can reveal this.

### **How to Analyze?**

📌 Use tools like:

- `JLECmd.exe` (part of Kroll’s EZ Tools)
- `JumpList Explorer`
- `Autopsy` (forensic suite)

### **Example:**

🔍 **Tracking an Attacker’s Activity**

- If `cmd.exe` or `mimikatz.exe` appears in a Jump List, it means someone used these tools on the system.