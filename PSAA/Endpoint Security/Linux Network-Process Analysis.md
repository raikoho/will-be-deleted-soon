`sudo netstat -t -n`
`sudo netstat -t -n -p` or `netstat -tnp`
![[Pasted image 20250128113605.png]]

`sudo ss -tnp`
![[Pasted image 20250128113735.png]]
![[Pasted image 20250128113902.png]]

`sudo ss dport == 4444 -tnp`
`sudo ss sport == 4444 -tnp`

sudo lsof
sudo lsof -u tcm
sudo lsof -i -n -P
sudo lsof -p 3610 //open all list of the files accociated with this id

![[Pasted image 20250128114546.png]]

--------

## Processes

`sudo ps -u tcm`

![[Pasted image 20250128115327.png]]

`sudo ps -AFH | less`

![[Pasted image 20250128115546.png]]

`sudo ps -p 3610 -F`
`sudo ps --ppid 2941`
`pstree`  // to find parents and child processes
`pstree -p -s 3610`

-------

`top` or `sudo top` //its like a task processor in windows
`sudo top -u tcm -c` //command was run to execute the process

![[Pasted image 20250128120036.png]]