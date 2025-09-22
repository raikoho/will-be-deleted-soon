
This section of the Incident Response domain will cover how to contain an incident to prevent it from affecting additional assets, collecting digital evidence, removing any malicious artifacts such as backdoors, addressing any issues that led to the incident occurring, as well as fixing damage that occurred during the attack.

---
# Incident Containment

Depending on the type of incident, there are several responses we can take to contain the incident, preventing it from spreading to additional systems and potentially causing more damage. This lesson will cover actions that can be taken, along with any negative consequences that could occur. By definition, Incident containment is a function that assists to limit and prevent further damage from happening along with ensuring that there is no destruction of forensic evidence that may be needed for legal actions against the attackers later.

# What is Containment?

Usually, organizations think of Containment as a step during the Incident Response process. But in our opinion, Incident containment should be a Strategy. Once a containment strategy is defined, the respective tools & technologies can be selected to participate in the fulfillment of the strategy. Containment strategies can be defined based on the focus area in the IT Infrastructure. It can be at the perimeter, the demilitarized zone, internal networks, or at the endpoint, or a combination of any of the above. The containment strategy will not be the same for every company as it depends on the systems and tools you are using, so it must be tailored to your environment. We will provide you with a list a few examples of such containment strategies below.

## Short-Term Containment

Typically short-term containment is break-fix or quick heal. The objective of the short-term containment is to prevent the asset or the user from causing further damage to the organization**.** Depending on the tools being used by the organization, there are different methods to contain an incident, but these will vary dramatically based on what activity is actually happening. Let's go through a few examples:

- If an Active Directory (AD) account is compromised and is trying to log into every system it possibly can (**security incident**), and is successfully accessing some systems, then the account can be disabled in AD and the attacker can no longer use this user account (**containment**).
- If an employee has accidentally downloaded malware to their corporate laptop (**security incident**), then we can use security tools to isolate the device and prevent any inbound or outbound connections, preventing it from connecting to other systems, exfiltrating data, or allowing the attacker to take remote control (**containment**).
- If periodic connections are found from internal servers to a known command-and-control server IP address (**security incident**), the remote IP can be blocked on the perimeter firewalls to prevent any further communications going outbound or coming inbound from the C2 IP (**containment**).
- If web attacks are being observed against the company's website (**security incident**), and all traffic shares a commonality (such as source IP or IP range, user-agent, headers), it can be blocked using a Web Application Firewall (WAF) on a device between the attack and the website server (**containment**).

However, it is important to note that this does not fix the real reason an incident happens. It also does not stop an incident from recurring on a different asset in the organization. This is where long-term containment comes into play.

## Long-Term Containment

Long-term containment is an enterprise-wide fix that is a step short of complete remediation of an incident. At this stage of the remediation process, the organization has identified the cause of the incident and is working to address it, so that similar incidents don't occur in the future (or at least we try to reduce the likelihood and impact of them). Some examples of long-term containment steps can include changing how internal networks are structured so that systems are better segmented from each other to prevent lateral movement and allow for better containment and isolation strategies with less impact on other systems. Other examples include:

- Patching vulnerabilities that may have been exploited by updating software or firmware, or making configuration changes
- Implementing new security tools to aid in the prevention of incidents, such as a new email gateway with security features, a better anti-virus solution, or a network intrusion detection system
- Reviewing all accounts to ensure they only have the appropriate level of permissions (Principle of Least Privilege)

## Containment Measures

**Perimeter Containment**

- Block inbound traffic and outbound traffic.
- IDS/IPS Filters to identify further malicious traffic and take automated actions, such as blocking active connections.
- Web Application Firewall policies, to detect and take action against web attacks.
- Null route DNS, to prevent DNS resolutions so internal hosts cannot find the IP address of a given domain name and establish a connection.

**Network Containment**

- Switch-based VLAN isolation, to restrict network access.
- Router-based segment isolation, to restrict network access.
- Port blocking, to prevent connections on specific ports.
- IP or MAC Address blocking, to restrict network access.
- Access Control Lists (ACLs), to provide rules that restrict what hosts on the network can and cannot do.

**Endpoint Containment**

- Disconnecting the infected system from any network connections (turning WiFi off, pulling ethernet cable).
- Powering off the infected system.
- Blocking rules in the local firewall.
- Host intrusion prevention system (HIPS) actions, such as device isolation.
## Has it Been Effective?

Now that you have a validated Incident Containment strategy, the next step is to ensure that your strategy was effective against the Attack Vector. This is where monitoring of the Attack Vector, Targeted Victims, Outbound Traffic from the victims, etc. become important measures of effectiveness. One way to achieve this would be to implement containment actions to prevent a compromised system from connecting outbound to the internet. We could create a rule in the SIEM that looks for any connections from the compromised system to any non-internal system. This rule could generate alerts named “On-going Incident 5537, Containment Verification, Immediate Escalation”, and SOC analysts can be informed to immediately contact the incident response team if an alert is generated because this should be impossible due to the containment measures.