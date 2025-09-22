This lesson will cover typical email defenses in more detail, and what they do to protect the organization from attacks. Let’s recap on typical security controls to protect against malicious emails, URLs, and attachments.

---

# SPF, DKIM, DMARC

Domain (DNS) records can be used for a wide variety of purposes, such as enabling a mail server to use a custom domain, hosting a website, and also offering the ability to set up anti-spoofing records as well.  With many cyber-attacks coming from phishing emails and spoofing, these domain records help protect custom domain names from being exploited by an attacker.  The following three record types; **SPF**, **DKIM** and **DMARC**; can be used together to help strengthen the security of an organizations email service.

**Sender Policy Framework (SPF):**

A Sender Policy Framework (SPF) record is a type of DNS (TXT) record that can help prevent an email address from being forged.  This record is established to identify the hostnames or IP addresses that are allowed to send emails for your custom domain.  When having an SPF record specified on your domain, it helps prevent a malicious actor from spoofing your domain. The SPF TXT record contains three parts: the declaration of the record type, the IP addresses and external domains that can send on your domain’s behalf, and an enforcement rule.

**Domain Keys Identified Mail (DKIM):**

Domain Keys Identified Mail (DKIM) is a method of email authentication that cryptographically verifies if an email has been sent by its trusted servers and hasn’t been tampered with during transmission across the internet.  The way that DKIM works is that when the mail server sends an email, an encrypted hash of the email contents is generated using a private key and then it adds this hash to the email header as a DKIM signature.  The receiving server will be able to verify whether the email contents have not been tampered with by looking up the corresponding public key in the domains DNS records.  Once the receiving mail server decrypts the email with the public key, it calculates a new hash and verifies whether the original and the newly generated hash match to ensure email message integrity.

**Domain-based Message Authentication, Reporting & Conformance (DMARC):**

Domain-based Message Authentication, Reporting & Conformance (DMARC) is an email authentication, policy, and reporting protocol.  DMARC is built largely off of concepts taken from SPF and DKIM, but it adds several improvements for those protocols.  This type of record allows the domain owner to specify what should happen if emails fail both SPF and DKIM checks.  There are three basic options that the mail server can take: none, quarantine, and reject.

---

# Marking External Emails

Employees must understand the risk of external emails. Although they could be legitimate from entities such as customers, employee personal email addresses, vendors, suppliers, and potential clients – the majority of phishing emails will come from external addresses. In platforms such as Microsoft Exchange or Office365, there is the ability to alter the subject line or body text of an email address that is coming into the organization to alert the recipient that this email isn’t an internal communication, and could potentially be malicious. This simple warning can make employees think twice about interacting with an external email, such as opening an attachment or clicking on a hyperlink.

A good idea is to apply a rule where any email coming from an external sender into the organization has the subject line appended with a very short message, such as “[EXTERNAL]” or “[EXT]”. Appending messages to subject lines can be counterproductive, and make it hard for employees to read subject lines at a glance, so some organizations opt to add a message to the top of the email body content using a bright font color such as red, so that it stands out and isn’t missed by employees.

---

# Spam Filter

Spam filters were created with the end-user in mind.  Since the rise of email messaging and the internet in the 1990s, more and more cyber-attacks can often be delivered through email services.  Phishing attempts, social engineering and payloads delivered through email can all be caught through a spam filter, depending on the type of filter and how they are configured.  Because of the plethora of filters, there are three main types of spam filters that could be utilized:

1. **Gateway Spam Filters –** Ones that sit behind an on-premises firewall of a network.  These can often be utilized by larger enterprise organizations and an example of a Gateway filter is the Barracuda email security gateway
2. **Hosted Spam Filters –** These are ones that are hosted within the cloud.  These work very similar to gateway spam filters but are able to update more quickly than some of the on-premises filters and an example of a hosted filter is SpamTitan.
3. **Desktop Spam Filters –** These filters are user-installed and are typically used in SOHO scenarios.  One major drawback of these kinds of filters is that they can sometimes be categorized as “Freeware” and you may not fully know what the application is installing on your system

---

# Data Loss Prevention

Data Loss Prevention, or DLP, is a combination of controls designed to prevent information from leaving an organization via email, or at least notifying someone that potentially sensitive documents have been sent out either via attachments or text in the email body.

These solutions can flag emails based on keywords such as ‘confidential’, ‘proprietary’, and many more to give the security team visibility of potential data leaks, whether they are intentional or accidental.

---

# Sandboxing

Malicious attachments get through email gateways. This is often because pre-defined rules and configurations are used to block specific file types or naming conventions, meaning that files that look legitimate, such as Microsoft Office documents with malicious macros can sail through and land in employee mailboxes. This is where attachment sandboxing comes in – emails that include file attachments are extracted and analyzed, and files are detonated (run) in a virtual environment, where everything is monitored to see actually what happens when a file is executed. If any malicious indicators are observed, such as trying to download additional files from a malicious domain or trying to create or alter existing processes, the attachment is classed as malicious, and the email will not be delivered.

---

# Attachment Restrictions

It isn’t a good idea to block attachments outright – employees will have difficulty sending legitimate documents internally and externally. The most appropriate way to approach this situation is to consider what file types are often used for malicious purposes, which file types the organization deals with on a regular basis, and whether blocking them would have any negative impact on the business. The most obvious file types that are used for malicious activity are:

- **.exe** (Executable)
- **.vbs** (Visual Basic Script)
- **.js** (JavaScript)
- **.iso** (Optical Disk Image)
- **.bat** (Windows Batch File)
- **.ps/.ps1**
- **.htm/.html**

---

# Security Awareness Training

Employees should routinely undergo security awareness training, that reminds them of their role in protecting the organization, as it is everyone’s job. This training should focus on policies that employees must adhere to, but also cover phishing topics such as; how to spot an email, and what to do when they find a suspicious email. 
This type of training works to address phishing at the human level, as it is a social engineering attack, and needs an employee to fall victim for the attack to succeed. Routine simulated phishing campaigns should be conducted against employees to gather metrics based on the number of employees that reported the emails as being malicious, and the number of employees that clicked on the link. Employees that have unfortunately fallen for the phishing attack should be given additional training and time to ensure they are able to spot and respond to these attacks in the future.