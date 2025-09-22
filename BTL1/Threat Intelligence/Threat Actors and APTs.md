## Common Threat Agents

#### What are Threats?

As you should remember from the **Management Principles** lesson in the **Security Fundamentals** domain, a threat is a danger that can exploit a vulnerability, resulting in a breach (impact). Below is a diagram demonstrating an intentional threat.

**Intentional Threat (Hacking)**

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d561541824d27399d66e994a61ff4373550e6429cf3eb5f7f04f6444e055f15c72176ae0fc12949668ee99833f03.png)
In the example above, a malicious user is exploiting a vulnerability, which is a lack of input validation (not preventing users from entering special characters into an input field, such as “``/ - = ` '`` “) which allows the attacker to conduct a [SQL injection attack](https://www.w3schools.com/sql/sql_injection.asp), and retrieve data stored in the SQL database connected to the back-end of the vulnerable website.

- **Vulnerability:** Lack of input validation
- **Threat:** Exploiting vulnerability to write a malicious SQL query
- **Result:** Username and password tables in the database are sent to the attacker
#### What are Threat Actors?

A threat agent or threat actor in regard to cyber threat intelligence is an actor that intentionally or unintentionally generates an adverse effect on an organization, such as conducting a cyberattack or unintentionally leaking information. Therefore, this can be an individual or group of individuals that cause harm in some way.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7bafc00d70a7ef94c6d81cec18a559c0302e4bd71161d9b5fdf290e4670c5b02dd2bb2ccdca5c55cb91c3c0643b5.png)
Let’s use a new example. If a cybercrime syndicate hacked a server belonging to ABC Industries that suffered a remote code execution vulnerability and managed to steal data such as user’s email addresses, billing addresses, and passwords, the cybercrime syndicate (a group of individuals) would be the threat actor in this scenario, and they have caused an intentional threat because they purposefully exploited the vulnerability and exfiltrated the data.

But not all threat actors are evil hackers or rain clouds, and sometimes threats can materialize as a result of an accident. If an employee unintentionally deletes a table in a database because they have not received proper training, then they become a threat actor themselves, despite not having malicious intentions.

- **Threat Actor:** Employee
- **Vulnerability**: Not properly trained
- **Threat:** Employee unintentionally deleting a database table
- **Result:** Missing data means the application attached to the database will likely not function correctly
- **Threat Type:** Unintentional = Accidental
#### Actor Categorization

When we talk about threat actors, we are generally referring to the threat intelligence term associated with an individual or group of malicious actors that conduct cyber-dependant attacks or operations. We can generally categorize threat actors into the following 4 groups:

**Cyber Criminals**

This group includes hackers and crackers that are looking to make money from malicious and illegal activity, such as cyber-attacks, ransomware, and phishing. The skill level can vary dramatically within this group, for example, you could see a really experienced hacker classed as a cyber criminal threat actor, but you could also see a “script kiddie” in the same group, which is a term used to describe an inexperienced individual that is dependent on pre-built tools and scripts, and generally has a low level of technical knowledge.

**Nation-States**

These are hackers or hacking teams that work for governments around the world, and have a very high level of technical sophistication as well as resources, making them some of the most advanced adversaries out there. They typically conduct prolonged covert cyber operations, staying undetected for long periods of time whilst they silently complete any objectives they have in the target network. Nation-States are often referred to as Advanced Persistent Threats (APTs).

**Hacktivists**

Individuals or groups placed into this category are typically socially or politically motivated and use cyber attacks as a way to express their views and beliefs. Hacktivists usually conduct distributed denial of service (DDoS) attacks that take systems offline by overloading their resources causing them to crash. Another common attack conducted by actors in this group is website defacement, the act of changing the content on a website’s homepage to display a message or image created by the attack, usually to make a statement related to social or political views.

**Insider Threat**

Individuals classed into this group have intentionally or unintentionally abused their power and knowledge of an organization they work at in order to leak confidential information. Intentional cases can include disgruntled employees that are taking revenge against the company, and unintentional cases can include employees accidentally emailing documents to the wrong email address, or falling victim to a social-engineering attack.

-----
## Motivations

When we consider why people or groups conduct cyber attacks and operations, there are a number of motivations that may be involved. Motivations can typically be classed into one of four high-level categories:

- **Financial Motives**
- **Political Motives**
- **Social Motives**
- **Unknown Motives**

------
## What Are APTs?

APTs, or Advanced Persistent Threats, are one of the most feared security concerns in large organizations, institutions, or governments. 
APTs include a group of highly skilled attackers, who have a state backing or otherwise almost unrestricted access to a variety of resources.

----
## Tools, Techniques, Procedures

TTPs are the actions that threat actors take when conducting cyber attacks. They’re used by defenders to track the tactics that different threat groups use, and let us gather intelligence to aid security operations teams

[MITRE’s ATT&CK Framework](https://attack.mitre.org/techniques/enterprise/) has over 260 different techniques mapped and split into 12 different categories:

- **Initial Access**
- **Execution**
- **Persistence**
- **Privilege Escalation**
- **Defense Evasion**
- **Credential Access**
- **Discovery**
- **Lateral Movement**
- **Collection**
- **Command and Control**
- **Exfiltration**
- **Impact**
#### Example Walkthrough

Let’s go through an example. If security analysts at Organization A discover a script that is exfiltrating data, this will be mapped to a TTP. In this case, it is [T1020](https://attack.mitre.org/techniques/T1020/). Now the security analysts and incident response team can use this to work backward, identifying how the attackers gained initial access and conducted other activities such as privilege escalation and lateral movement. 
All of this information can be mapped as an attack path and used to fully understand cyberattacks, how successful cyber-attacks have occurred, and how to prevent a similar attack in the future.

Each TTP in the MITRE ATT&CK Framework also has mitigations and detection advice. If we look at this information for [T1020](https://attack.mitre.org/techniques/T1020/), we’re provided with the following:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6e903059af3d6591eb36e53a0943626a440d1a9059bc1ec17c8e90357d5b30bbbd9f888ed21685b6a616dec11198.png)

Over time, defenders are able to build up attack paths for different incidents, and this process can potentially provide attribution for certain groups. 
If security analysts at Organization A observe a threat actor following a specific TTP path, they can see if any known APTs follow the same or a similar path, and then to a reasonable degree can attribute that group to the observed attack. 
The organization can then start implementing defenses against other tactics and malware this group uses as a proactive measure.