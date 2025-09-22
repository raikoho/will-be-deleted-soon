One of the most important changes is that profiles are no longer required when running commands. Remember in Vol 2 when we had to initially run `volatility -f memdump.mem imageinfo` to get the right profile? And then we used that value in every subsequent command (like `volatility -f memdump.mem --profile=Win7SP1x64 pslist`). That's gone.

|Command Purpose|**Volatility 2 Command**|**Volatility 3 Command**|
|---|---|---|
|Get process tree|volatility --profile=PROFILE pstree -f file.dmp|python3 vol.py -f file.dmp windows.pstree|
|List services|volatility --profile=PROFILE svcscan -f file.dmp|python3 vol.py -f file.dmp windows.svcscan|
|List available registry hives|volatility --profile=Win7SP1x86_23418 -f file.dmp hivelist|python3 vol.py -f file.dmp windows.registry.hivelist|
|Print cmd commands|volatility --profile=PROFILE cmdline -f file.dmp|python3 vol.py -f file.dmp windows.cmdline|

- --profile is no longer present in Vol 3
- Generic plugin names are now replaced with OS-specific plugins
- pstree > windows.pstree, linux.pstree, mac.pstree