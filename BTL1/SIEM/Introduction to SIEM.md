**Security Information Management,** also known as **SIM** is specialized security software that helps with the collection, monitoring, and analysis of data and event logs generated from all security devices in a network (IDS, IPS, Antivirus Software, Firewalls). 

Facilitating the task of the investigators and the security team of an organization by centralizing all this information in a single service.

## What Does SIM Do?

SIMs are mainly concerned with the collection and translation of information relating to the operation of a network. 
These elements collect data and logs from devices within an organization, and may even collect information from some devices or sources outside the organization (such as public threat identification services and correlation networks), looking for patterns that will allow the system to understand the activity, operation and behavior of these devices, and then make reports, graphs and charts that will be presented to the user. Some of the actions performed by a SIM are:

- **Monitoring of events in real-time.**
- **Sending and generating alerts and reports.**
- **Automatic response to incidents.**
- **Correlation of data from multiple sources to improve the quality of the information presented.**
- **Translation of event logs from different resources through XML files.**

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/156e333389c9e8c20566023ee01d3e5e43fd6ce76d19ca7085a9d9c1587c54acf54fd32c74a920e81644df3b3094.png)
## Advantages and Disadvantages

SIMs are services that bring many benefits to the users who implement them in their organizations, some of which are:

- _**Easy to deploy.**_
- _**They can store and analyze large volumes of data.**_
- _**They allow a fast and efficient analysis of all events in a system.**_
- _**They correlate logs and events to provide the most accurate overview of the system.**_
- _**They allow for easy threat management (assessment, containment, and analysis)**_

However, it is always important to mention some disadvantages that may affect users who want to apply this type of solution to their network:

- _**They can be very expensive tools.**_
- _**It is not completely certain that they can be properly adapted to the working environment.**_
- _**Some providers do not provide full technical support for this type of service.**_

---
## Benefits of a SIEM

**Advanced Threat Detection:** Malware has evolved in a way that eludes detection by traditional antivirus solutions, firewalls, intrusion detection and prevention systems, and other security solutions. Many organizations have implemented a defense-in-depth strategy around their network security solutions, hence generating a huge amount of data, which is difficult to monitor. As a result, a new type of security solution called advanced threat detection has emerged. SIEMs are capable of continuous real-time monitoring and correlation across the breadth and depth of the enterprise; therefore can help detect, mitigate, and prevent advanced threats such as malicious insiders and data exfiltration.

**Forensics and Incident Response:** A forensics investigation can be a long process because a forensics analyst must interpret log data to determine what happened and also preserve the data in a way that makes it admissible in a court of law. SIEMs can help organizations in a forensics investigation by storing and protecting historical logs and providing tools to quickly navigate and correlate the data. SIEMs can help security analysts realize that a security incident is taking place and set immediate steps for remediation.

**Compliance Reporting and Auditing:** Primarily, SIEM is implemented in response to governmental compliance requirements. Every business is bound by some sort of regulation such as HIPAA, PCI/DSS, SOX, FERPA, and HITECH. SIEMs can help organizations prove to auditors and regulators that certain requirements are being met. SIEM aggregates log data from across the organization and presents it in an audit-ready format.

**Other reasons why businesses need SIEM include:** data storage, gaining and maintaining certifications (such as ISO 27000, ISO 27001, ISO 27002, and ISO 27003), log management and retention, case management, or ticketing systems, and policy enforcement validation and policy violations.

---
## SIEM Platforms

### Graylog

[**https://www.graylog.org/**](https://www.graylog.org/)

Graylog offers two different SIEM products, Graylog Open Source which is 100% free, and their paid-for product, Graylog Enterprise. If you want to download and play around with Graylog Open Source you can download it [here](https://www.graylog.org/downloads#open-source). Graylog Enterprise has a free limit and can be used by small organizations (less than 50 staff) that process less than 2 GB worth of events per day. Below is a screenshot of a search page within Graylog, giving you an idea of how the platform looks.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e526a3616c934209684806581f6703d6157b96d565734d32e92807f84ca94f13ddda3ca0a17229550fe1c27801e0.png)

---

### Arcsight

[**https://www.microfocus.com/en-us/products/siem-security-information-event-management/overview**](https://www.microfocus.com/en-us/products/siem-security-information-event-management/overview)

ArcSight (with their SIEM ArchSight, also referred to as ArcSight Enterprise Security Management or ESM) states that it can help SOCs to build out a layered analytics approach by integrating with a wide range of commercial security tools, and offers Security Automation and Response (SOAR) workflows to provide an automated response to security events, leaving analysts to focus on more important investigations. Powerful real-time correlation within ArcSight claims to be the fastest way to detect threats from large datasets.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e175bd864c911a8eee8e4d99e8848b2d7cfa133181f64579f534c43a66cbf267befe1bebf15563547c61599b112a.jpg)

---

### QRadar

[**https://www.ibm.com/uk-en/security/security-intelligence/qradar**](https://www.ibm.com/uk-en/security/security-intelligence/qradar)

In addition to basic SIEM capabilities, QRadar SIEM also offers the ability to import data from threat intelligence feeds. When purchasing QRadar, clients can also opt-in to subscribe to the paid-for IBM Security X-Force Threat Intelligence, which identifies malicious indicators, which can be used to provide investigation enrichment, or for immediate alerting. Additional modules exist for QRadar that can assist security teams with incident response, risk management, and vulnerability management.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/12bfa937c42433ecd4dd1652cf79134e2176234995b2258e61d35f68e2a2bb61c4ff9687dc461b073896e9c98d9d.png)

---

### LogRhythm

[**https://logrhythm.com**](https://logrhythm.com/)

LogRyhthm boasts some pretty impressive features, such as machine learning, Security Automation and Response (SOAR), End-Used Behavioural Analytics (UEBA), and Network Detection and Response (NDR) to give unmatched environment visibility and response capabilities, directly from the SIEM platform. LogRhythm also states that _“you’ll easily baseline your security operations program and track your gains — so you can easily report your successes to your board”_, which does indeed sound like a useful and efficient way to generate metrics and prove to executives that we really do protect the business, every single day.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6e5f4e82c0ec7f9fd4921985af46d53d74220c8ced8b6b3d40694bb41ba372b64ab0f57885b8651bca7a3bb15797.jpg)

---

### Splunk

[**https://www.splunk.com/en_us/platform.html**](https://www.splunk.com/en_us/platform.html)

Splunk is one of the most popular SIEM platforms in the industry. SIEM administrators can download and add “Apps” that provide additional functionality to Splunk, such as analytics, dashboards, improved searching, and data manipulation. Imported data can be searched using custom-written search queries, which can also be used to generate alerts, and create visual dashboards.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6c4866fcec5f7cad7ae59d427654b4c97c81ff1f2cc20b6deffca34ef4aff481d11d2841e1ed9185394f1bb1a790.png)