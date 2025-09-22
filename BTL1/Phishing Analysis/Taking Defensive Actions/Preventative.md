## Marking External Emails

It means to whenever someone receive an email - it will be market or user can this that this email can be malicious, because it alerted by created rules formarly.

Employees must understand the risk of external emails. 
In platforms such as Microsoft Exchange or Office365, there is the ability to alter the subject line or body text of an email address that is coming into the organization to alert the recipient that this email isn’t an internal communication, and could potentially be malicious. 
This simple warning can make employees think twice about interacting with an external email, such as opening an attachment or clicking on a hyperlink.

A good idea is to apply a rule where any email coming from an external sender into the organization has the subject line appended with a very short message, such as “[EXTERNAL]” or “[EXT]”.

----
## Email Security Technology

The technologies we will cover are **SPF**, **DKIM**, and **DMARC**. 
#### SPF Records

A Sender Policy Framework (SPF) record is a type of DNS (TXT) record that can help prevent an email address from being forged.  This record is established to identify the hostnames or IP addresses that are allowed to send emails for your custom domain.  When having an SPF record specified on your domain, helps prevent a malicious actor from spoofing your domain. The SPF TXT record contains three parts: the declaration of the record type, the IP addresses and external domains that can send on your domain’s behalf, and an enforcement rule.

**The basic syntax of the record is:**

`v=spf1 <IP> <enforcement rule>`

For example, **securityblue.team** has the following SPF record:

`v=spf1 a: include:mailgun.org protection.outlook.com -all`

We can see that the record declares that it’s an SPF record, that it allows mail to be sent from mailgun.org and protection.outlook.com, and the -all specifies that the email will show a **hard fail** if the domain is spoofed by an unauthorized sender.
#### DKIM Records

Domain Keys Identified Mail (DKIM) is a method of email authentication that cryptographically verifies if an email has been sent by its trusted servers and hasn’t been tampered with during transmission.  The way that DKIM works is that when the mail server sends an email, an encrypted hash of the email contents is generated using a private key and then it adds this hash to the email header as a DKIM signature.  The receiving server will be able to verify whether the email contents have not been tampered with by looking up the corresponding public key in the domain's DNS records.  Once the receiving mail server decrypts the email with the public key, it calculates a new hash and verifies whether the original and the newly generated hash match to ensure email message integrity.

**The basic syntax of the record is:**

`V=DKIM1 <key type> <public key>`
#### DMARC Records

Domain-based Message Authentication, Reporting & Conformance (DMARC) is an email authentication, policy, and reporting protocol.  DMARC is built largely off of concepts taken from SPF and DKIM, but it adds several improvements to those protocols.  This type of record allows the domain owner to specify what should happen if emails fail both SPF and DKIM checks.  There are three basic options that the mail server can take: none, quarantine, and reject.

**The basic syntax of the record is:**

`v=DMARC1 <action> <report address>`

For example, **securityblue.team** could have the following DMARC record:

`v=DMARC1; p=quarantine; rua=mailto:contact@securityblue.team`

We can see that the record declares that it’s a DMARC record, that it sets emails to go to the quarantine/spam folder when failing both checks, and that aggregate reports are sent to [contact@securityblue.team](mailto:contact@securityblue.team) of emails that have failed DMARC.

---
## Spam Filter

To prevent these kinds of messages from being delivered into email systems' inboxes, spam filters were created. There are hundreds, if not thousands of spam filters used throughout the world and these are used in conjunction with existing email services or are built into services such as Gmail and Outlook.  
These filters use rulesets, algorithms, machine learning, community interaction, and a variety of other techniques to determine what emails are spam, and what emails are legitimately meant for the receiver.

#### Types of Spam Filters

Since each vendor/email service uses different kinds of spam filters, these can be broadly classified by the way they detect spam:

**Content Filters**

A content filter is the classic depiction of a spam filter and uses information in the email header and body to try to determine whether the email is legitimate or spam.  
When looking at the header, the filter could cross-reference the header with published blacklists or known spamming networks and automatically classify it as spam. 
When this filter scans the body of the message it could, for example, look for adult-oriented content and determine that as spam, based on preferences set on the account.

**Rule-Based Filters**

A rule-based filter allows for emails to be filtered based on predetermined criteria.  A good example of this is Mail Flow rules in Microsoft Exchange where you could say:

_If the subject or body contains “FREE OFFER” and the Sender is located Outside of the Organization, raise the likelihood of the message being spam_

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b2b0d9e987838a577591154b671407126ca0478f66069347bcf0e1ac69ba36b63550cb18b21d07b8c9fd310503d4.png)

## **Bayesian Filters**

