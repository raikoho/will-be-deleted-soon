Sharing SIEM rules can be an extremely beneficial process for a security team, whether they’re sharing them or retrieving them, but SIEM rules are written in specific structures depending on the SIEM platform.

**Sigma** is a generic and open signature format that allows you to describe relevant log events in a straightforward manner. The rule format is very flexible, easy to write, and applicable to any type of log file. The main purpose of this project is to provide a structured form in which researchers or analysts can describe their detection methods and make them shareable with others.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/03977171c62b3d50167cf173c1d3e6ae0af22c65dcd9f7fab0a1174228007d410bf1be317dae0e9bd6cbb7e70e54.png)
Rules can be written in the Sigma language and then using a converter (Sigmac) they can be exported as rules in the correct format for a number of different SIEM platforms. This process can also be reversed allowing security professionals to export rules from their vendor format to Sigma format so they can be used by teams with a different SIEM.

## Which Platforms Support Sigma?

- Splunk
- QRadar
- ArcSight
- Elasticsearch (Elastalert, Query strings, DSL, Watcher, & Kibana)
- Logpoint

## Benefits of Using Sigma

- Describe your detection method in Sigma to make it sharable
- Write your SIEM searches in Sigma to avoid vendor lock-in (meaning you can flexibly change the SIEM solution without having to lose all of your custom rules)
- Share the signature in the appendix of your analysis or research report along with IOCs and YARA rules to allow others to replicate your work and build detection rules
- Share the signature in threat intel communities (ISACs) – e.g. via MISP (which we covered in the Threat Intel domain!)

## SIGMA Rule Example

In this example we’re looking at a Sigma rule that can detect when a web server has been compromised and is running a web shell, allowing a malicious actor to visit a specific URL which will provide them with a console, allowing them to execute commands as if they are on the server. We’ll break down the rule below, even though it’s really human-readable!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/33cb6db6d749401c108735754ea81e60f009a6f6cb4486e17dd1cf18b4b86736fd93c8c11198ef70851c6f0aca14.png)

  
On line 6 we can see that the ‘detection’ is declared, stating how this rule works. Line 7 states it is using the method of matching keywords against a URL string (mentioned on Line 2).

So if this rule was actively being used to monitor a web server and we had a web shell running on **https://example.com/13919595/asjkdasjdkasjvn/shell.php?** , and we visited the interface and tried to use the command ‘`whoami`’ this would be included in a GET HTTP request to the web server, meaning the URL will be changed to include ‘=**whoami**’. This activity would generate an alert for the security team to investigate, making them aware of the web shell. It is extremely unlikely that a normal visitor would ever need to include these operating system commands in a GET URL request so there is a low rate of false positives (but some scenarios are covered on lines 13 and 14).

There are some great real-world rules to take a look at on Florian Roth’s Github page [GitHub – Neo23x0/sigma: Generic Signature Format for SIEM Systems](https://github.com/Neo23x0/sigma). Additional rules are available at [https://github.com/SigmaHQ/sigma/tree/master/rules](https://github.com/SigmaHQ/sigma/tree/master/rules). We highly recommend taking a look at these to better understand how they function.

---

# Writing Sigma Rules

First, you’ll need to go [download the Sigma master ZIP file from the Github](https://github.com/SigmaHQ/sigma):

**Disclaimer:** Your AV solution will possibly flag this file as malware due to it containing malicious strings/commands, so the Sigma rules can detect that activity. Disregard.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0a52cc9ca27bf063b29c5c1d3142a286242114261a4bafa5648680379102c7990fb4ebfb67bbb85b876f94c04ece.png)

Once you have the .ZIP file we need to extract the contents. To make things easier create a folder on your Desktop called ‘BTL1-SIGMA’, move the downloaded ZIP file to this folder, then extract it.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8e01fa2cbe0393bd7447bc795c342f280f6cac7f5cd08f9b258b8df534ff9782ec13f876c2a6833db65bf890bc2a.png)

