A typical day in the life as a Cyber Threat Intelligence Analyst focusing on tactical intelligence typically involves performing threat exposure checks to see if malicious indicators have been identified within the environment, conducting public exposure assessments to see how what information about the company and its employees is freely available online and if that could be exploited in any way, and collecting and using actionable intelligence to improve defenses by implementing threat feeds to power automated defenses and provide context to security investigations.

## Threat Exposure Checks Explained
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/949e35a4865d37a90fe806d98428eb49cb7e234cb87d172562a2bde79f8d6e3cb9c8ae52e69efde72ec05d396bdb.png)
A threat exposure check is when an analyst uses multiple tools such as SIEM and EDR to look for the presence of any indicators of compromise they have retrieved from intelligence vendors, information sharing partners, government alerts, or OSINT sources. 
This activity is considered a tactical task, as it requires a deep technical understanding to analyze the results from several different tools to determine if any exposure has been detected, and then assess exactly what’s been observed so it can potentially be passed to security analysts for investigation.

---
## Watchlists/IOC Monitoring

IOC monitoring is an important part of security operations and can help alert security analysts to malicious activity by monitoring for the presence of any precursors or indicators of compromise across the environment. Watchlists are typically created in either the SIEM or EDR platform (or both).

This allows Threat Exposure Checks (TECs) to be conducted continuously without a need for a human threat intelligence analyst to perform the searches themselves, freeing them up to work on more important tasks.
#### Example – Malicious IP Watchlist

A Threat Intelligence Analyst is given a list of IP addresses that have been acting malicious (used for command-and-control, scanning IPs, used to host malware, etc). The Analyst decides to create a watchlist within their SIEM platform to generate an alert whenever a malicious IP address is observed as either the Source or Destination IP.

This alert fires when an employee clicks a malicious link in a phishing email, taking them to a web server hosted on one of the monitored IPs that is used to distribute malware. A Security Analyst opens the alert and can determine what has happened and can take action to protect the user.

---
## Public Exposure Checks Explained

When we say public exposure checks, what we mean is the process a threat intelligence analyst takes to determine what information is publicly available online about their organization, and if this can be exploited in any way to cause damage. 

This can range from employees posting pictures of them in the office on social media to employee credentials in data breach dumps for sale on the dark web. This work is important and works to protect the organization more than you think.
### Social Media Monitoring

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4b8a831a50ee8a31dea49d36cb14326a157f918f8071b6e0b475fdc49d75765088bcf8fd1c373ed16777f147bac1.png)
#### Image Metadata

**Why do we care if people take selfies in the office?** – We’re not robots, and let’s face it, we don’t work 100% of the time we’re at work. As long as we’re not disruptive or unproductive it’s usually fine. But taking photos at work can cause some serious issues. You’d be surprised at what information can be contained in a single photo. If you took a photo at work, depending on the device and settings, attackers could potentially discover the make and model of the device you took the photo on, the devices name (we typically name our devices after ourselves, such as “Josh’s iPhone”), the date and time the photo was taken, and in some cases even direct GPS coordinates. If this photo gets posted to social media, an attacker could immediately find the exact location of that office – super not good if it’s a secure or covert site.
#### Leaked Information

Following on from the example above of taking photos or videos in an office, there’s still more damage that can be done. Maybe the selfie looked really good and you’re getting tons of likes on Instagram, but what about the computer screens in the background that are extremely clear, and show the operating system and programs your organization uses. What about the whiteboard on the far wall with confidential business diagrams and information all over it. And the sticky note on someone’s screen with their login details. Even tiny details can help attackers in the long run. An innocent photo could end up being a goldmine of information for attackers, so be careful what you post, and refer to the organization’s social media policy!
#### Early Warnings Signs of Insider Threats

John posts on Twitter that he hates his job. Okay, maybe he’s just had a bad day. John continues to tweet how he’s had enough, he doesn’t get any respect from his peers, and he’s “going to do something about it”. This Tweet could mean a lot of different things – maybe John is going to work extra hard, or just maybe he’s going to become an insider threat, and intentionally cause damage to company assets. The security team can monitor the situation, and work to monitor this individual closer using forensic-grade tools such as [DTEX](https://www.dtexsystems.com/). Whether the employee uses technical skills and access to damage IT equipment, steals confidential documents and gives them to competitors, or works with malicious actors to give them a foothold in the network, monitoring early signs like this could turn out to be nothing, or it could save the organization a lot of money by stopping an attack before it happens.
#### Brand Abuse and Impersonation

Social media account hijacking requires access to legitimate login credentials. Impersonations do not, and therefore are much more dangerous. Impersonations can occur when a threat actor pretends to be an individual or organization, often seeking to either tarnish a reputation, cause general chaos and confusion, or conduct a phishing campaign. With almost no effort, in the digital world, nefarious actors can create digital footprints (websites, social media, e-commerce, apps, etc.) that look like your brand and execute a monetization strategy to target your customers. The immediate impact of brand infringement on your business is lost revenue and eroded customer trust.
### Data Breach Dumps

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4d5e0bff25132b025fb1d77cd4308ec4cabb12ac0d13401ef681f506dac5f29274defe657d244163b7f7c9094eb5.png)

