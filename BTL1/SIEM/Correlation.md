This section of the SIEM domain will introduce you to SIEM correlation, and how the aggregated data is used to identify security events, incidents, and anomalies, generating alerts that can be investigated by human analysts. We will cover the normalization process, and how SIEM rules are written to aid security monitoring and detection.

---
# Normalization and Processing

Normalization merges events containing different data into a reduced format that contains common event attributes. Most logs capture the same basic information – time, network address, operation performed, etc. Categorization involves adding meaning to events – identifying log data related to system events, authentication, local/remote operations, etc.
## Log Enrichment

Log enrichment involves adding important information that can make the overall data more beneficial for security analysts when investigating alerts or unusual activity. One example could be logs that contain public IP addresses, but not their geographical location. Performing a simple lookup to see what geographical range the IP belongs to, can now immediately provide analysts with the country this IP is based in, which can aid investigations and help to build metrics.
## Log Indexing

SIEMs can hold an absolute ton of data, and to search through all of that, especially when looking over a long period of time such as a couple of weeks, can be extremely slow. By indexing attributes that are shared by a large number of logs, it can make searching for specific attributes across large data faster compared to having to scan every single piece of data in the SIEM storage to get the answers you need.
## Log Storage

For large organizations, the amount of storage needed to support a SIEM can be a large effort on the part of infrastructure and security teams. While alternatives to on-premises servers exist, such as Amazon Web Services S3 buckets or Hadoop, it is important for teams to consider all of their options, weighing in factors such as cost, ease-of-use, and scalability.
## Normalization

Different software, hardware, and devices produce their own format of logs, as there is no universal format (we wish!). This makes it difficult when sending tons of different logs to a SIEM, because the platform needs to be able to understand and sort all of the attributes to allow for analysts to perform searches through all of the data stored within the SIEM.

SIEM log normalization is the process of changing log formats into a format that is as similar as possible across all devices and log sources, giving the SIEM a break and allowing for more consistent searching and information breakdown. Obviously, logs from a Windows endpoint won’t look the same as logs from a Linux system, but if we can match up things the best we can, the SIEM can handle the rest.

A great example by Travis Marlette in the Splunk Best Practice book is the following: “In our example, let’s say source_ip represents both the src_ip field from Cisco network devices and the source_address from Juniper network devices.” This means we can now search in our SIEM for source_ip value, and it’ll check both Cisco and Juniper logs!

---

# SIEM Rules

They are search queries that are looking for specific activity, looking at any imported or real-time data that is being fed into the SIEM solution. If the rule query matches a piece of data, different actions can be triggered, such as generating an alert, sending an email to a team, or recording the activity to a separate location. 
These search queries can be running continuously (real-time detection), or set to run at specific scheduled times, such as every day, or every week.
## Examples of SIEM Rule Functionality

We can create rules to detect an endless amount of activity, providing the SIEM is pulling in the required logs. Below are just some of the things we can monitor for:

**Authentication/Account Activity:**

- Failed logon attempts
- Successful (or failed) login attempts to disabled accounts
- Use of specific accounts (local administrator, administrator, domain administrator)
- SID (Security Identifier) changes to an account (a potential indicator of privilege escalation)

**Process Execution:**

- Execution from unusual locations (such as temporary directories or browser caches – may indicate malware execution or persistence mechanisms)
- Suspicious process relationships (such as Microsoft Word spawning a child process of CMD or PowerShell window (potentially a malicious macro that is executing code))
- Known bad hashes (MD5, SHA1, SHA256 hashes that are generated from confirmed malicious files)

**Network Activity:**

- Port scans
- Service enumeration
- Host discovery
## False Positive Reduction and Tuning

False positives are alerts that have been generated but do not actually represent a malicious event. An example of this would be a rule that is monitoring [Windows Event ID 4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625) – ‘**An account failed to log on**’. Monitoring this log will tell us when an account fails to login successfully. Everyone has entered their password in wrong once or twice, so creating a rule that looks for single occurrences of login failures isn’t going to provide much value, and will be very noisy (meaning it will generate a LOT of alerts). Thresholds can be set to allow for more control over what happens when searches bring back results from the aggregated data. We can set a rule threshold, so if an account fails to log in 10 times within 10 minutes, then generate an alert. This can help us to identify attacks where a malicious actor is trying to log into an account by guessing the password (brute-force or dictionary attacks).

In some cases the rule may need to be altered to specify that some values should be ignored. Let’s go through an example; we have a rule that looks at firewall logs to identify network scanning activity where one source IP is sending traffic to a high number of internal systems. Our company then purchases a vulnerability scanner and sets it up in an internal network, planning to perform host discovery scans to actively identify running systems so this information can be stored and used to plan vulnerability scans in the future. While the scanner is sending traffic to every potential IP in it’s defined target range this rule is going to alert on activity that isn’t malicious – if the security team deems it appropriate they can choose to exclude this source IP from the rule. So now when the scanner activates the activity will be observed by the SIEM but the rule is telling it not to alert when this specific source IP is seen – we have now prevented future false positives from generating.

## Writing Search Queries and Alerts

We’re going to cover this in the next section, where you’ll set up your own local version of Splunk SIEM, and learn how to write search queries to find specific information within a dataset that contains hundreds of thousands of logs. Once you know how to write search queries, you can apply this to set up alerts!

Before you jump into that section we recommend reading this page on creating detection rules in the ELK stack, an open-source SIEM alternative. While we’re going to be using Splunk, this will definitely give you a great insight into the logic behind rules! – [https://www.elastic.co/guide/en/security/current/rules-ui-create.html](https://www.elastic.co/guide/en/security/current/rules-ui-create.html)

---
