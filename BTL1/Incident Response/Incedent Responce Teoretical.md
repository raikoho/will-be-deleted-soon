## Security Events vs Security Incidents

This lesson will explain the key differences between security events and security incidents. It is important to establish why these are different and why different measures are taken to address them. By the end of this lesson, you should be able to explain the difference and provide examples of each category. **It’s important to remember that all security incidents are security events, but not all events become incidents.**
## Security Events

A Security event is anything that _**could**_ have a security implication, such as causing damage or disruption. Examples of this include:

- **Spam emails –** as they could potentially include hyperlinks to malicious websites such as credential harvesters or malware downloads.
- **A malicious actor performing a vulnerability scan –** as this could identify a vulnerability that can later be exploited.
- **A malicious actor performing reconnaissance scans –** as this helps them to build up a better idea of the systems used by the organization, which can be researched to identify vulnerabilities and weaknesses.
- **An explained anomaly –** an unusual circumstance, but the cause is identified and it is not malicious (such as disruption on the network caused by a misconfiguration).
- **A user downloads software from the internet –** to a company-owned device. There is always a risk with downloaded files from the internet. Users that are not very tech or security-savvy may inadvertently download malicious software or legitimate software that is bundled with malware such as trojans.
- **A malicious actor begins a brute-force attack –** against a login portal on a web server. This is an event until the attacker gains access.

Security events are happening constantly, and are typically dealt with by automated security controls or simply logged in case they evolve into security incidents.
## Security Incidents

Security incidents are security events that have resulted in damage to the organization. Revisiting the examples of security events, let’s cover how they could turn into incidents.

- **The spam email –** contained a malicious URL that downloads Maze ransomware to the system, encrypting all of the organization’s files. The email being delivered is the **security event**, and the ransomware encrypting files is the **damage** as it causes operational disruption.
- **The vulnerability scan –** showed a number of easily-exploited vulnerabilities, which the malicious actor proceeded to exploit giving them remote access to a server in the DMZ, where the actor then exfiltrated data from a database. The vulnerability scan is the **security event**, and the data breach is the **damage**.
- **An unexplained anomaly –** an unusual circumstance, where the root cause has not yet been identified. This is classed as an incident, as until this has been properly scoped, there is the potential for malicious activity.
- **A user downloads software from the internet –** to a company-owned device. This turned out to be a piece of malware, which infected the system and began beaconing to its command-and-control server to retrieve instructions. The operators tell the malware to collect common files (such as .docx, .xlsx, .pptx) and send them to the malicious actors. The user downloaded software is the **security event**, and the data exfiltration is the **damage**.
- **A malicious actor is successful with their brute-force attack –** against a login portal on a web server. They can now browse files, edit web pages, and view the contents of a MySQL database. The brute-force attack is the **security event**, and the intrusion and access of private information is the **damage**.

## Events vs Incidents

Security events will typically be dealt with by security analysts (often within a Security Operations Center, or SOC) whereas security incidents are often handled by specialist incident responders (depending on the size of the organization and security team) who can perform advanced analysis and investigation into what exactly has occurred, and how to contain and respond to the incident. If there is a high risk to the organization, either an internal or external Computer Security Incident Response Team (CSIRT) may be activated to respond.

Not every SIEM or IDS alert is an incident. It is more likely to be an event that is manageable, such as an IP scanning the organization’s public IP range, or it could even be a false positive, where an alert is generated, but no malicious activity has taken place. It’s important to look into every alert that is generated, and use knowledge and experience to determine what this alert is representing, and how to respond to it appropriately.

---
# Incident Response Lifecycle

Many organizations have procedures for handling computer-security incidents, and this is known as having an Incident Response Plan (IRP).  Many of these plans are based on the NIST SP 800 61r2 guidelines. While different organizations have put forward other types of incident response lifecycles, like SANS, the one guided by NIST has shown to be the most popular.  The Incident Response Lifecycle is split into four different categories and this document will be going over each one individually.  One thing to keep in mind is that the cycle is an ongoing process and all four parts are used to help prevent the same incident from recurring in the future.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4ee8b7b48b8a8bd5c0f93b9df8e7f001274acad723564866d0d7925db0d7ff695ec906825c7f033faf09647561c4.png)

