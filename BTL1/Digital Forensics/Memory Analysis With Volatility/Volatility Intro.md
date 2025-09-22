Volatility is an open-source memory forensics framework for incident response and malware analysis.

This is a very powerful tool, and we can complete lots of interactions with memory dump files, such as:

- **List all processes that were running.**
- **List active and closed network connections.**
- **View internet history (IE).**
- **Identify files on the system and retrieve them from the memory dump.**
- **Read the contents of notepad documents.**
- **Retrieve commands entered into the Windows Command Prompt (CMD).**
- **Scan for the presence of malware using YARA rules.**
- **Retrieve screenshots and clipboard contents.**
- **Retrieve hashed passwords.**
- **Retrieve SSL keys and certificates.**
- **And lots more!**

## Volatility Walkthrough

 you need to understand a fundamental concept about how Volatility actually works:

- **Volatility needs profiles to work.** When we have the memory image file we want to analyze we first need to use the command

`volatility -f memdump.mem imageinfo`

- Once this command is run, Volatility will identify the system the memory image was taken from, including the operating system, version, and architecture. For example, if we took a memory image from a Windows 7 machine with Service Pack 1 and it had a 64-bit architecture, Volatility would tell us the best profile to use is Win7SP1x64. In the below screenshot, we can see that this memory image has been given a suggested profile of WinXPSP2x86 (Windows XP, Service Pack 2, 32-bit architecture). When running any other command on this memory image we need to provide the profile somewhere, in the format `--profile=WinXPSP2x86`, otherwise, the command will not run.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0ef876fea758d23ec6c92ef887b7e4b41e229dc061179b1da9de222c7540de5a73a7d7042af796a8647e441533bd.png)

## Command List

`volatility -f memdump.mem imageinfo` **//** Take memory image “memdump.mem” and determine the suggested profile for analysis. The profile is the operating system, version, and architecture.

`volatility -f memdump.mem --profile=PROFILE pslist` **//** Take memory image, provide the profile, then use the **pslist** plugin to print a list of processes to the terminal.

`volatility -f memdump.mem --profile=PROFILE pstree` **//** Use the **pstree** plugin to print a process tree to the terminal.

`volatility -f memdump.mem --profile=PROFILE psscan` **//** Use the **psscan** plugin to print all available processes, including hidden ones often used by malware (compare this to pslist to see if there’s any differences!).

`volatility -f memdump.mem --profile=PROFILE psxview` **//** Use the plugin psxview plugin to print expected and hidden processes. This is a combination of pslist and psscan plugins.

`volatility -f memdump.mem --profile=PROFILE procdump -p PIDHERE` **//** Use the **procdump** plugin to save a process as a file. You must provide a process ID using the -p flag.

`volatility -f memdump.mem --profile=PROFILE netscan` **//** Use the plugin **netscan** to identify any active or closed network connections.

`volatility -f memdump.mem --profile=PROFILE timeliner**` **//** Use the **timeliner** plugin to create a timeline of events from the memory image.

`volatility -f memdump.mem --profile=PROFILE iehistory` **//** Use the **iehistory** plugin to pull internet browsing history.

`volatility -f memdump.mem --profile=PROFILE filescan` **//** Use the **filescan** plugin to identify any files on the system from the memory image.

`volatility -f memdump.mem --profile=PROFILE cmdline -p PIDHERE` **//** Use the **cmdline** plugin to retrieve any command-line arguments passed to a process. You must provide a process ID using the -p flag.

`volatility -f memdump.mem --profile=PROFILE dumpfiles -n --dump-dir=./` // Use the **dumpfiles** plugin to retrieve files from the memory image. In this case our terminal is open in the Desktop (root@SBTLab2:~/Desktop) and we are using the output location `./` which tells Volatility to put the files in our current location, the Desktop.