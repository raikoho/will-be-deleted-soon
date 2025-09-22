SOC-109102 
Ticket Number: SOC-109102 
Date/Time Reported: 2024-09-16 /15:45:18 UTC 
Affected Endpoint: WEB-CORP-01 
Assigned To: You 

Through its endpoint detection solution, the SOC was alerted that the web server hosting the organization’s corporate website (crestwaybank.com) had been compromised on September 16, 2024. However, the initial access vector used by the attacker remains unclear. As a SOC analyst, you are tasked with investigating the events that were ingested from around the time of the suspected compromise to identify how the attacker gained initial access. To investigate the logs, you can access the SOC’s Splunk instance from the Ubuntu investigator workstation at http://10.10.0.10:8000. You can use the index of crestway-web. 

REMINDER: You will not be able to access http://10.10.0.10:8000 from your host machine; this is expected. Instead, you can access it through Firefox in the exam-provided Ubuntu machine. 



Investigation Questions 

![[Скриншот 02-02-2025 18.03.29.png]]
![[Скриншот 02-02-2025 18.03.50.png]]
It is only one IP and it is consists at any useragents and urls

### Your investigative report should aim to answer the following questions: 
1. At what timestamp did the attacker first access the website? 

![[Скриншот 02-02-2025 18.13.52.png]]

9/16/24 2:50:51.000 PM


2. What vulnerability scanning tool and version was used against the web server? 

![[Скриншот 02-02-2025 18.00.25.png]]
wpscan

3. What tool did the attacker use to enumerate files and directories on the server? 

index="crestway-web" 23.254.226.90 // +filter by useragent

![[Скриншот 02-02-2025 18.10.01.png]]
gobuster

4. What is the most likely way the attacker gained credentials to the website’s admin panel? 

![[Скриншот 02-02-2025 20.55.58.png]]

---

index="crestway-web" 
| eval payload_length = length(uri_query) 
| where payload_length > 100 
| table _time, clientip, useragent, uri, uri_query, status, bytes

![[Скриншот 02-02-2025 20.32.03.png]]


No many Failed Login Attempts - This suggests the attacker may have **already had valid credentials** and wasn’t brute-forcing.

I found some steps SQL Injection. And imeditely after this, wa accessed /wp-admin/ - so its possible SQL Injection.



------

But it was also found LFI attack. But it was much later.

![[Скриншот 02-02-2025 20.35.17.png]]


5. At what timestamp did the attacker successfully authenticate and access the admin panel? 

index="crestway-web" crestwaybank.com uri_path="/wp-login.php"  uri="/wp-login.php" 
| sort _time

**3:29:40 PM (16/Sep/2024)** – This is the timestamp where the attacker received a 302 status code, which likely indicates successful authentication or redirection to the admin area after logging in.

![[Скриншот 02-02-2025 19.52.10.png]]

6. What is the name of the plugin that was uploaded by the attacker? 

index="crestway-web" crestwaybank.com uri="/wp-admin/plugin*" | dedup uri

![[Скриншот 02-02-2025 19.59.39.png]]
2024-09-16 15:30:00: `wp-admin/plugins.php?action=activate&plugin=wp_webshell%2Fwp_webshell.php`

Answer:
wp_webshell/wp_webshell.php

7. What vulnerability did the attacker introduce by adding this plugin? 

RCE.
The plugin `wp_webshell/wp_webshell.php` is a known malicious WordPress plugin often used for web shell attacks.

RCE: The `wp_webshell` plugin typically allows an attacker to execute arbitrary code on the WordPress server. This could give the attacker full control over the server, allowing them to upload malicious files, run commands, and interact with the file system, essentially taking over the website.

Data Exfiltration: If the attacker has full access, they can exfiltrate sensitive data such as user credentials, financial data, and other confidential information stored on the site.

8. What IP address and port did the web server use to establish a connection back to the attacker?

i searched for 

`index="crestway-web" "wp_webshell.php"`
![[Скриншот 02-02-2025 20.11.31.png]]

the attacker is using the `nc` (Netcat) command to initiate a reverse shell to the IP `46.166.190.182` on port `3443` :

![[Скриншот 02-02-2025 20.11.58.png]]


--------
