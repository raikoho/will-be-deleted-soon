threat intelligence is information that an organization uses to understand the threats that are currently targeting them, or could target them in the future
This knowledge can help security teams to develop better defenses, mitigate cyber risk, and aid with monitoring their networks for any signs of compromise.
## Threat Intelligence Lifecycle

Threat intelligence is all about gathering raw data and transforming it into intelligence that has value and can actually be used. To achieve this, we can follow what’s known as the “Threat Intelligence Lifecycle”. This can vary depending on which organization you’re looking at – so we’ll be combining the best bits of the lifecycles presented by [Recorded Future](https://www.recordedfuture.com/threat-intelligence/) and [CrowdStrike](https://www.crowdstrike.com/epp-101/threat-intelligence/).
#### 1) Planning & Direction

This is the most crucial part, as it determines what the scope is for this specific threat intelligence project. Goals need to be set, and the stakeholders need to be clearly defined. This helps the project to stay on track, and not waste time or resources working on intelligence that is not important.

For example, if an organization received intelligence from another company that a foreign hacking group posted on a dark web forum boasting they are about to conduct a prolonged cyber attack against the company, an intelligence program could plan to do the following activities:

- **Research and learn more about the hacking group, including who is involved, and how skilled/sophisticated they are.**
- **Check for public exposure in order to understand the attack surface of the organization** (the total number of ways hackers could break into a network. If a company had all of its systems fully patched, it would have a small attack surface, however, if patches were not applied there are more security flaws attackers can take advantage of).
- **Discover the most appropriate actions that can be taken to defend against this threat**.
#### 2) Collection

This is the stage where the team will go out and collect all of the data they need to achieve their end goal of creating actionable intelligence. In our example, this would include scraping as many posts from the underground forum as they can get access to, any information associated with forum user accounts, performing OSINT searches to try to find information on the group, and anything else they agree is in scope as defined in phase 1. Mature threat intelligence teams typically use a centralized threat intelligence platform (such as MISP, which we will discuss later in this domain) to store indicators and indicators of compromise from a range of public and private threat feeders, which are lists of actionable intelligence shared between organizations.
#### 3) Processing

Now that the team has a vast amount of data, they need to transform it into a clear and readable format so that it can be analyzed, typically by human threat intelligence analysts. Following our example again, it was mentioned that the source of the hacking group’s claim to conduct an attack came from a “dark web forum” and that the actors were foreign. If the posts were not written in English, they would need to be expertly translated to ensure that the exact information was maintained. This is an example of processing collected data to make it easier to analyze.
#### 4) Analysis

This stage involves a human process where processed information (from the previous step) is turned into actionable intelligence that can be used. Depending on the circumstances, the decisions might involve whether to investigate a potential threat, what actions to take immediately to block an attack, how to strengthen security controls, or how much investment in additional security resources is justified.

This information needs to be presented in an appropriate manner based on the audience. If a technical threat intelligence piece was being passed to security analysts then it can remain technical and use security jargon, however, if it is a more strategic piece being presented to a typically non-technical audience such as members of the executive board, then it needs to be simpler and not use jargon, with a focus on how this intelligence affects the business considering factors such as money and reputation.
#### 5) Dissemination

Dissemination involves getting the finished intelligence output to the places it needs to go. This can be SOC or Security Analyst, fellow Threat Intelligence Analysts, and even the executive board (for high-level strategic intelligence, that can be used to inform security budgets and decision making).

For each of these audiences, you need to ask:

- What threat intelligence do they need, and how can external information support their activities?
- How should the intelligence be presented to make it easily understandable and actionable for that audience?
- How often should we provide updates and other information?
- Through what media should the intelligence be disseminated?
- How should we follow up if they have questions?
#### 6) Feedback

It is critically important to understand your overall intelligence priorities and the requirements of the security teams that will be consuming the threat intelligence. Their needs guide all phases of the intelligence lifecycle and tell you:

- What types of data to collect
- How to process and enrich the data to turn it into useful information
- How to analyze the information and present it as actionable intelligence
- To whom each type of intelligence must be disseminated (as mentioned in the dissemination stage), how quickly it needs to be disseminated, and how fast to respond to questions

You need regular feedback to make sure you understand the requirements of each group, and to make adjustments as their requirements and priorities change.

----
## Types of Intelligence

This lesson covers four different types of intelligence; SIGINT, OSINT, HUMINT, and GEOINT.
#### SIGINT

Signal intelligence involves the interception of radio signals and broadcast communications to gather intelligence. This came about as early as the First World War. These come from communication systems, weapons systems, and radar transmissions. SIGINT falls under two different categories:

- `COMINT` **–** Communications intelligence related to communications between people and groups of people (messages and voice) and is often synonymous with SIGINT, even though it is considered a discipline of SIGINT.
- `ELINT` **–** Electronic intelligence is collected from systems not used directly for communications, such as guidance communication for missile systems and radars.

Commonly you can find these methods executed in electronic warfare through surveillance drones, unmanned aerial vehicles (UAVs), and communications interceptions between foreign governments to keep intelligence pipelines open.
#### OSINT

There is an endless amount of information available to us online, almost too much. Open-source intelligence is information that is gathered from public sources. Types of information that can be gathered are driving records, telephone numbers, street addresses, social messaging and social network information, email addresses, domain names, and much more. The amount of information that can be used to detect, track, or stop threats is almost endless. This is also a double-edged sword, in that bad actors can utilize the same information to plan cyber attacks.
#### HUMINT

In the broadest sense, human intelligence (HUMINT) is gathered from other humans. Being effective in this discipline requires an understanding of how humans feel, think, and act, which can vary from person to person. This intelligence is often gathered through in-person meetings, debriefings personnel tasked with acquiring information through observation, document gathering, etc. Such information can be attained through espionage or open communications between diplomats, for example.
#### GEOINT

Whether traveling the seas or flying, geospatial intelligence (GEOSINT) is the type of intelligence that helps these modes of engagement possible during times of natural disasters, wartime, or through other major events, such as political turmoil. Satellite imaging is highly used to provide intelligence personnel with targets, landmass structures, and whether they’re manmade or natural, where our militaries are and their enemies, to better coordinate attack and defense efforts. This also allows aid to allies during times of natural disasters, so first-responders can better identify the state of their deployment.

------

## Disciplines of threat intelligence

There are three primary disciplines of threat intelligence. Let's take a look at each of them!
#### Strategic Threat Intelligence

This type of intelligence provides high-level, typically non-technical information that can be understood by anyone. It is used when presenting to executives and other decision-makers within an organization to aid with decisions such as budget spending and policy review or creation. Below are some examples of strategic intelligence pieces:

- A presentation that covers global events and links them with cyber activity (such as the Coronavirus pandemic resulting in an increase of tailored phishing attacks claiming to be from health authorities such as the World Health Organization).
- A report on patterns of cyber attacks that the organization is facing over a period of time (such as recognizing that the organization is receiving a more distributed denial of service (DDoS) attacks on Monday, and suggesting plans to mitigate this).
- Keeping the internal security team informed about activity related to threat actors that target organizations operating in the same industries (such as the threat intelligence team in a bank monitoring for attacks against other banks, and updating their internal team so they are aware and can prepare for attacks).

Strategic intelligence specialists can be very geographically-focused, understanding the political situation and motives of a country. They will then provide closer tracking of threat actors which have been linked to regions or countries that may pose a threat to the organization based on the industries it operates in. Any geopolitical tension between the country or countries the organization operates in and foreign nations. They will also focus on activity happening within the industry in which the business operates. So strategic analysts at a bank or financial institution would keep track of any cyber attacks that occur within the financial industry.
#### Operational Threat Intelligence

Operational intelligence is all about studying threat actors that might target the organization, in order to gain information about who they are, their motivations, and tactics, techniques, and procedures (TTPs) used to conduct campaigns or prolonged cyber operations. This can help to build more effective defenses by actively monitoring techniques that are used by adversaries, and understanding the actor(s) at a deeper level. This work, which is typically technical, is not easily automated and requires human analysts to track and research malicious groups.
#### Tactical Threat Intelligence

Tactical intelligence is technical in nature and is of immediate value to an organization. It is typically shared in the form of indicators of compromise (IOCs), which are known malicious artifacts such as URLs, domains, email addresses, file hashes, IP addresses, and more. These can either be used by human analysts to check for exposure or can be ingested by security tools via APIs or threat feeds. Below are some examples of tactical intelligence pieces:

- A list of email addresses (IOCs) that are being used to send phishing emails containing the Emotet malware is given to an analyst, and they manually check the email gateway security tool to identify any incoming emails from these addresses.
- A threat feed that can be subscribed to, which includes a constantly updated list of malicious IPs, is primarily intended to feed into network intrusion prevention systems, so they can autonomously block bad IPs.
- A public report from a threat intelligence company that includes a number of IOCs gathered by monitoring exploitation activity targeting a new zero-day vulnerability.

----
## Why Threat Intelligence Can be Useful

If used correctly, threat intelligence has the capability to provide a number of benefits for organizations of any size. Below are a number of examples of how this security practice can provide value to a business by providing in-depth context, prioritization, enrichment, and building a network with other organizations.
#### Cyber Threat Context

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5e9a236fe6328f3c1e5061e438d52d8ba967dd0448e085cbb92cb3553bba511736bfdb39b09e0012b03f74966c17.png)
While a risk analysis may take a very brief look at the threat actors out there and the chance that the organization will be attacked by them, having a dedicated threat intelligence function could allow the business to perform in-depth research on the threats that are out there, and use historic events and targeting to truly determine what the chances are of being in their crosshairs. Proactive defensive measures can be taken to further reduce the risk, such as giving a vulnerability management team context around the vulnerabilities that are identified during a scan, helping to prioritize patching, and reducing the attack surface.
#### Incident Prioritization

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/80600f743ea1ef928e5711e1c84ae220ffc2c88368dc163318fd6632224bc0e1b58424e5ffdb26acf7c786353731.png)
Having two incidents occur simultaneously can be draining on resources, and it’s crucial that the incident with the highest potential impact is given the right attention and resources so it can be dealt with before damage occurs. Threat intelligence context can potentially give incident responders the information they need to make informed decisions about which incident to prioritize based on the threat actors that have been known to target similar organizations, and by retrieving indicators of compromise enrichment to get as much information from every piece of data.
#### Investigation Enrichment

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9777fccd7bfa8c418be1bbc11e34f3316eab36e9bbf9ff528e5e8fa242ea1284d5c8600961cf659efc9ae4f513c0.png)

