SOC-108912 
Ticket Number: 
SOC-108912 
Date/Time Reported: 2024-09-15 / 19:30:00 UTC 
Affected Endpoint: DESKTOP-I51F5PU 
Affected User: Jordan Anders 
Assigned To: You 

The SOC received a Snort IDS alert indicating a known malicious le transfer from the internet onto the workstation `DESKTOP-I51F5PU`, which belongs to Jordan Anders. The alert agged this transfer as potentially harmful and associated with known malware signatures. Following this initial alert, several additional alerts were triggered, indicating potential malware activity and signs of data exltration on `DESKTOP-I51F5PU`. The IDS system automatically captured network trac around the time of the initial alert. You are tasked with investigating this packet capture (.pcap) le to determine what actions were taken and to identify any network indicators or artifacts involved in the compromise. The packet capture le, named `SOC-108912.pcap`, has been transferred to your Ubuntu investigator workstation and is located on the Desktop in the `SOC-108912` directory. 

## Investigation Questions 

Your investigative report should aim to answer the following questions: 

1. **Packet Capture Metadata** 
   a. How many packets are in the capture file? 
   b. What is the timestamp of the first and last packet? 
   c. What is the elapsed time between the first and last packet? 
   d. What is the IP address of `DESKTOP-I51F5PU`?
2. **Initial Infection**
   a. In UTC, what time did the initial infection occur?
   b. From where (IP address and domain) did the initial infection originate? 
   c. What was the name of the file involved in the initial infection? 
   d. What is the SHA-256 hash of the le involved in the initial infection? 
   e. When the malware executes, what destination port number does the victim use to connect back to the attacker? 
3. **Second Stage Compromise**
   a. After the initial infection, what was the name of the additional malware file transferred to the host? 
   b. From where (IP address and domain) did this malware originate? 
   c. Which software utility was used to retrieve the malware? 
   d. What is the SHA-256 hash of the malware? 
   e. What is the MITRE Software ID of the malware? 
4. **Command and Control** 
   a. Where (IP address and domain) is the host beaconing to? 
   b. How frequently is the host beaconing? 
   c. What is the beacon_id? 
   d. What is the likely MITRE Software ID of the malware agent initiating the beacon? 
5. **Exltration** 
   a. What protocol was used for data exltration?
   b. What IP address received the exltrated data from the attacker? 
   c. What credentials were used to authenticate before data exltration? 
   d. What file was exltrated? 
   e. What is the value of the NTLM hash that was stolen?
----
1.
a) 3340

![[Скриншот 02-02-2025 13.51.02.png]]
b) 
**First packet timestamp**: 14:13:59.932551
**Last packet timestamp**: 14:19:43.764728

![[Скриншот 02-02-2025 13.54.34.png]]

c) approximately 5.73 minutes

![[Pasted image 20250202140024.png]]
d) 
i used first

`tcpdump -tt -r SOC-108912.pcap -n tcp | cut -d " " -f 3 | cut -d "." -f 1-4 | sort | uniq -c | sort -nr`

![[Скриншот 02-02-2025 14.05.29.png]]

![[Скриншот 02-02-2025 14.33.06.png]]


![[Скриншот 02-02-2025 15.23.16 1.png]]

10.0.2.15

--------------

## 2

a) What time it occur?
![[Скриншот 02-02-2025 15.23.16.png]]





![[Скриншот 02-02-2025 14.47.46.png]]
![[Скриншот 02-02-2025 14.50.10.png]]
Uf we follow http stream we found .exe:

![[Скриншот 02-02-2025 14.53.13.png]]

![[Скриншот 02-02-2025 14.58.19.png]]
![[Pasted image 20250202145942.png]]
![[Pasted image 20250202150450.png]]
![[Pasted image 20250202150711.png]]
![[Pasted image 20250202150807.png]]
 a. In UTC, what time did the initial infection occur?
 
 2024-09-15 19:15:26.724078
