SOC-108925 
Ticket Number: SOC-108925 
Date/Time Reported: 2024-09-16 / 04:10:19 UTC 
Affected Endpoint: SW-LAN-SFO-02 
Assigned To: You 

On September 16, 2024, a system administrator reported that after attempting to download router troubleshooting documentation on an enterprise Windows server, they realized that the downloaded le might not have been from a legitimate vendor. The administrator promptly reported the suspicious download to the SOC. You are tasked with investigating the compromised endpoint in a live scenario to determine what actions took place and to identify any indicators or artifacts involved in the compromise. You have access to the affected endpoint, including event logs that were recorded and extracted during the incident. These can be located on the Desktop of the affected Windows host in the SOC-108925 directory. 

Note: As this is a live incident response scenario, any artifact leftover across the system is in scope for investigation. However, regarding event logs specically - you should only leverage the event log les that have been extracted and placed into the SOC-108925 directory during your analysis. Due to the nature of the environment, relying on the system's real-time logs will not show events captured during the incident.

## Investigation Questions 

Your investigative report should aim to answer the following questions: 

1. What was the file name of the malware that was downloaded onto the server? 


The filename of the malware that was downloaded onto the server is:

**`Cisco_Troubleshooting_Guide-v2.pdf.exe`**

This is evident from the Sysmon Event ID 11, which shows that a file was created at:  
📍 **`C:\Users\Administrator\Downloads\Cisco_Troubleshooting_Guide-v2.pdf.exe`**


- The `.exe` extension suggests it is an executable rather than a legitimate PDF.
- It has an **Alternate Data Stream (ADS)** `:Zone.Identifier`, meaning Windows tagged it with security info (likely from being downloaded from the internet).
- The download was initiated by **Microsoft Edge (`msedge.exe`)** under the **Administrator** account.

![[Скриншот 03-02-2025 10.43.12.png]]

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Id -eq 11 } | Select-Object TimeCreated, Message | Format-List
```

2. What is the SHA-256 hash value of the malware? 

i used:

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Id -eq 1 -or $_.Id -eq 15 } | Select-Object TimeCreated, Message | Format-List
```

![[Скриншот 03-02-2025 10.49.38.png]]

![[Скриншот 03-02-2025 10.49.54.png]]

704c1260c638b57175724260d81ece00e5fdfde29fba3232a43b255f1d08dcf1

1. What is the full URL where the malware was downloaded from? 

- **Referrer URL:**  
    `https://www.file.io/`
    
- **Host URL (where the malware was downloaded from):**  
    `https://file.io/xfamPHXmEnhP`

![[Скриншот 03-02-2025 11.22.25.png]]
```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Message -like "*Cisco_Troubleshooting_Guide-v2.pdf.exe*" } | Select-Object TimeCreated, Message | Format-List
```




1. What was the process ID of the malware’s first execution? 

i used :

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Id -eq 1 -and $_.Message -like "*Cisco_Troubleshooting_Guide-v2.pdf.exe*" } | Select-Object TimeCreated, Message | Format-List
```

and took the most erarlier.

![[Скриншот 03-02-2025 11.29.02.png]]
Answer: 5252


1. What was the parent process (name and process ID) of the malware? 

From the logs we can see that:
- **Parent Process ID**: `4544`
- **Parent Process Name**: `C:\Windows\Explorer.EXE`

2. What IP address and port did the malware use to connect back to the attacker? 

![[Скриншот 03-02-2025 11.34.09.png]]
we can see that it is:
IP: 3.134.39.220
port: 16979

1. What is the first command that the attacker ran once compromised? 

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Id -eq 1 -and ($_.Message -like "*cmd.exe*" -or $_.Message -like "*powershell.exe*") } | Select-Object TimeCreated, Message | Format-List
```

![[Скриншот 03-02-2025 11.52.40.png]]

the absolutely next one:
9/16/2024 4:02:01 AM 
whoami

2. What is the account name of the backdoor user that was created? 

![[Скриншот 03-02-2025 11.54.57.png]]
the same prior command.
Answer:
user : cisco_support

or this command:

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\security.evtx" | Where-Object { $_.Id -eq 4720 } | Format-List *
```

![[Скриншот 03-02-2025 12.06.32.png]]

3. When (date and time) was the backdoor user deleted? 

9/16/2024 4:06:06 AM
![[Скриншот 03-02-2025 11.55.53.png]]
still same command.

AND i also used this command to doble check (from security logs):

```
Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\security.evtx" | Where-Object { $_.Id -eq 4726 } | Format-Table TimeCreated, Id, Message -AutoSize
```

![[Скриншот 03-02-2025 12.09.01.png]]
1. What IP address and port does the implanted persistence mechanism connect to when it executes?

![[Скриншот 03-02-2025 12.14.03.png]]

Get-WinEvent -Path "C:\Users\analyst\Desktop\SOC-108925\sysmon.evtx" | Where-Object { $_.Id -eq 3 } | Format-Table TimeCreated, Id, Message -AutoSize

--
The backdoor persistence mechanism connected to the following IP address and port:

- **Source IP Address** (local machine): 172.31.41.137
- **Source Port**: 51077
- **Destination IP Address** (remote server): 3.134.39.220
- **Destination Port**: 16979