Giving context to an investigation can make a huge difference. An IP on the internet scanning the organization’s public IP range is very common, and normally these IPs are either blocked (if they are sending a high volume of requests) or left alone as the perimeter firewalls are actively blocking them. But, if the threat intelligence context states that this IP has been utilized by an advanced persistent threat (APT), such as a foreign nation-state, then this definitely needs more investigation and analysis to see exactly what the IP in question is scanning for.
#### Information Sharing

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/68e71a1aecdb16e609a114a96255e43a1a917cdb2b9bbccca75c93010200b22e66b7b6712f240d9cd4bebddd2851.png)

Connecting with analysts in other organizations can really help to boost an organization’s security posture, by simply seeing how other organizations manage their security and the tools they use. This insight can help the security team make informed decisions based on experience from intelligence-sharing partners. It can also help the organization to better defend itself, by receiving early warning signs such as precursors and indicators of compromise, so proactive defensive measures can take place, stopping an attack before it has already begun. We will cover how information can be shared, and in what formats, in the lesson **TI5) Strategic Threat Intelligence, IOC/TTP Distribution**.

----
## The Future of Threat Intelligence

Threat intelligence is ever-changing. One big step forward in the threat intelligence and vulnerability management world is the development of **predictive prioritization** by Tenable, the company behind the Nessus vulnerability scanners and auditing tools. 
Before we cover it, we need to set the scene and introduce some vulnerability management basics as it is out of scope for this course.
### CVEs and CVSS Scores

