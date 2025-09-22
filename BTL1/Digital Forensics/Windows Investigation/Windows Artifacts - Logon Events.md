## Artifact Description

Identifying what user accounts have logged into a system, and at what time, can be useful for both digital forensic investigations and incident response. Doing so can help us attribute activity to a user account by showcasing they were the account signed in before these events occurred. For this artifact, we're looking specifically at:

- Event ID 4624 (Successful Logon)
- ID 4672 (Special Logon)
- ID 4625 (Failed Logon)
- and ID 4634 (Logoff)
## Artifact Location

Windows Event Logs are stored at the following location: `C:\Windows\System32\winevt\Logs`.

The logs we're interested in are stored in the `\Security` folder of this location.

## Artifact Analysis, Overview

To analyze this artifact we'll simply use Windows Event Viewer, the default utility for reading Event logs. Alternatively, if your organization is pulling these specific Event logs into a SIEM (which is very likely to detect local account bruteforce or abuse), this platform could instead be used to read them. Another tool we can utilize for analysis is Microsoft Excel, as Event Viewer allows us to export logs in CSV format.

**Artifact Analysis, 4624 Successful Logon**

First, we need to understand what information we're provided in these logs. Let's start with 4624, which shows successful logons to the system.

One of the most important properties for us to note is the Logon Type, where there are 8 possible values:

2 – **Interactive** (interactively logged on, meaning a physical logon to the device)  
3 – **Network** (accessed system via network)  
4 – **Batch** (started as an automated batch job)  
5 – **Service** (a Windows service started by service controller)  
6 – **Proxy** (proxy logon; not used in Windows NT or Windows 2000)  
7 – **Unlock** (unlock workstation - think Interactive logon, but unlocking to resume a previous session)  
8 – **NetworkCleartext** (network logon with cleartext credentials)  
9 – **NewCredentials** (used by RunAs when the /netonly option is used)

**Artifact Analysis, 4672 Successful Special Logon**

Special Logon events are when a user with administrative privileges logs into the system. For example, in the screenshot below I am logging into my own PC. As I am the only user account, I am in the Administrators local group, and therefore show up as a Special Logon, instead of a Successful Logon.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/files/9a5a5c942fef51a7f0dcfb6772b65a9d7151ea916a6b6772af4283a052bbdf4b3d636733a80bfb057d51b3cc0c1a.png)

First, let's look at the Subject information. This tells us the name of the account that is logging into the system. In this case, as the account is a Microsoft account (as opposed to a local account, or domain account) it will show the email address. The Security ID is the computer name, followed by the username. The Logon ID is a useful randomly-generated value that allows us to keep track of logon sessions. When looking at this logon, with the ID 0x25A036D, if we wanted to find the associated logoff with this session then we would look for the same ID in a Logoff log.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/files/b0eb4be92df09069954fe553c773b05efad122042981afb29a91598450fc389a72efe2bee8ab17667b97bd1b99dd.png)

And in the bottom half of the display we can see log-related information. Arguably the most important piece of information in here is the Logged timestamp, which tells us when this activity happened.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/files/89a5b0f8376a5b738a4101318e270f0011a6c8b14fc52ae6cb8672acf9cfcf7b714aa42395a4b29b2b2f7ee69c52.png)

**Artifact Analysis, 4625 Failed Logon**

Failed Logon events are very useful for us, especially when dealing with incident response. This is because these logs contain error codes, which help us to understand exactly why the logon attempt failed. The different error codes are:

|NETLOGON LOG ERROR CODE|DESCRIPTION|
|---|---|
|0xC0000064|The specified user does not exist|
|0xC000006A|The value provided as the current password is not correct|
|0xC000006C|Password policy not met|
|0xC000006D|The attempted logon is invalid due to a bad user name|
|0xC000006E|User account restriction has prevented successful login|
|0xC000006F|The user account has time restrictions and may not be logged onto at this time|
|0xC0000070|The user is restricted and may not log on from the source workstation|
|0xC0000071|The user account’s password has expired|
|0xC0000072|The user account is currently disabled|
|0xC000009A|Insufficient system resources|
|0xC0000193|The user’s account has expired|
|0xC0000224|User must change his password before he logs on the first time|
|0xC0000234|The user account has been automatically locked|

A high volume of attempted logins to a disable account (_0xc00000072_)? Suspicious.  
A high volume of attempted logins to an account that doesn't exist (bad username, _0xC0000006D_)? Suspicious. While most SOCs will use this log and the error codes within to generate alerts, there's definitely value for us as forensic investigators.

**Artifact Analysis, 4634 Logoff**

Logoffs are simple - they represent, well, a logoff from the current session. Above in the section for Special Logons we discussed Logon IDs to help us track sessions, and how we can marry up logons and logoffs using this value. In the below screenshot is a Logoff event with the same Logon ID from the Special Logon earlier. Interestingly, we can also see ‘Logon Type : 7’ below the second highlighted section, something we didn't see in the Special Logon earlier - revisiting what we learned about Logon Types in the section for ID 4624, we now learn that this session, between the Special Logon and Logoff, was an 'Unlock' where the account had previously logged in but the system was locked. The user then entered their credentials to resume the session, before logging off.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/files/3bd3ecdbedb0df72521483a38b2d3c331a5bc5223321acdb157e4f9d93d0dae8f3ba4bbec7eb88aa554c7e7939a1.png)

In the bottom section of the main panel, we can see the Logged timestamp value, which tells us when this event happened. Using a Logon or Special Logon with a Logoff event, we can tell exactly when an account was accessed, and when the session ended.

**Bringing it All Together**

Using the information from all of these events we can tell exactly when an account was accessed, and when the session ended. This can be used to help provide attribution to activity by evidencing that a user account or accounts were connected at that time.