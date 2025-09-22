![[Pasted image 20250127115912.png]]

```
tasklist
tasklist /V
tasklist /V  //display also dll and libraries
tasklist /m /fi "pid eq 3644"  //display dll and modules for certain
```
![[Pasted image 20250127120220.png]]
![[Pasted image 20250127120254.png]]
![[Pasted image 20250127120412.png]]

```
wmic process where processid=2088 get name, parentprocessid, processid
wmic process get name, parentprocessid, processid | find "192"
```

![[Pasted image 20250127120626.png]]
![[Pasted image 20250127120800.png]]