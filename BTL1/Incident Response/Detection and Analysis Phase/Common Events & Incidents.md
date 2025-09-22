The events we will cover are:

- **Remote to Local Scanning**
- **Remote to Local DoS/DDoS**
- **Local to Local Scanning**
- **Login Failures**

Before we jump into these security events, we want to explain what is meant by “remote to local”, “local to remote” and “local to local”. When considering an organization's private network, we use the term internal, as it is inside the organization. Anything outside of the organization, such as websites not hosted by the company and public IP addresses, is referred to as external, or remote.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7e8b6686f1a9fd45f10cd7acb44d865739968ca98edea9b477db425f604985bdb64f0113bd3d70149b8c58522e07.png)

So any activity that occurs between two systems within a private network is **local to local**, while activity from an external IP address towards a public IP address owned by the organization would be **remote to local**. Throughout the rest of this lesson we will be using the abbreviations:

- **R2L – Remote to Local**
- **L2R – Local to Remote**
- **L2L – Local to Local**

# R2L Port Scanning

With this activity, an external public IP address is scanning the public IP addresses owned by the organization. This is typically conducted to see what IP addresses are used by the organization, which of them are in use, and what ports are open. This type of activity is likely to happen all day, every day, and is arguably the most common alert analysts will see, depending on how the specific organization monitors this activity.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/91cbfe6cad2b6b28b1859eeb1dc9514aed209a2103d70d9962be2a9339d9b4a23e3612bd295a3bad8c329f3e18fe.png)

In the simplified diagram above, we have shown how a system present on the internet is able to perform a port scan against systems in the DMZ by going through a list of public IPs that are owned by the organization. The red lines represent the system sending a request to an IP address on a specific port, and the blue lines represent a response from the system (provided there is an active system on that IP).

## **Detection**

For this, we would want to collect logs from perimeter firewalls and web application firewalls. The rule would look for multiple connections within a small timeframe to a number of different ports on the system. Typically, web servers should only ever be contacted on ports 80 (http) and 443 (https). A remote system that starts connecting on 93, 1195, 1959, and other random non-standard ports is most likely scanning or fingerprinting the system.

## **Potential Impact**

Scanning happens all the time, and there is rarely an immediate impact. Older systems could be affected by scanning if there is no scalability, and the actor is performing an intense scan. This could potentially use up a lot of bandwidth and lead to other systems not being able to connect to it, causing a denial-of-service (DoS).

---

# R2L DOS/DDoS

With this activity, one (DoS) or more (DDoS) external IP addresses are sending a high volume of requests or malformed packets to a target system in an attempt to crash it.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a1bddb8b25cdef82ddda24975bc88347fd0ef87127f086d1ee6b5b5d9c9e3ee5014f65280956bfdd91a50eea92a4.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f7589f133f66a6ce4f6630c968bc663171cefc46067bbd690bc6f2fec9a12a3d22659bf27889e9d575f5fdea6f49.png)

The diagram on the left shows an R2L denial of service attack, where one IP is attempting to send more packets to the target system than it can process, causing it to crash, preventing legitimate traffic from reaching it, resulting in a denial of service.

The diagram on the right shows an R2L distributed denial of service attack, where multiple IPs are attempting to crash or consume the target system’s resources so that it can’t process legitimate requests, resulting in a denial of service.

## **Detection**

We can use rules that monitor the number of requests the systems in the DMZ receive. Establish a baseline for the levels of “normal” traffic that is expected to be received by these systems, and create a rule that will generate an alert when a threshold higher than the baseline is observed.

## **Potential Impact**