![[Скриншот 02-02-2025 16.19.39.png]]
 http.request.uri contains ".exe"
 
b. From where (IP address and domain) did the initial infection originate? 
![[Скриншот 02-02-2025 15.23.16 2.png]]
46.242.130.165

c. What was the name of the file involved in the initial infection? 

ab.exe

d. What is the SHA-256 hash of the le involved in the initial infection? 
![[Скриншот 02-02-2025 16.05.17.png]]
8f1b96104e641d359f6720a8e845f64226cd09bb04ad80feec17713128218fec

e. When the malware executes, what destination port number does the victim use to connect back to the attacker? 

![[Скриншот 02-02-2025 16.24.48.png]]
![[Скриншот 02-02-2025 16.29.08.png]]
port 6668 тому що самі він відкрився лише після запуску ab.exe /

---

**Second Stage Compromise**
   a. After the initial infection, what was the name of the additional malware file transferred to the host? 

EdgeUpdateInstaller.exe

   b. From where (IP address and domain) did this malware originate? 

81.177.32.15

   c. Which software utility was used to retrieve the malware? 

See User Agent:
![[Скриншот 02-02-2025 16.37.25.png]]

_Windows PowerShell_. _Microsoft_

   d. What is the SHA-256 hash of the malware? 

92804faaab2175dc501d73e814663058c78c0a042675a8937266357bcfb96c50


   e. What is the MITRE Software ID of the malware? 

Знайшов на вірус тотал при пошуку по хеш:
![[Скриншот 02-02-2025 16.43.40.png]]
![[Скриншот 02-02-2025 16.46.25.png]]
![[Скриншот 02-02-2025 16.47.15.png]]

бо це асоціюється з мімікатц.

----

**Command and Control** 
   a. Where (IP address and domain) is the host beaconing to? 

185.114.247.170

   b. How frequently is the host beaconing?  

We can see that it is every 30 seconds:
![[Скриншот 02-02-2025 16.51.28.png]]

   c. What is the beacon_id? 

i opened 1 packet with backon (post):

![[Скриншот 02-02-2025 16.55.20.png]]

![[Скриншот 02-02-2025 16.55.35.png]]
  
  id= 23d4e1f9

d. What is the likely MITRE Software ID of the malware agent initiating the beacon? 

The user agent `DarkTortilla/1.0` along with the beacon data suggests a malware tool that performs C2 (Command and Control) communication using HTTP-based beaconing.

![[Скриншот 02-02-2025 16.59.55.png]]
S1066

-------

**Exltration** 
   a. What protocol was used for data exltration?

Я поглянув на smtp, smb2 - нічого не було знайдено. Наступним був саме 'ftp':

![[Скриншот 02-02-2025 17.08.30.png]]
Я зробив остаточний висновок, оскільки комунікація відбулася лише за кілька хвилин ПІСЛЯ зараження. До цього вона була відсутня.

   b. What IP address received the exltrated data from the attacker? 

З попереднього скріншоту видно, що присутня лише одна айпі адреса.
Я на всякий випадок перевірив це на вірустотал.
![[Скриншот 02-02-2025 17.07.28.png]]
   

   c. What credentials were used to authenticate before data exltration? 

Ми можемо це переглянути відразу :

![[Скриншот 02-02-2025 17.11.31.png]]
   
USER impossibreak
PASS potential4danger!

d. What file was exltrated? 

exfil_loot.b64.txt

![[Скриншот 02-02-2025 17.14.04.png]]

e. What is the value of the NTLM hash that was stolen?

cat exfil_loot.b64.txt:

ICAuIyMjIyMuICAgbWltaWthdHogMi4yLjAgKHg2NCkgIzE4MzYyIEZlYiAyOSAyMDIwIDExOjEzOjM2CiAuIyMgXiAjIy4gICJBIExhIFZpZSwgQSBMJ0Ftb3VyIiAtIChvZS5lbykKICMjIC8gXCAjIyAgLyoqKiBCZW5qYW1pbiBERUxQWSBgZ2VudGlsa2l3aWAgKCBiZW5qYW1pbkBnZW50aWxraXdpLmNvbSApCiAjIyBcIC8gIyMgICAgICAgPiBodHRwOi8vYmxvZy5nZW50aWxraXdpLmNvbS9taW1pa2F0egogJyMjIHYgIyMnICAgICAgIFZpbmNlbnQgTEUgVE9VWCAgICAgICAgICAgICAoIHZpbmNlbnQubGV0b3V4QGdtYWlsLmNvbSApCiAgJyMjIyMjJyAgICAgICAgPiBodHRwOi8vcGluZ2Nhc3RsZS5jb20gLyBodHRwOi8vbXlzbWFydGxvZ29uLmNvbSAgICoqKi8KCm1pbWlrYXR6ICMgcHJpdmlsZWdlOjpkZWJ1ZwpQcml2aWxlZ2UgJzIwJyBPSwoKbWltaWthdHogIyBzZWt1cmxzYTo6bG9nb25wYXNzd29yZHMKCkF1dGhlbnRpY2F0aW9uIElkIDogMCA7IDQyMjQxOSAoMDAwMDAwMDA6MDAwNjcyMTMpClNlc3Npb24gICAgICAgICAgIDogSW50ZXJhY3RpdmUgZnJvbSAxClVzZXIgTmFtZSAgICAgICAgIDogam9yZGFuLmFuZGVycwpEb21haW4gICAgICAgICAgICA6IENSRVNUV0FZCkxvZ29uIFNlcnZlciAgICAgIDogQ1JFU1RXQVktREMxCkxvZ29uIFRpbWUgICAgICAgIDogOS8xNS8yMDI0IDc6NTk6MDkgQU0KU0lEICAgICAgICAgICAgICAgOiBTLTEtNS0yMS0xNTIxMTQ0MjU3LTM5NjI4OTk3MTUtODIzMjYzMTE0LTEwMDEKICAgICAgICBtc3YgOgogICAgICAgICBbMDAwMDAwMDNdIFByaW1hcnkKICAgICAgICAgKiBVc2VybmFtZSA6IGpvcmRhbi5hbmRlcnMKICAgICAgICAgKiBEb21haW4gICA6IENSRVNUV0FZCiAgICAgICAgICogTlRMTSAgICAgOiAxMzlmODFkOTFjMmY1ZTU5YjZiODkxZGQ1NzdiZDgwNgogICAgICAgICAqIFNIQTEgICAgIDogMDRjNmUyM2IxZTE3Y2M0NGQ4MGI4YzlhZWI5NjI0NjRlZWE2NGVhNwogICAgICAgICAqIERQQVBJICAgIDogMDRjNmUyM2IxZTE3Y2M0NGQ4MGI4YzlhZWI5NjI0NjQKICAgICAgICB0c3BrZyA6CiAgICAgICAgd2RpZ2VzdCA6CiAgICAgICAgICogVXNlcm5hbWUgOiBqb3JkYW4uYW5kZXJzCiAgICAgICAgICogRG9tYWluICAgOiBDUkVTVFdBWQogICAgICAgICAqIFBhc3N3b3JkIDogKG51bGwpCiAgICAgICAga2VyYmVyb3MgOgogICAgICAgICAqIFVzZXJuYW1lIDogam9yZGFuLmFuZGVycwogICAgICAgICAqIERvbWFpbiAgIDogQ1JFU1RXQVkKICAgICAgICAgKiBQYXNzd29yZCA6IChudWxsKQogICAgICAgIHNzcCA6ICAgS08KICAgICAgICBjcmVkbWFuIDoKCm1pbWlrYXR6ICM=

![[Скриншот 02-02-2025 17.18.15.png]]

Answer:

139f81d91c2f5e59b6b891dd577bd806