_Source:_ [_NIST_](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)
### Preparation

Being prepared is one of the most important aspects of incident response.  If you do not have the right teams, resources, or documentation then the incident response process is being set up for failure. With the right amount of preparation, you can prevent attacks before they even happen.  Being prepared consists of two major groups, being prepared for incidents and actively preventing incidents. 

Some activities that involve being **prepared for incidents** are:

- Contact Information for all stakeholders
- Having a war room for central communication and coordination
- Documentation
- Baselines for running systems
- Equipment that can be used in an IR scenario, such as digital forensic toolkits

Activities that involve actively **preventing incidents** would be:

- Having current risk assessments
- Utilizing Client and Server security
- Having a user awareness and training program established

While there is no perfect preparation phase of the incident response process, it is the first line of defense of an attack that could have catastrophic damage.

### Detection and Analysis

The Detection & Analysis phase of IR involves two distinct sub-phases that if properly implemented, will be able to alert the CSIRT team at the company or organization of an active event taking place.  For the detection sub-phase, many SOCs, internal security teams, and organizations have tools such as intrusion detection and prevention systems (IDPs), antivirus/antispam/antimalware software, and log monitoring solutions set up to alert the appropriate team when incidents are detected.  Having members of the IR team know what systems are in place, can be beneficial in knowing how to enter the next sub-phase, analysis.  Analysis can often be one of the most complex steps in the IR lifecycle because it involves finding how the initial attack took place and how it moves throughout the network.  Many organizations utilize network profiles and baselines, knowledge bases, and policies for log retention, in order to make this phase easier for the incident responder. 

Three other things to note is that the responder needs to be able to effectively document their finding when analyzing the attack, as well as prioritize actions that need to be taken place, and then the IR team needs to notify the proper authorities. This notification is often outlined ahead of time in what is typically called a Communication Plan that exists within various organizational policies. This includes managers, computer leaders, Human Resources, and the Legal department to name a few and then those parties would alert third parties or the public, depending on the type of organization that the attack occurs in.   With those two sub-phases completed, the responder can continue to the next phase of the IR process.
### Containment, Eradication, Recovery

The Containment, Eradication & Recovery phase of the IR Lifecycle contains two sub-phases that are extremely important to ensure that the organization can successfully recover from the attack.  The first sub-phase is containment, and this can come in many different forms.  For example, the way to contain a mass-spear phishing campaign would be a lot different than a Sodinokibi ransomware attack.  There are a few key criteria that NIST established to determine what the containment strategy should be:

- **Potential damage to and theft of resources**
- **Need for evidence preservation**
- **Service availability**
- **Time and resources needed**
- **Effectiveness**
- **Duration of the solution**

During the containment sub-phase, it is also important, like the Detection & Analysis phase, to keep a detailed log of all evidence that you find regarding the attack.  This could be information that could be used for further prevention tactics, as well as the knowledge that could be shared with the cybersecurity community.  The second sub-phase is eradication & recovery and this phase is the act of returning your systems back to normal.  Actions for eradication could consist of rebuilding machines from known good backups, deleting a malware, or resetting credentials on compromised accounts.  Actions for recovery consist of restoring those systems to their pre-attack state.  This could also include eliminating any vulnerabilities that were exploited in the attack, as well as changing passwords, installing patches, tightening network security, etc.
### Lessons Learned

The most important part of the Post-Incident Activity phase is learning and improving the existing systems. Incident response teams are supposed to be an ongoing and ever-growing effort to prevent threats before they happen and respond to new threats as they emerge.  

NIST recommends holding a “lessons learned” meeting that could address the following questions:

- Exactly what happened and when did it happen?
- How well did staff and management perform in dealing with the incident?
- What information was needed sooner?
- Were any steps or actions taken that might have inhibited the recovery?
- What would staff and management do differently the next time a similar incident occurs?
- How could information sharing with other organizations have been improved?
- What corrective actions can be taken?
- What indicators should be watched for in the future?
- What additional tools or resources are needed to mitigate future incidents?

After this meeting is conducted, it is important to implement answers to those questions, back to the Preparation phase in order to learn from the attack and use it to their advantage in defending the company or organization.

---

# CSIRT and CERT Explained

