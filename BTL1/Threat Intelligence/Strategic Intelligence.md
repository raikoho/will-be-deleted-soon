This section of the Threat Intelligence domain will focus on strategic roles and responsibilities. A typical day in the life as a Cyber Threat Intelligence Analyst focusing on strategic intelligence typically involves collecting and sharing actionable intelligence with partners and the internal security team to provide threat intelligence context, giving defenders more useful information about malicious actor activity on a global scale.

## Intelligence Sharing and Partnerships

If an organization has an established threat intelligence team, someone will likely be responsible for connecting with other organizations to join or form an **Information Sharing and Analysis Center** (ISAC). These are typically industry-specific groups comprised of multiple organizations in order to share actionable intelligence such as indicators of compromise, precursors, and information about attacks and threats.

For example, if Organisation A operates in the aviation industry, and so does Organisation B, they could form an intelligence-sharing partnership, and recruit in other organizations that also operate in the same industry. Together they can share information to help each other defend against threats that target the aviation industry. If Organisation B suffers a damaging cyber attack, they can share information about the attack with other members of the ISAC so they can take proactive defensive measures so the same doesn’t happen to them. ISACs can be extremely beneficial if members are active, regularly share intelligence, and have online meetings to discuss trends and strategic intelligence surrounding threats.

An example of an ISAC is the Aviation ISAC or a-isac. This is a collective of organizations that operate within the aviation industry and come together to share threat intelligence to help each of the member partners to better defend themselves. You can view their website for more information, and an insight into a real ISAC here – [https://www.a-isac.com/.](https://www.a-isac.com/)
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/93dc90fa838af1a346876870580151fb99f94bf5e2f26c51f282424c1a3b98c13f1608f4a6b7f73340abae013576.png)
Having someone that focuses on strategic intelligence to manage and maintain relationships with not only ISAC and industry partners, but also government contacts and agencies could bring valuable intelligence into the organization so it can be used to power defenses and keep team members updated with trends and campaigns that they could have to deal with in the future.

---
## IOC/TTP Gathering and Distribution

While the task of collecting and distributing indicators of compromise and TTPs can be completed by anyone, it makes sense for a strategic threat intelligence analyst to perform this duty, as they will regularly be in contact with information-sharing partners and receive government-issued alerts from organizations such as [NCCIC](https://www.cisa.gov/national-cybersecurity-communications-integration-center), [US-Cert](https://www.us-cert.gov/), [NCSC](https://www.ncsc.gov.uk/), and more.

This task includes gathering IOCs regarding threat actors that are likely to target the organization, as trying to digest IOCs from every single cyberattack out there will generate a lot of noise and overwhelm defenders with alerts and false positives. If a threat actor is targeting banks and banking systems, the threat intelligence team at an aerospace company isn’t going to be running the same equipment and therefore is unlikely to encounter that specific threat agent.

IOCs that are gathered from threat intelligence vendors, government alerts, information sharing partners, and public sources are then passed down to tactical threat intelligence analysts, or the wider security team based on the information. We’ve created a diagram to help visualize this process.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/df5ac5444669d9f8d6080cabaf85dcd37a4b5ee343ad1b11777cfd502611f3e27d56754bd0c1b94f0be469109643.png)
# Example Walkthrough

The strategic threat intelligence analyst at Organisation A receives an email from an analyst at Organisation B, who is in their industry-specific information-sharing partnership (ISAC). Organisation B’s analyst informs the strategic analyst that they have just been hit by an APT who specifically targets the industry they operate in, and during incident response, they collected IOCs including IP addresses that were used to scan and exploit systems at Org B. The strategic analyst then passes these IOCs to a tactical threat analyst who performs threat exposure checks within the SIEM platform to see if the same IPs have scanned Org A recently based on perimeter firewall logs.

The strategic analyst also provides the wider security operations team with a situational awareness email, informing everyone that a similar organization has been hit by an APT and that they may target Org A in the near future.

---
## OSINT vs Paid-for Sources

### Open-Source Intelligence

There are a ton of great resources to collect free intelligence, but this information needs to be reviewed, and sources should be verified to ensure the intelligence is legitimate and of use. For organizations looking to build out a threat intelligence capability, starting with OSINT sources can be a great way to get used to collecting, analyzing, and utilizing threat intelligence for strategic, tactical, and operational purposes. Free intelligence sources can also be great for independent security researchers that want to provide more context around cyber-attacks and activity.

