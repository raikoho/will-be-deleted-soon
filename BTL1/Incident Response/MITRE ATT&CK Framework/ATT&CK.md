The [MITRE ATT&CK™ framework](https://attack.mitre.org/matrices/enterprise/) is a comprehensive collection of tactics and techniques used by adversaries, which can be utilized by both blue and red team members to improve the security posture of an organization. Below we will cover some applications for defensive and offensive purposes.

**FOR DEFENSIVE ROLES**

- By looking at each tactic and technique within the framework, defenders can work out which areas they have good visibility over, and areas that they don’t. They can then work to improve visibility and detection capabilities by writing rules or alerts that will trigger on suspicious or malicious activity (a good tool for this is [ATT&CK Navigator](https://mitre-attack.github.io/attack-navigator/enterprise/), which you’ll be using later!).
- Threat hunters can also use these tactics and techniques to proactively hunt for malicious activity inside the network, working to discover and stop covert or unknown threats.

**FOR OFFENSIVE ROLES**

- Adversary emulation is the process of performing a penetration test or red team exercise while copying the tactics and techniques of a threat actor that is likely to target the organization. For example, if we work for a telecommunications company, then [APT 19](https://attack.mitre.org/groups/G0073/) may want to target us, as they have attacked organizations in the same industry before. We could task our offensive security team with attacking the organization, but copying the techniques used by APT 19. This will allow the blue team to test their detection capability, and if there are any blind spots the red team will report on this so they can be addressed.

The following lessons will introduce you to the 12 stages in the ATT&CK framework, so that you can feel more confident mapping cyberattacks to these steps, and improve your understanding of tactics and techniques used by adversaries during cyber operations. We will also provide further reading material if you wish to learn more about this framework, and we’ll also include links to MITRE’s own training courses.