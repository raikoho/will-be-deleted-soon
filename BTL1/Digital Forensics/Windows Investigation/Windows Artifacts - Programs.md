## Windows Artifacts - Programs

This lesson will focus on artifacts that can be gathered from systems running Windows, specifically focusing on artifacts related to the use of applications and programs on the system. Seeing what files have been run on the system can provide valuable evidence such as: how many times a file has been run, when it was last run, when it was created, full file paths, and more. We will explore the following artifacts:

- **LNK Files**
- **Prefetch Files**
- **Jump List Files**
### [1] LNK Files / Shortcut Analysis

#### Artifact Description

LNK files are used by the Windows OS to link one file to another, which is how we can have application shortcuts that work as a redirector – so when we click on a shortcut it will go and find the application wherever it resides in the file system and runs the corresponding application. We can collect valuable metadata from LNK files such as the location of the folder it is linked to, the date the LNK file was created, modified, last accessed, the file size, and more.
#### Artifact Location

LNK files can be found at: `C:\Users\$USER$\AppData\Roaming\Microsoft\Windows\Recent`
#### Artifact Analysis

To view these files in a human-readable format, we can use [Windows File Analyzer](https://www.mitec.cz/wfa.html).
### [2] Prefetch Files

#### Artifact Description

Prefetch files can provide us with incredibly useful information about programs including the name of the application, the path to the executable file, when the program was last run, and when the program was created/installed.
#### Artifact Location

Prefetch files can be found at: `C:\Windows\Prefetch`
#### Artifact Analysis

To view these files in a human-readable format, we can use [Prefetch Explorer Command Line](https://ericzimmerman.github.io/#!index.md) also known as PECmd.exe.
### [3] Jump List

#### Artifact Description

Using the Windows Jump List feature we are able to find two different types of files: _automaticDestination-ms_ and _customDestination-ms_. These files contain information about applications that are pinned to the taskbar, such as the file path, timestamps, and application identifiers (AppIDs).
#### Artifact Location

The Jump List files can be found at: `C:\Users\% USERNAME%\AppData\ Roaming\Microsoft\Windows\Recent\AutomaticDestinations`  
`C:\Users\%USERNAME%\AppData\ Roaming\Microsoft\Windows\Recent\CustomDestinations`
#### Artifact Analysis

To analyze these files we can use tools such as [JumpList Explorer.](https://ericzimmerman.github.io/#!index.md)