**Some great sources of free and open-source intelligence include:**

- [**Spamhaus**](https://www.spamhaus.org/)
- [**URLhaus**](https://urlhaus.abuse.ch/)
- [**AlienVault Open Threat Exchange**](https://otx.alienvault.com/)
- [**Virus Share**](https://virusshare.com/)
- [**List of Free Threat Feeds**](https://threatfeeds.io/)
- [**Anomali Weekly Threat Briefing**](https://www.anomali.com/learn/wtb-ff?utm_medium=cpc&utm_source=google&utm_content=wtb&cid=7011Y000001msr5&ads_cmpid=1490291931&ads_adid=57145116403&ads_matchtype=p&ads_network=g&ads_creative=341966870846&utm_term=threat%20intelligence&ads_targetid=kwd-298507837126&utm_campaign=&utm_source=adwords&utm_medium=ppc&ttv=2&gclid=Cj0KCQjwz4z3BRCgARIsAES_OVd8ssLYx3uxKt8FJsAFedmLSBcZroI9ROnujeaZMQhjZPw-y6XoPX0aAofMEALw_wcB)
- [**US Cybersecurity and Infrastructure Security Agency – Automated Indicator Sharing**](https://www.cisa.gov/automated-indicator-sharing-ais)
- [**SANS Internet Storm Center**](https://isc.sans.edu/)
- [**Talos Intelligence – Free Version**](https://talosintelligence.com/)
### Paid-For Intelligence

Purchasing intelligence from vendors can be very expensive, and is likely not a viable option for small to medium organizations. It is typically large enterprises that have dedicated threat intelligence teams that are able to ingest the intelligence and put it to use. But even with a big budget, intelligence can still take a chunk out of it. It’s advised to identify what kind of intelligence the organization actually requires, based on the threats that have, or may target, the industries that the company operates in. This is a good idea when purchasing intelligence from vendors such as FireEye, which sells it based on packages relating to different fields and industries.

**If you’re interested in finding out more about paid-for intelligence, take a look at the sites for some of the giants in this game:**

- [**FireEye**](https://www.fireeye.com/)
- [**Recorded Future**](https://www.recordedfuture.com/)
- [**CrowdStrike**](https://www.crowdstrike.com/)
- [**Flashpoint**](https://www.flashpoint-intel.com/)
- [**Intel471**](https://intel471.com/)

---
## Traffic Light Protocol

Traffic Light Protocol, shortened to TLP, is a way of classifying information for sharing and is commonly used for security reports and threat intelligence.

The purpose of TLP is to allow the author of the original information to state how they want their information to be circulated, such as sharing only with specific individuals, within an organization, within trusted communities, or in the public domain. It is extremely important that if you ever receive a document that uses the TLP system you do not breach the intended level of distribution, as the entire protocol relies on trust.
### TLP Classifications

#### TLP Clear

Information that is classed as TLP CLEAR can be publicly shared, but copyright rules still apply. Reports or updates that use this TLP are distributed freely for the good of everyone.

**Example:**

The US Cybersecurity and Infrastructure Security Agency (CISA) shares a number of TLP:WHITE analysis reports on malware, and freely shared the related indicators of compromise. Other organizations offer the ability for anyone to subscribe to an email listing that will send out security updates and reports which can be freely shared. We suggest students take a look at a couple of the CISA analysis reports, they’re awesome! – [Cybersecurity Alerts & Advisories | CISA](https://www.cisa.gov/news-events/cybersecurity-advisories)
#### TLP Green

Information that is classed as TLP GREEN may be shared within communities, such as information sharing and analysis centers (ISACs), which are groups of organizations operating in the same industry or industries. This information should not be shared outside of the intended communities, such as posting it publicly on the internet.

**Example:**

‘Organisation A’ operates in the aviation industry and forms an ISAC with four other companies who all operate in aviation too. One day Org A is subject to a cyber attack from APT33, an Iranian-based threat actor that has been known to target this sector. During the incident response process, Org A collects a number of indicators of compromise (IoCs) such as the email address that sent a spear-phishing email, hashes of malicious files, IP addresses used for command-and-control communication, and so on. Org A has the choice to disclose the IOCs ISAC member organizations to help other companies defend themselves from the same threat actor, but this means these companies (which may be competitors in the business space) will know Org A has been the victim of a successful cyber attack (which could damage the reputation, projected sales, stock price, etc if it is leaked to the public).
#### TLP Amber

Information that is classed as TLP AMBER may only be shared internally, or with clients of the organization, on a need-to-know basis to limit who has access to the information.

**Example:**

Penetration test reports, red team engagement reports, and vulnerability scan results are likely to be TLP AMBER as they contain information about serious security flaws that can be exploited to achieve certain actions. Only specific individuals within the organization would need to see these documents, and if they were publicly disclosed there is the chance that malicious actors will find these sensitive reports and could use them to launch effective cyberattacks against the organization because they now have detailed information about the systems, network layout, and vulnerabilities present within that company.
#### TLP Amber Strict

This classification restricts sharing to the _organization_ only. TLP:AMBER+STRICT may be used when information requires support to be effectively acted upon however still carries risk to privacy, reputation, or operations if shared outside of the organization.

**Example:**

An Advanced Persistent Threat (APT) group has just launched a new kind of malware. A cybersecurity firm has discovered this malware during an investigation for a client. The malware has a unique signature that has not been detected by any other antivirus or endpoint detection systems yet. The team would continue to investigate and analyse any findings and write up a report, This report would typically include its technical indicators, behaviors, and potential mitigation steps.

In this instance - this report would be classified as TLP AMBER:STRICT as a firm's public report like this could potentially tip off the APT group. This classification would mean tighter restrictions over how the report is distributed, especially within the organization.
#### TLP Red

Information that is classed as TLP RED is **extremely** sensitive and could have severe consequences if it falls into the wrong hands. If an online or in-person meeting is classed as TLP RED then the information should not be shared with anyone that isn’t present in the meeting. Regarding electronic communication such as emails, if an email is TLP RED then only the listed recipients should be exposed to the material, and it should not be shared under any circumstances without the author’s permission.

**Example:**

During a threat hunt, the blue team has discovered what they believe to be an advanced adversary within the network that has Domain Administrator privileges (the highest possible access and permissions). A meeting occurs between the hunting team, the security incident response team (SIRT), and other personnel. Due to the nature of this attack, the organization doesn’t want any information getting out that could alert the adversary that they have been discovered, so only the persons in the meeting are permitted to discuss what has happened.

---
## Permissible Action Protocol

PAP is a framework designed to classify **actions** based on the potential exposure of sensitive data to malicious entities. Just as with TLP, the PAP structure also relies upon a tiered system, each distinctly represented by a color code.
### PAP Classifications

#### PAP Clear

Actions are relatively unrestricted at this level. There are no severe constraints and information can be handled as desired provided they align with legal and licensing frameworks. The primary goal is to ensure a seamless yet compliant handling of the data.
#### PAP Green

PAP at this level permits controlled, non intrusive actions with malicious sources.,

This would be likened to something like an organization blocking incoming threats at their firewall, especially if they can trace it back to a particular IP. Similarly, blocking outbound malicious traffic targeting specific web addresses via proxy servers is a standard protocol.
#### PAP Amber

Activities at this level are confined to passive data handling, ensuring actions remain undetected by malicious sources.
##### Example:

PAP:AMBER in this instance would be if organizations leverage open-source platforms or online knowledge repositories to further clarify and understand the provided data from an investigation or a breach.

In situations where infrastructure might already be compromised, this data proves pivotal to pinpoint possible IOCs.

Note, that direct or indirect communication with the threat actor is forbidden at this level.
#### PAP Red

PAP:RED at this level is centered exclusively around detection and investigation of the threat actor. Just like TLP:RED access is based on a "need-to-know" principle. The infrastructure at hand is typically protected from the public domain but also segregated from the organization's overall system to seclude the information and maintain integrity. In this instance, direct engagements with external services and devices are a strict off limits.

It is expected that permitted actions will be invisible to potential adversaries. A classic example would be searching non-production environments based on previously logged data.
##### Example:

Threat hunting and Incident Response teams are to be mentioned here as they typically have insight and capabilities to monitor infrastructures to confirm the absence or detect the appearance of a threat while maintaining the integrity of the isolated network their are monitoring.