Bayesian filters have become one of the most intelligent types of spam filters that can be used. This is because it can often utilize concepts such as machine learning, to learn the users’ spam preferences. 
For example, when the user marks an email as spam, it can analyze the characteristics of that message and use that information to block similar messages from going to the inbox. One slight downside to this kind of filter, however, is that it can often require a large amount of spam to efficiently utilize the machine learning capabilities.

While there are many other kinds of filters, the three listed above are some of the most widely used. One important thing to note about spam filters is that they need to be configured correctly to work properly. If the individual maintaining a Bayesian filter flags legitimate email, then the system will start classifying legitimate email as spam. It is important to maintain proper configurations and provide user training on what should and shouldn’t be considered spam.

---
## Attachment Filtering

The most obvious file types that are used for malicious activity are:

- **.exe** (Executable)
- **.vbs** (Visual Basic Script)
- **.js** (JavaScript)
- **.iso** (Optical Disk Image)
- **.bat** (Windows Batch File)
- **.ps/.ps1** (PowerShell Scripts)
- **.htm/.html** (Web Pages / Hypertext Markup Language)

Typically businesses will use and send the following file formats via email, which can also be used for malicious purposes:

- **.zip** (Archive)
- **.doc/.docx/.docm** (Document file, often for Microsoft Word)
- **.pdf** (Portable Document Format)
- **.xls/.xlsx/.xlsm** (Spreadsheet file, often for Microsoft Excel)

Email gateways and email security tools will often allow for different actions to be taken once a certain attachment has been identified, such as scanning it for malicious indicators, blocking the email from being delivered, quarantining the email, stripping the attachment, alerting the email gateway administrator, sending an email to specific recipients about the activity (such as the security team), or generating logs which can be ingested by a SIEM platform and used to generate an alert for security analysts to investigate.

---

## Attachment Sandboxing

Emails that include file attachments are extracted and analyzed, and files are detonated (run) in a virtual environment, where everything is monitored to actually see what happens when a file is executed. 
If any malicious indicators are observed, such as trying to download additional files from a malicious domain or trying to create or alter existing processes, the attachment is classed as malicious, and the email will not be delivered.

**Some advanced sandboxing products will provide functionality such as:**

- Machine learning can develop its understanding of malicious indicators by retrieving information and behavioral analytics from millions of malicious emails and malware samples so that over time it can determine which emails to let through, and which to stop.
- Virtual environments that can scale to meet the analysis requirements of constantly changing the volume of incoming emails.
- Sandbox reports detailing exactly what the attachment attempted to do so that security teams can implement defenses in case any manage to get through or share intelligence with organizations that don’t utilize attachment sandboxing.

---
## Security Awareness Training

It is **crucial** for organizations to take phishing seriously, and to ensure that they run routine user awareness training sessions so that anyone can detect and report a suspicious email when they see one. There are two main ways to educate users on the importance of phishing, and how to quickly identify it.

#### Awareness Training

Preferably during the onboarding process (where a new employee joins a company), users should be put through either an in-person or an online training course that teaches them how to spot phishing emails, and the actions they should take (generally reporting them to the security team). This should cover identifiers of a phishing email such as:

- **Coming from an unknown sending address**.
- **Improper grammar and spelling mistakes**.
- **Poor styling**.
- **Trying to get the recipient to click on a button or complete an action**.
- **Suspicious URLs** **and attachments**.

If employees are able to spot these common issues with phishing emails, then they become less likely to click on any malicious artifacts, therefore not creating a security incident that needs to be handled by the security team. It is impossible for email defenses to catch every single phishing email, so users need to be ready to identify and report any that land in their mailboxes.

#### Simulated Phishing Attacks

It is common for security-conscious organizations to launch simulated phishing attacks against their own employees in order to determine how effective their current security awareness training is. There are a number of security services that offer phishing attacks as a service, and allow you to customize the email that will be sent to mailboxes under the organization’s domain. If the user clicks on a “malicious” link, they will be redirected to a safe website (typically owned by the company conducting the simulated attack) and will inform them that they have just fallen for a phishing email. Security teams can also monitor how many individuals report the phishing email to them, identifying employees that have understood the training and are able to identify suspicious emails. These events should be conducted every few months to test employees and identify any that are consistently falling for phishing emails so that they can receive additional training.

**Some great platforms for doing this include:**

- Sophos Phish Threat – [Link](https://www.sophos.com/en-us/products/phish-threat.aspx)
- GoPhish Open-Source – [Link](https://getgophish.com/)
- Trend Micro’s Phish Insight – [Link](https://phishinsight.trendmicro.com/en/simulator)
- PhishingBox – [Link](https://www.phishingbox.com/)

----