With the number of cyber-attacks that happen daily, many companies and governmental bodies needed to develop a team of specialized individuals that could respond to these attacks.  
That is where the Cyber Emergency Response Team (CERT) or Cyber Security Incident Response Team (CSIRT) was introduced. Their core responsibilities are coordinating and responding to IT security incidents and determining how these incidents can impact the organization or government entity. CSIRTs often contain key stakeholders from different business units, such as; infrastructure, networking, legal and public relations, communications, security, and more, providing the CSIRT the ability to address all aspects of the company in an emergency.

### Why are they Important?

CSIRTs are important because they provide vital functions in our digital world.  For most businesses, this is divided into:

- Having a central communication point or command center where all incident information is handled.
- Promotes Security Awareness and Training (Such as Phishing Exercises) for a company.
- Act as the emergency contact group for an organization in all things related to cybersecurity.
- Investigate new security vulnerabilities and threats and develop plans to mitigate and respond to these incidents if exploited at their company.
- Determine the MTTR & MDT for a company’s assets.
- Provide useful information to other CSIRTs and the Cyber Security community.

### Public vs Private

Since the creation of CERTs and CSIRTs, a lot of confusion has surrounded how they are named.  Many organizations tend to use different names such as CERT, Security Incident Response Team (SIRT), Incident Response Team (IRT), or Computer Security Incident Response Centre (CSIRC), but they all describe an organization that has the same goals. The term CERT has often been used to describe teams in countries such as Australia (AusCERT), Brazil (CERT.br), New Zealand (CERTNZ), South Korea (KrCERT), the United Kingdom (CERT-UK), and the United States (US-CERT).  The term CSIRT is more often associated with teams that businesses adopt for internal cybersecurity breaches and are not designated as nationally recognized response teams.

## Case Study: New Zealand Cert

Since CERTs started to develop in the early 2000s, most developed countries contain some type of government-sponsored CERTs.  The goal of these CERTs is to protect businesses and individuals in their home country, as well as to help other CERTs respond to incidents where their people could be affected.  Many of these CERTs try to maintain visibility to the public and publish quarterly and annual reports on both the activity that was reported and what they have done to respond to issues.  A great example of this is the New Zealand CERT.  They publish annual reports that detail incidents that they saw for that year, as well as ways they responded to them.  Below is an example of an infographic on their website:
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4dba7c3f9660af5ddd4248fec361c212a7b3ff0e3179df9c5f1b4c7efb0ae6dd2c0c8e899b7a61eb1a58a4436ee3.png)

---

# Resources

- **Various Incident Response Resources**  
    **//** [Incident Response Consortium | The First & Only IR Community](https://www.incidentresponse.org/)

- **Incident Response Resources From Infosec Institute**  
    **//** [https://resources.infosecinstitute.com/category/incident-response-resources/](https://resources.infosecinstitute.com/category/incident-response-resources/)

- **A Curated List of Tools for Incident Response**  
    **//** [https://github.com/meirwah/awesome-incident-response](https://github.com/meirwah/awesome-incident-response)

- **Incident Response Tools by AT&T Cybersecurity**  
    **//** [https://cybersecurity.att.com/resource-center/ebook/insider-guide-to-incident-response/incident-response-tools](https://cybersecurity.att.com/resource-center/ebook/insider-guide-to-incident-response/incident-response-tools)

- **Proactive Incident Response by Secureworks**  
    **//** [https://www.secureworks.com/centers/proactive-incident-response](https://www.secureworks.com/centers/proactive-incident-response)

- **Incident Handler’s Handbook by SANS**  
    **//** [https://www.sans.org/reading-room/whitepapers/incident/paper/33901](https://www.sans.org/reading-room/whitepapers/incident/paper/33901)

- **Ultimate Guide to Cybersecurity Incident Response by TechTarget**  
    **//** [https://searchsecurity.techtarget.com/Ultimate-guide-to-incident-response-and-management](https://searchsecurity.techtarget.com/Ultimate-guide-to-incident-response-and-management)

- **A Beginners Guide to Open Source Incident Response Tools and Resources by Cybersecurity Insiders**  
    **//** [https://www.cybersecurity-insiders.com/beginners-guide-to-open-source-incident-response-tools-and-resources/](https://www.cybersecurity-insiders.com/beginners-guide-to-open-source-incident-response-tools-and-resources/)