Denial of service attacks, while dependent on a number of factors, have the potential to take systems offline. This can result in loss of customer trust, a decline in sales, and potentially even damage to the affected system. Let’s go through an example; if Organisation A is an online retailer and their website is hit by a DDoS attack and it goes offline, customers will be unable to place orders, resulting in lost sales. Customers who hear how the site has been “attacked”, without proper context and knowledge of cybersecurity may believe the site has been hacked, and take their business elsewhere. In 2016 a DDoS attack was launched against Dyn, a DNS provider. This led to organizations that used Dyn to also go offline, as users that attempted to visit the sites were unable to resolve the IP address from the domain name. This attack affected companies such as Amazon, BBC, PayPal, Reddit, and Twitter. You can read more about this high-profile DDoS attack [here](https://en.wikipedia.org/wiki/2016_Dyn_cyberattack).

---

# L2L Scanning

With this activity, an internal private IP address is scanning another, or multiple, private IP addresses.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9c6e0240f481bf6a59183a068def99f703fcce662c7e19b381a9ad641fa5be8fd77bf84e910849f977ff0c118138.png)

In the simplified diagram above, we have shown how a system within the private network is scanning other systems on the same network, sending out requests and receiving replies, using these to determine what systems are active and perform fingerprinting activities to identify the operating system and any running services on other hosts.

## **Detection**

SIEM rules can be configured to generate alerts when one private IP is making rapid connections to other internal private IPs. Thresholds or patterns should be used to prevent false positives, as internal systems will make legitimate connections to each other, but it is highly unlikely internal systems should be port scanning or fingerprinting each other! Internal vulnerability scanners should be whitelisted from any L2L scanning rules, as if the security team starts an internal vulnerability scan, the SIEM will generate an alert as the scanner begins scanning other internal systems.

## **Potential Impact**

If an internal system has been compromised, the likely next step for an attacker once persistence has been achieved would be to identify other systems in the same network so they can perform lateral movement – the process of moving from one system to another. They will identify other systems by conducting scans using ARP, UDP, TCP, or ICMP to see what other IPs are in use, and what ports and services are running on them, looking for a way into the machine.

---

# Login Failures

There are three typical reasons this activity occurs;

1. A user has had their password reset routinely and has forgotten their new password.
2. A user has simply forgotten their current password and entered it in wrong multiple times.
3. A malicious actor is attempting to gain unauthorized access to a user account, and has incorrectly guessed the password.

Luckily in Windows Active Directory domains, we can get useful information from the domain controller, giving us context to the login failures. Within the login failure event, [Windows Security Log Event ID 4625](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/event.aspx?eventID=4625#fields), there is a field for “failure information” which will contain one of the following codes:

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e5e72a49050655d9f7a71a23b2fe6689caf91362ff4b9cf229a5109940943605b44c893d05f5fdc8d7a53971d6a5.png)

These codes give us tons of useful information, so we can recognize why the login actually failed. For example, if we had an alert for multiple login failures, and we saw the status code 0xC0000071, we know that the login has failed because the password has expired and needs to be reset. If we had another SIEM alert with the status code 0xC0000064 then we know that someone is trying to login with a username that doesn’t actually exist.

## **Detection**

In a Windows environment, we can monitor Windows Security Log Event ID 4625, and set thresholds to detect multiple login failures against the domain controller for the same username. Analysts will then be able to investigate by looking at the status code from the security log and take actions based on the alerting activity. [Password spraying attacks](https://doubleoctopus.com/security-wiki/threats-and-tools/password-spraying/) can also be detected by monitoring for a small number of login failures (2/3) for a large number of users within a short period of time.

## **Potential Impact**

Users that are locked out can’t work, resulting in a decline in productivity. Typically users will call up or visit their IT service desk to get the account unlocked, so it isn’t a major issue and is typically resolved very quickly. However, login failures where the username is not recognized (0xC0000064) or the account is locked out because of too many failed logins (0xC00000234) could be signs of an attacker that is trying to gain access to internal accounts using a username and password wordlist, employing a [dictionary attack](https://www.techrepublic.com/article/brute-force-and-dictionary-attacks-a-cheat-sheet/), acting as an indicator that an internal system has been compromised.