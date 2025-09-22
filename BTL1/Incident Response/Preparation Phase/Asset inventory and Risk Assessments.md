If we want to protect systems, we need to know what assets our organization actually has, so keeping an up-to-date asset inventory can help to monitor production systems, test environments, and other devices that fall under our protection.

Whilst we would ideally protect all systems, sometimes it is not cost-efficient to protect certain assets, and that’s where risk assessments come in. Using them, we can identify systems that are of high value to the business, and therefore require more protection than others. This is a huge part of incident response – if multiple incidents occur at the same time, it needs to be clear which incident has priority, and whether the response needs to be immediate or can be delayed.

If a security function is unsure of risk to different systems and assets, a good place to start is by looking at the Business Impact Plan and Business Continuity Plan, both of which should clearly outline the critical systems for business operations.

---

# Asset Inventory

There's a common saying in cybersecurity - you can't protect what you can't see. This means that if we're not aware of a system within an organization, we can't take steps to protect or monitor it, because we haven't been told it exists.

An asset inventory is a centralized and updated list of all IT assets within an organization. This typically includes:

- Desktops/Laptops
- Servers
- Printers
- Internet-of-Things Devices (IoT) (such as heaters, TVs, alarms, vending machines, and anything else network connected)
- Network Devices (firewalls, switches, routers, load balancers)
- Mobile Devices (phones, tablets)

Other names for an asset inventory include a ‘computer management database’, or ‘CMDB’.

The purpose of this practice is to store key information associated with a device, such as a system owner, the operating system version, the software installed, what IP address it's using (if it is assigned a static IP address), and more. This allows IT teams to manage assets, track what systems need to be updated, and assist with technical support.

For Security teams, this can help us with a number of exercises:

- Identify out-of-date operating systems without using a vulnerability management solution. We can simply look at the OS version details to identify systems running old versions, such as Windows 7 or older versions of Windows Server.
- If we have an incident or security event and we have a list of affected internal IP addresses, we can find the appropriate system owners or contacts using the asset inventory.
- If we have a system that is acting suspiciously but we're not sure what the purpose of the system is, and importantly, what type of data is stored on this system (such as confidential or non-confidential) then we could check the asset inventory to understand what team looks after this device, and what it's used for.

---

# Risk Assessments

A risk assessment works to determine the systems that are the most critical to the business, therefore the most valuable. More protection and priority need to be given to these systems, especially if two incidents occur at the same time, prioritization needs to be clear so that time and resources are focused in the right place.

When risks are identified (such as an internet-facing system, an unpatched system, or a business-critical system) appropriate measures should be taken to properly defend it, but only equal to the amount of risk. There’s no point in spending £100,000 on security controls for a server that isn’t used for anything and isn’t facing the internet. By determining risk, the right amount of resources can be given to protect that system. As we covered at the start of the course, there are four approaches to risk:

- Transfer the risk (such as purchasing insurance)
- Accept the risk (a decision that is made to not spend any resources as the impact would be low and the cost too high)
- Mitigate the risk (apply security and other controls to protect the asset and reduce the risk)
- Avoid the risk (an asset that is at too high a risk may simply be taken offline so it can’t be exploited)