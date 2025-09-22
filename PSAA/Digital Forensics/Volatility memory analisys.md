- [https://volatilityfoundation.org/the-volatility-framework/](https://volatilityfoundation.org/the-volatility-framework)
- [https://github.com/volatilityfoundation/volatility3](https://github.com/volatilityfoundation/volatility3)

## Info

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.info > ~/Desktop/win10-info.txt`

## Network

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.netstat` //info about network
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.netscan` //detailed about network

## Process

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pslist | less`
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pslist | grep services`
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pslist | grep 3728` //grep process id
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.psscan`

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pstree`
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pstree --pid 5792`
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.pstree | grep svchost.exe`

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.cmdline`

## Registry

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.registry.userassist | less` // will show programs, how many times was executed and time

`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.registry.hivelist`
`python3 vol.py -f ~/Desktop/memdump/win10.vmem windows.registry.hivelist --filter "Bill Duhtry"`

`python3 vol.py -f ~/Desktop/memdump/win10.vmem -o ~/Desktop/ windows.registry.printkey --key "Software\Microsoft\Windows\CurrentVersion\Run"` //

