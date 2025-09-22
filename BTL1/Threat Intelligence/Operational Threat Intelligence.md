## Precursors Explained

“Precursors” or “Threat Precursors” are elements of the incident identification and response process that allow both an attacker and a security researcher or professional to determine the existence of flaws and/or vulnerabilities within a system. 
By identifying precursors organizations can work to prevent cyber attacks before they occur.
#### Types of Precursors

Attacks can take many different forms, and attackers can find many ways to compromise a system. With this in mind it is undeniable to admit that precursors can appear in many different ways and above all, both attackers and security professionals can use many tools to obtain them. Some examples will be shown below.

**Port Scanning, Operating System and Application Fingerprinting**

One of the most effective ways to obtain information about a network is through scanning. Using tools such as Nmap, Netcat, or Nessus, both a researcher and an attacker can learn about the services and vulnerabilities that exist on a system. A lot of information can be gained from performing host discovery, port scanning, and vulnerability scanning activities, such as which ports or services are running and responding on a system, what operating system is installed on the system, and what applications and versions of applications are present.

When considering the precursors that this activity would generate, we would mainly be looking to monitor network connections and event logs from internet-facing systems.

- Logs from firewalls or web application firewalls (WAFs) that have rules written to alert and log when one source IP is attempting to connect on X number of ports over a short period of time.
- Logs from systems that are being scanned.

**Social Engineering and Reconnaissance**

Another way to obtain the greatest amount of information about an organization is, without a doubt, social engineering. This is because, with social skills and deception, both an attacker and a researcher can learn about any type of information and vulnerabilities of an organization. Techniques such as “dumpster diving” (searching for items in the rubbish such as USB sticks, printed documents, notebooks, etc) or “eavesdropping” (Listening to conversations between employees) are very useful for identifying pieces of information that can be brought together to potentially discover vulnerabilities that can be exploited by an attacker.

When considering the precursors that this activity would generate, we would mainly be looking to listen to employee reports of unusual or suspicious activity or CCTV footage from both inside and outside the office.

- Non-employees looking through the organization’s bins that are conducting ‘dumpster diving’.
- Non-employees hanging around outside the office or lobby areas.
- Employees being engaged with outside or near the office by unknown individuals.
- Calls from unknown, withheld or spoofed phone numbers.
- Documents or office equipment going missing.

**OSINT Sources and Bulletin Boards**

And finally, we have the review of social media, blogs, forums, and bulletin boards, security articles and reports, and other OSINT data both on the clear web and dark web.

When considering the precursors that this activity would generate, we would mainly be looking to monitor OSINT sources using free tools such as TweetDeck and paid intelligence resources such as Recorded Future.

- An email or online message from a threat group threatening or stating they will attack the organization.
- Publicly disclosed vulnerabilities (CVEs) that affect systems or programs that are used by the organization.
- Chatter on underground forums about a zero-day or new malware that is being exploited or utilized in the wild.
- Reports stating an increase in vulnerability exploitation activity supplied by government organizations or intelligence vendors.

---
## Indicators of Compromise Explained

#### Example of IOCs

Below is a list of typical indicators of compromise that are shared publicly and between organizations.

- **Email Addresses –** These are mailboxes that have been acting maliciously, such as sending emails containing malicious URLs, malicious attachments, or attempting to socially engineer email recipients into taking actions they wouldn’t usually take such as giving out information.
- **IP Addresses –** These IPs have acted maliciously, such as performing unauthorized port or vulnerability scans, hosting malicious content or websites, or have been linked to malicious actor infrastructure such as command-and-control (C2) servers. WHOIS lookups can also be conducted to gain more information, such as who owns the IP, where it’s geographically based, hostname, and occasionally contact details.
- **Domain Names/URLs –** Sites that have been acting maliciously, such as hosting malware, phishing sites, or other malicious content.
- **File Hashes/File Names –** We can easily share intelligence about malware or other malicious files, often by referring to them by their unique hash values (typically MD5, sha256, or sha1). These can be used by security teams to blacklist the specific file hashes so that they are detected and deleted by security solutions such as endpoint detection and response (EDR).
#### IOC Formats

STIX and TAXII are common methods of sharing threat intelligence, such as indicators of compromise. These values alone don’t mean a lot, but with STIX we can share information in a structured format, providing a lot more than just lists of IOCs.