**Data breaches happen all the time**, and unfortunately, sometimes employees get caught up in it. While it is not the job of the security team to alert employees if their personal email addresses have been included in data breaches, it is important when company email addresses are included, especially if passwords were leaked. Password reuse is common, and it won’t go away – it’s just too convenient, but it’s very insecure. If James G was going on a work trip and stayed with The Blue and White Hotel when he books it he’ll probably use his work email, as it’s a work trip, and he can get the expenses refunded by the company. If the hotel gets hacked, and email addresses and passwords are leaked, it’s only a matter of time before _someone_ tries to use James’ credentials elsewhere.
#### Acquiring Data Breach Lists

Sometimes these lists can be shared on the clear web, and threat intelligence analysts can acquire them for analysis, looking for any company-owned email addresses. Other times it can be a lot harder to get access, such as if the list is only being sold to trusted customers on the dark web. Threat intelligence companies around the world work hard to infiltrate dark web marketplaces, and will sometimes purchase data breach lists on behalf of all their clients, allowing them access to only the data related to their organization, reducing further exposure of credentials or private details.

---
# Threat Intelligence Platforms

Threat Intelligence Platforms can be deployed as Software-as-a-Service or an on-premises solution to effectively manage a large volume of cyber threat intelligence, such as; actors, campaigns, signatures, bulletins, and Tools, Techniques, and Procedures (TTPs). TIPs are designed to provide the following functionality for security teams:

1. Aggregation and normalization of intelligence collected from multiple sources.
2. Integrate with existing security controls such as firewalls and intrusion prevention systems.
3. Analysis and sharing of threat intelligence.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2247c748871e9844eff5551069b70f7e234d8c6d03685101e8fc58cfb1f5d8c6e0fbd3b51628db4713044e90a7d8.png)

## Why use a TIP?

Simply put, a Threat Intelligence Platform allows an organization to store everything related to threat intelligence in one single location. Whether it’s technical indicators of compromise or high-level awareness reports, TIPs provide a solid foundation for any cyber threat intelligence function. Anomali have defined three main groups that will benefit from the implementation of a TIP:
#### Security Operations Center (SOC) Teams

- These teams are focused on the operational day-to-day tasks and responding to threats as they occur. A TIP provides automation for routine activities such as integrations, enrichment, and scoring.
#### Threat Intelligence Teams

- These teams look to make predictions based on associations and contextual information between actors, campaigns, etc. A TIP provides them with a “library” of information that simplifies and streamlines this process.
#### Management and Executive Teams

- A TIP provides management with a single platform through which to view reports at both technical and high levels. This enables them to effectively share and analyze data as incidents occur.
## Data Aggregation

A Threat Intelligence Platform automatically collects and reconciles data from various sources and formats. Ingesting information from a variety of sources is a critical component of a strong security infrastructure. Supported sources and formats include:

**Sources:**

- Open-source
- 3rd party paid
- Government
- Trusted Sharing Communities (ISACs)
- Internal

**Formats:**

- STIX/TAXII
- JSON and XML
- Email
- .csv, .txt, PDF, Word document
## TIP Products

There are numerous Threat Intelligence Platform products in the industry. Let’s briefly take a look at some of them and their features.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1f404e7fbff503f2e2e228f82e914ff62870bcec48054dd2ec143cabad20f8ed9149dd07dfb97307d9ef157e0d5d.png)

### Malware Information Sharing Platform (MISP)