#### **What are CVEs**?

- CVEs (common vulnerabilities and exposures) are a method of uniquely tracking publicly-reported vulnerabilities. If someone finds a vulnerability in the Windows operating system, they’ll report it and apply for a CVE. If granted, a CVE value is generated based on the year and the number of vulnerabilities. An example of this is CVE-2019-0708 which was a critical vulnerability in the Remote Desktop Protocol (RDP) in 2019. Using CVEs makes sharing information easier – you can simply provide someone with a CVE number, and they can look up the ID and find all the information they need (provided it has been published). Revisiting [CVE-2019-0708](https://nvd.nist.gov/vuln/detail/CVE-2019-0708), you can view information about this specific vulnerability by visiting the [National Vulnerability Database](https://nvd.nist.gov/) offered by NIST (just click the CVE number in this sentence!).
- [https://CVEDetails.com](https://www.cvedetails.com/) is a security vulnerability database that has lots of information and can allow us to search for specific CVEs, or even look at vulnerabilities sorted by release date.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c5384e838d17edcf79ccb1343415beb65a2787aa926aa2412681cfe01c9493b0335bbd8009ee4595b7cd0babf78d.png)

#### **What are CVSS scores?**

- **Example CVSS rating:** CVSS:3.0/AV:N/AC:L/PR:N/UI:R/S:U/C:H/I:H/A:H.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d288fd3b2722960342692058afffa321404977d01149ec73d3f5257ba05079ebd3328a3c27a61c6bbb5774106de2.png)

This is the Common Vulnerability Scoring System, used to help rank vulnerabilities based on their attributes. Whilst this may look like some confusing code, it’s actually fairly simple. **Base Score: 8.8 HIGH** tells us that this vulnerability has a high severity. 
The idea behind these scores is that it provides value at a glance, so you can look at the score and immediately tell if this vulnerability is bad. 
Obviously, this is a generic score, and what may be a critical vulnerability for one company may not affect another company at all – it all depends on the products and versions you’re using, the security controls you have in place, and a number of other factors, so this score value should only be taken as a generic guideline.
### Vulnerability Context

The issue with CVSS scores is that a vulnerability that may be rated 10.0 CRITICAL might not actually affect some organizations, as it depends on the technology that is being used. A vulnerability in Solaris systems isn’t going to affect a company that uses only Windows systems.

Another issue is that whilst some vulnerabilities could be very damaging if executed correctly, hackers might not actually bother trying to exploit them due to factors such as technical complexity. If no threat actors are exploiting a critical-rated vulnerability, then there is less of a risk than a high-rated vulnerability that is actively being exploited in the wild (a term used to describe activity across the internet).

It’s all about context and tracking exploitation activity to determine the prioritization rating for the organization. But the guys and girls over at Tenable have had a very clever idea.
### Predictive Prioritization

Tenable claims that predictive prioritization will help “focus first on the security issues that matter most”. Predictive Prioritization combined vulnerability data with threat intelligence to provide context and generate new scores that consider which vulnerabilities are most likely to actually be exploited. 
The new scoring system, named Vulnerability Priority Rating, or VPR, is a dynamic value that will change based on threat intelligence updates – if a previously quiet vulnerability was suddenly seen being exploited in the wild, the VPR number would go up, so that security teams know it has a higher priority for remediation. 
This is the perfect case study to talk about when considering how threat intelligence will change the future of cybersecurity. 
By providing scores that actually reflect the genuine risk of a vulnerability being exploited, organizations can patch security issues that need to be done as a priority, instead of completing remediation work that will have immediate defensive benefit.

---
## Further Reading, Threat Intelligence

### Resources

- **A curated list of Awesome Threat Intelligence resources**  
    **//** [https://github.com/hslatman/awesome-threat-intelligence](https://github.com/hslatman/awesome-threat-intelligence)

- **A curated list of awesome threat detection and hunting resources**  
    **//** [https://github.com/0x4D31/awesome-threat-detection](https://github.com/0x4D31/awesome-threat-detection)

- **A curated list of amazingly awesome open source intelligence tools and resources**  
    **//** [https://github.com/jivoi/awesome-osint](https://github.com/jivoi/awesome-osint)

- **Get the latest technical details on significant advanced malware activity**  
    **//** [https://www.trellix.com/en-us/advanced-research-center.html](https://www.trellix.com/en-us/advanced-research-center.html) 

- **10 of the Best Open Source Threat Intelligence Feeds**  
    **//** [https://d3security.com/blog/10-of-the-best-open-source-threat-intelligence-feeds/](https://d3security.com/blog/10-of-the-best-open-source-threat-intelligence-feeds/)

- **Weekly Threat Briefing—Cyber Threat Intelligence Delivered to You**  
    **//** [Anomali Weekly Threat Briefing](https://www.anomali.com/learn/wtb-ff?utm_medium=cpc&utm_source=google&utm_content=wtb&cid=7011Y000001msr5&ads_cmpid=1490291931&ads_adid=57145116403&ads_matchtype=p&ads_network=g&ads_creative=341966870837&utm_term=threat%20intelligence&ads_targetid=kwd-298507837126&utm_campaign=&utm_source=adwords&utm_medium=ppc&ttv=2&gclid=EAIaIQobChMIkKvBrMLl6QIVVeDtCh24pQTnEAMYAyAAEgJGvPD_BwE)

- **Threat Intelligence Defined and Explored**  
    **//** [https://www.forcepoint.com/cyber-edu/threat-intelligence](https://www.forcepoint.com/cyber-edu/threat-intelligence)