**STIX:**

Structured Threat Information eXpression, or STIX, was developed by MITRE and the OASIS Cyber Threat Intelligence Technical Committee as a standardized language for sharing threat information. For some organizations and information-sharing committees, this has been the standard and is widely used. Whilst STIX is designed to be used in conjunction with TAXII, it can be shared without it. STIX is designed to share not just IOCs, but also threat:

- Motivations
- Abilities
- Capabilities
- Response

**TAXII:**

Trusted Automated eXchange of Intelligence Information, or TAXII, defines how cyber threat information can be shared by using services and message exchanges. Designed to handle STIX information, this platform is run on a server and allows the sharing of information between specified groups or provides a public “threat stream” that individuals can sign up to and receive intelligence.

-----
## MITRE ATT&CK Framework

MITRE’s Adversarial Tactics, Techniques, and Common Knowledge (ATT&CK) is a knowledge base and model for cyber adversary behavior, reflecting the various phases of an adversary’s attack lifecycle and the platforms they are known to target.  
Since it was introduced in 2013, it has become one of the most respected and referenced resources for cyber security professionals.
#### ATT&CK For Threat Intel

ATT&CK gives analysts a common language to structure, compare, and analyze threat intelligence.

- [Getting Started with ATT&CK: Threat Intelligence Blog Post](https://medium.com/mitre-attack/getting-started-with-attack-cti-4eb205be4b2f): This blog post describes how you can get started using ATT&CK for threat intelligence at three different levels of sophistication
- [ATT&CKing Your Adversaries Presentation](https://www.slideshare.net/JamieWilliams130/attcking-your-adversaries-operationalizing-cyber-intelligence-in-your-own-environment-for-better-sleep-and-a-safer-tomorrow): This presentation covers how to use ATT&CK to take cyber threat intelligence and operationalize it into behaviors that can drive relevant detections.
- [Blog posts on threat intelligence](https://medium.com/mitre-attack/using-att-ck-to-advance-cyber-threat-intelligence-part-2-6f21fdba80c): These blog posts explain the fundamentals of how to use ATT&CK for threat intelligence.
- [ATT&CKing the Status Quo Presentation](https://www.youtube.com/watch?v=p7Hyd7d9k-c): This middle part of this presentation provides an introduction to using ATT&CK for threat intelligence. [Slides are also available](https://www.slideshare.net/KatieNickels/bsideslv-2018-katie-nickels-and-john-wunder-attcking-the-status-quo).
- [ATT&CKing with Threat Intelligence Presentation](https://www.pscp.tv/w/1yoKMVDjbrkGQ): This presentation provides a perspective on how to use threat intelligence for ATT&CK-based adversary emulation. [Slides are also available](https://www.slideshare.net/ChristopherKorban/attcking-with-threat-intelligence).
- [ATT&CK Navigator Use Case for Threat Intelligence](https://youtu.be/pcclNdwG8Vs): This demo provides an overview of the ATT&CK Navigator as well as a threat intelligence use case for how to compare group behaviors. A corresponding written tutorial on comparing Navigator layers is [available here](https://attack.mitre.org/docs/Comparing_Layers_in_Navigator.pdf).

---
## Lockheed Martin Cyber Kill Chain

The Cyber Kill Chain (CKC) framework was developed by Lockheed Martin in 2011 and it is an Intelligence Defense model for the identification and prevention of cyber-attacks, specifically ones that can be classified as Advanced Persistent Threats (APTs).
In recent years, it has become the de facto standard to describe how attacks can happen on a network.
### Kill Chain Stages

#### [1] Reconnaissance:

**Attackers:** Malicious actors will research the target organization typically using both active and passive reconnaissance methods such as domain record lookups, public IP range ports, vulnerability scanning, scouting out employees on social media, and more.

**Defenders:** Activity conducted by the security team or defenders at this stage will come in the format of precursors, such as IPs that are performing port or vulnerability scanning, employees being approached by individuals that they do not know, and employees potentially receiving connection/friend requests on social media.
#### [2] Weaponization:

**Attackers:** Malicious actors create their backdoor instead of purchasing commodity malware, and host this file on a domain they own. They then write a macro within a Microsoft Word document that connects to the attacker-owned domain and downloads the malware to the system where the file was opened.

**Defenders:** It is extremely hard for the security team to detect this stage, as it is not happening within their environment therefore they have no visibility of what happens outside the organization (except for cyber threat intelligence). Typical defenses should be employed such as anti-virus, email security, and system hardening.
#### [3] Delivery:

**Attackers:** Malicious actors have crafted a spear-phishing email using information gathered on the target from OSINT sources. The email contains a Microsoft Office document with a malicious macro that will run malware in the context of the currently signed-in user.

**Defenders:** The security team should have email defenses in place such as attachment sandboxing which should be able to detect any malicious attachments such as immediately malicious binaries or malicious Word documents or PDFs.
#### [4] Exploitation:

**Attackers:** Malicious actors have identified a vulnerability, that if exploited, can provide them with higher privileges than the current compromised account has, providing them with more access and the ability to perform more actions.

**Defenders:** The security team can prepare for this stage by hardening systems and performing vulnerability management processes to identify and remediate vulnerabilities that are both internal and externally present.
#### [5] Installation:

**Attacker:** Malicious actor installs a backdoor and deploy persistence tactics and techniques to ensure that they can keep a foothold within the infected system, allowing continuous access.

**Defenders:** The security team can deploy endpoint detection and response (EDR) software agents to potentially infected hosts to allow for the detection, investigation, and eradication of a malicious presence.
#### [6] Command and Control:

**Attackers:** The malicious actor installs malware that opens a channel between the malicious actor and remote machine, allowing them to send commands to the malware and attempt to gain the ability to complete step 7, actions on objectives.

**Defenders:** The defender's last step to fully stop the threat, prevention of command execution is key
#### [7] Actions on Objectives:

**Attackers:** The malicious actor was successful in their attack and has obtained keyboard access, they are now able to attempt to complete any objectives they have.

**Defenders:** The defender must detect this stage as quickly as possible to prevent further damage and minimize the time that the attacker can complete their objectives.

----
## Attribution and its Limitations

Attribution is the determination of a cause or origin of action. In the realms of cybersecurity, we are primarily concerned about this when malicious actors are in play, and determining who, what or where a cyber breach or intrusion has occurred. Attribution is not solely focused on laying blame but on gathering information, a new user may inadvertently cause a system failure, this would be attributed to inexperience rather than a malicious act.
#### Machine Attribution

Attributing malicious cyber activity to a machine or multiple machines would mean identifying the machine(s) used in an attack. This would usually require examining things like the IP address, log files that document what is happening in the network, who has logged in to the machine. So, we could find out that Azleon’s machine was used in an attack but find a trail leading to Jupiter’s machine which was the originating point of attack. There could be multiple machines in a trail. The IP address may be in another country or require further investigation. Should the IP lead back to Azleon then law enforcement could seize that machine for investigation.
#### Human Attribution

Attributing the malicious activity to a human is finding the identity of the person(s) responsible for the activity, those pushing the keys as it were. Technical forensics which looks at data left behind may not be able to help much further, credentials may point to one person but that may not have been the person physically executing the attack. Credentials get stolen or machines compromised. Technical means may not be enough to identify the person involved as data collected would need to be compared to a database to match an identity, therefore it is only as good as the database. If you can identify the person responsible it is vital to know why it was carried out and if other parties were involved.
#### Ultimately Responsible Attribution

Attributing this malicious activity to the ultimately responsible party answers the question of who is to blame? Was the actor working alone and fully responsible or working on behalf of an organization or nation-state? The “why” is often a more important factor here as people can be coerced into committing these acts, or may be in a position that they feel they can’t refuse. Law enforcement could decide to prosecute an individual or a nation could decide to engage in diplomatic discussion with the offending nation, they might then attribute this to an organization and prosecute or even retaliate.

As you can see the process of assigning attribution can be difficult and complicated, even more so when it is easy to use proxies in other countries. Then requiring deeper and longer investigations will need more cooperation with other agencies.
### Key Indicators to attribution

- **Tradecraft** – Frequently used behaviors such as an attacker’s techniques, tools, and procedures used to conduct cyber-attacks.
- **Infrastructure** – The physical machines or networks used in the attack; are often compromised by other means before an attack.
- **Malware** – Malware can be specific to a threat actor; it can be reused or it can be modified quickly if a compromise is suspected to avoid attribution.
- **Intent** – The intent behind the attack, the motivation, or reasoning.
- **External sources** – External reports from organizations like cyber security companies, media even students.
### Cyber Attribution Techniques

Investigators use many different tools and programs to reveal information about attacks. As an example, let's consider a US-based company that was attacked with malware. This was written in a non-native language, the Cyrillic alphabet. This information can be used by security professionals to help identify the actors behind it. If the malware itself is written with references to Cyrillic, Russian actors could be involved.

Some threat actors, based on their intentions and motived, may WANT to be recognised for their attacks, Example of this could include intentionally fingerprinting malicious files, setting specific filenames during attacks, initiating connections from IP addresses or domains previously linked to the actor, and using custom malware not utilized by any other groups.
### Issues with Attribution

A major difficulty in analyzing data from attacks is to determine what can be reliable. Metadata such as source IP addresses, email data, domain names, user names, and registration data can all be helpful. Still, it may be faked, through proxies and by using other compromised targets to carry out the attack. The TOR browser can enhance anonymity for malicious actors and automatically encrypts traffic.

Threat actors may choose to share infrastructure to make attribution to a single group harder or use commodity malware or living-off-the-land techniques to prevent identification via the use of unique tools or techniques. Copy-cat attacks can occur where one malicious actor will use the same tools and techniques as another actor in an attempt to trick researchers and threat intelligence analysts into believing the attack was conducted by the other group.

Remember our example of the US company getting hit with malware that include Russian phrases? This could have been engineering by threat actors in another country to try and mislead analysts and researchers!

-----
## Pyramid of Pain

The pyramid of pain is a visual representation of the amount of pain we can cause a malicious actor in denying them certain indicators, working to disrupt their operations.
 
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b06ac1e027004ce9c1fc1c6fc0dc4230b307d5c47bb8ff0ac4886462037307dc0c03910ad3dcc71c11efd6af039a.png)
### Layers Explained

**Hash Values**

Trivial amounts of pain relate to **hash values.** They can provide the highest confidence indicators yet are vulnerable to modification by the attack or accidentally by the end-user. By the degree that these can change and how often, these would be the least useful indicators and provide a minimal amount of frustration to an attacker.

**IP Address**

Stepping up the pyramid, next is **IP addresses**. Though having a unique address is beneficial, it is not uncommon to change these with VPNs, TOR browsing, or open proxies to reassemble your attack from a different address.

**Domain Names**

Rising higher we sit on **domain names**, which can be changed, but require registration and hosting. Many DNS providers do not all have the same standards across the board in terms of legality and restrictions, which can make it fairly easy for an attacker to change domains. Though not as easy as IP addresses, these can be modified with a longer wait time.

**Network/Host Artifacts**

**Network and host artifacts** start to provide more difficulty to the attacker once you begin implementing defenses against these tools and methods they are using. This could be determined by finding where directories are commonly created, specific registry values, files, etc. As an example, the Locky spam waves showcased:

- different domain names
- different IP addresses
- different hashes

But, through a three-month campaign, the host artifacts performed the same. Changing the logic in the malware is much harder than changing IP addresses. By signaling out these indicators and stopping them, it creates greater frustration and hurdle for the attacker.

**Tools**

**Tools** are hard to change. Carpenters can use a reliable saw for years. The same goes for adversaries attacking your network. Identifying one or more of the tools they are using to distribute attacks and halting their use puts a severe bend in their hose. This requires re-tooling, researching, or building another method to attack. This could also simply force them to move on.

**TTPs**

Finally, we come to **tactics, techniques, and procedures (TTPs).** These are not just tools, but these are behavior patterns. You learn their methods by profiling the behavior and responding accordingly, such as spearphishing with PDFs. These attackers are human and act in similar, producible patterns. Forcing them to change their behavior and methods is the most time-consuming defense against them. This requires a reworking of their whole methodology in attacking.
### Why Use It?

The purpose of recognizing these indicators is how to best identify weaknesses and mitigate them. Most importantly, it makes the lives of these adversaries harder. Each layer in front of the bad actor helps solidify your response and tune your organization to better prepare and detect and respond to indicators of compromise.

---