**Website:** [https://www.misp-project.org/](https://www.misp-project.org/)  
MISP is an open-source, community-ran project, developed and maintained by an awesome group of [volunteers](https://www.misp-project.org/who/#who-is-behind-the-misp-project). MISP is used by over 6000 organizations around the world, and has been designed to be as simple as possible, making it accessible and usable. MISP offers an absolute ton of features providing extended functionality for multiple use-cases, including the ability to easily share intelligence with fellow humans, and even automated defenses.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9c8a6845d403c7fd7526973ef9e7afc76bab268af3efcaab339e4bb4ba7ed444a1fd17d55390d881260e749e07d7.jpg)

### ThreatConnect

**Website:** [https://threatconnect.com/solution/threat-intelligence-platform/](https://threatconnect.com/solution/threat-intelligence-platform/)  
ThreatConnect have produced their own Threat Intelligence Platform that can completely automate the intelligence collection process, regardless of the source format. Whether it’s an email, RSS feed, or blog, ThreatConnect can ingest it and store the intelligence within the TIP. ThreatConnect also provides automation in the form of runbooks, allowing human analysts to determine what actions should be taken under specific circumstances.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d0cf43fa0b07744e0be1836ffa46e6bc0abe843c21a080f78d3f154c1d2329127b45b37a21dff0f60c488f1129fe.png)
### Anomali

**Website:** [https://www.anomali.com/](https://www.anomali.com/)  
The TIP produced and maintained by Anomali is utilized by many different Information Sharing and Analysis Centers including the [Financial Services Information Sharing and Analysis Center (FS-ISAC)](https://www.fsisac.com/who-we-are). Anomali offers the ability for an organization to quickly and easily create its own ISAC, allowing other organizations to partner together and share intelligence together. The website also offers an “app store” where organizations can purchase integrations and threat feeds to boost the capabilities or the TIP and other security controls utilized by the organization.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7087c5f94c685b06cf6fb50bf1420a8d7bef1091713e2d4fd95c96f91e519a86cc765b3ca3d1a4cfcf1906231977.png)
### ThreatQ

**Website:** [https://www.threatq.com/threat-intelligence-platform/](https://www.threatq.com/threat-intelligence-platform/)  
The ThreatQ platform is based on a threat-centric approach to security operations, allowing security teams to “prioritize based on threat and risk, collaborate across teams, automate actions and workflows and integrate point products into a single security infrastructure”. ThreatQ also states that it can do more than a typical TIP, and can assist with security practices such as Vulnerability Management, Spear Phishing, Incident Response, and Threat Hunting.

---
## Malware Information Sharing Platform (MISP)

The Malware Information Sharing Platform (MISP) is an open-source software solution created by a community of volunteers for collecting, storing, distributing, and sharing cyber security indicators and threats about cyber security incidents analysis and malware analysis. MISP is designed by and for incident analysts, security and ICT professionals or malware reversers to support their day-to-day operations to share structured information efficiently.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f2a05d51d785d3d0faf0f6019c9c9788c3c4abe40702dd4bc972299ecbd46fdcf8c7ff2e883719172b8cc047d199.png)

The objective of MISP is to foster the sharing of structured information within the security and threat intelligence communities. MISP provides functionalities to support the sharing and consumption of information from tools such as Network Intrusion Detection Systems (NIDS), Host Intrusion Detection Systems (HIDS), and log analysis tools such as SIEMs.

It’s important to mention that other similar platforms do exist, however, we will be using MISP due to the functionality and availability as a result of it being a free and open-sourced project.
### What Does MISP do?

- Facilitate the storage of technical and non-technical information about seen malware and attacks
- Automatically create relationships between malware and their attributes
- Store data in a structured format (allowing automated use of the database to feed detection systems or forensic tools)
- Generate rules for Network Intrusion Detection System (NIDS) that can be imported on IDS systems (e.g. IP addresses, domain names, hashes of malicious files, pattern in memory)
- Share malware and threat attributes with other parties and trust-groups
- Improve malware detection and reversing to promote information exchange among organizations (e.g. avoiding duplicate works)
- Create a platform of trust – trusted information from trusted partners
- Store locally all information from other instances (ensuring confidentiality on queries)
### How Does MISP Work?

Malware Information Sharing Platform is accessible from different interfaces like a web interface (for analysts or incident handlers) or via a ReST API (for systems pushing and pulling IOCs). The inherent goal of MISP is to be a robust platform that ensures a smooth operation from revealing, maturing, and exploiting the threat information.

There are 4 options regarding distributing events and their respective attributes:

- Your organization only (private)
- This community only
- Connected communities
- All communities (public)

There is also a set of sharing groups accessible to various members per sector (such as the Financial sector).

**MISP, Malware Information Sharing Platform and Threat Sharing, core functionalities are:**

- An efficient IOC and indicators database allows to the storage of technical and non-technical information about malware samples, incidents, attackers, and intelligence.
- Automatic correlation finding relationships between attributes and indicators from malware, attack campaigns, or analysis. The correlation engine includes a correlation between attributes and more advanced correlations like Fuzzy hashing correlation (e.g. ssdeep) or CIDR block matching. Correlation can also be enabled or event disabled per attribute.
- Built-in sharing functionality to ease data sharing using different models of distributions. MISP can automatically synchronize events and attributes among different MISP instances. Advanced filtering functionalities can be used to meet each organization’s sharing policy including a flexible sharing group capacity and attribute level distribution mechanisms.
- An intuitive user interface for end-users to create, update and collaborate on events and attributes/indicators. A graphical interface to navigate seamlessly between events and their correlations. An event graph functionality to create and view relationships between objects and attributes. Advanced filtering functionalities and [warning lists](https://github.com/MISP/misp-warninglists) to help the analysts to contribute events and attributes and limit the risk of false positives.
- Export: generating IDS, OpenIOC, plain text, CSV, MISP XML or JSON output to integrate with other systems (network IDS, host IDS, custom tools), Cache format (used for forensic tools), STIX (XML and JSON) 1 and 2, NIDS export (Suricata, Snort and Bro/Zeek) or RPZ zone. Many other formats can be easily added via the misp-modules.
- Import: bulk-import, batch-import, import from OpenIOC, GFI sandbox, ThreatConnect CSV, MISP standard format or STIX 1.1/2.0. Many other formats easily added via the misp-modules.
- STIX support: import and export data in the STIX version 1 and version 2 format.

---