Open the ‘rules’ folder – we’re presented with a number of sub-folders that contain some basic rules:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/002b12c46f92f32a1c55e787ef650aaf351270b6275a7c2ce24bba79ed04e55efab7e1585464703f64f476c41b3a.png)

Now go into the ‘unsupported\network folder’ and then open **net_dns_c2_detection.yml** in Sublime Text 2 (or your text editor of choice):
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0ece554701bed77bfb768b549ba15e5937835e31e0ee03c0ed50dedf3be0d77eba495c6440c61e685d39f4a6a2e2.png)

Before we start customing this rule to suit our own needs, let’s recap exactly what this rule is doing and how it’s formatted. Take note of the different rows explained below, as you’ll be editing some of these very soon!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d97132c3bbe6159245a025b0212ac1cc8ffcce7bc16330d3c0fa40dfff2d59fd4c0ac724f92642752d2ff54fcda7.png)

1. `title` is a custom descriptive value that is used to provide a very brief explanation of what the rule is looking for.
2. `id` is used as a unique identifier for this rule.
3. `status` is a custom descriptive value used to explain the state of the rule. Some examples could include ‘incomplete’, ‘experimental’, or ‘production’.
4. `description` is a custom descriptive value used to provide a more detailed explanation of what the rule is trying to detect and how.
5. See above.
6. `author` is a custom value used to hold the author(s) of this SIGMA rule.
7. `date` is a custom value used to hold the date the rule was first created.
8. `modified` is a custom value used to hold the date when the rule was last edited by an author.
9. `references` is a custom list that holds URLs that help to explain what the rule is trying to detect
10. see above (9)
11. see above (9)
12. `logsource` is used to explain what logs are required in the SIEM for the rule to function
13. the `logsource category` is dns, showing that the security team will need to be pulling dns logs into their SIEM for the rule to work
14. `detection` explains the logic behind the rule including conditions that, when met, can generate an alert.
15. `selection` states that something must be selected from the DNS logs. In this case it’s the parent domain (or root domain, such as Google.com).
16. `parent_domain` states the log field that should be selected. The * asterisk symbol represents a ‘wildcard’ meaning that any value can be used. This means that ANY domain should be selected.
17. `condition` states the actual detection logic. For this rule it will retrieve all parent_domain values and count the number of queries to that domain. If the count is over 1000 (> 1000 meaning greater than 1000) then it will alert.
18. `falsepositives` is a custom list that states how false positives could occur.
19. `falsepositives 2` – The author explains that legitimate software that uses dns to transfer data would generate an alert, even though it is not malicious activity.
20. `level` is a custom descriptive value that in this rule appears to be stating how urgent this alert should be.
21. `tags` is a custom list that includes different MITRE ATT&CK techniques that can be detected using this rule.

So, we know that this rule is used to detect potential [DNS tunneling](https://attack.mitre.org/techniques/T1071/004/) for command-and-control communication by looking for a large number of queries to domains, and will alert when 1001 or more requests have been observed by looking at DNS logs.

Now it’s your turn to make some changes, allowing us to detect some specific activity. Read the intelligence briefing below and try to make changes to this existing rule file to reflect the information provided.

## Intelligence Briefing

We’ve recently observed a new type of malware that we have named ‘TRANSPORTER’ which uses DNS tunneling to provide a command-and-control channel across the internet, allowing an attacker to send commands to infected systems. As DNS traffic is extremely common in environments this traffic blends in and does not immediately look suspicious. DNS packets contain many fields and headers in which data can be concealed.

At the time of writing, we have only observed one domain name that is being used to send and receive C2 traffic, which we have included below. Speaking with one victim we observed that their SIEM did not detect this activity as they were not monitoring for excessive DNS queries to domains.

**Domain Name:** redhunt.net  
**Average Number of Requests:** 500  
**MITRE ATT&CK Techniques Used:** T1071.004 (Application Layer Protocol: DNS)

**Tips**

- You can remove the ‘id’ and ‘modified’ lines from the existing rule as they are not required.
- Use the ‘title’ and ‘description’ lines to include information from the above intel briefing.
- Consider the average number of requests, we should alert on something that is lower than this to catch any infections where the traffic count falls below this average.