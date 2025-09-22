## Recon

Reconnaissance emails, also referred to as recon emails are used for one reason: **to get a response from the recipient.**
#### Spam Recon Emails
These emails do not use any tactics, and are simply looking to see if an email error code is sent back to the attacker, such as "undeliverable". This allows the attacker to determine whether the mailbox is in use (no error email sent back means the mailbox is in use, and the email was delivered).

![[Pasted image 20250210144609.png]]

#### Social Engineering Recon Emails
Use social engineering techniques, such as posing as a person that the recipient may know or have regular communications with in order to get a response.

#### Tracking Pixels Explained
This is an HTML code snippet that is loaded when a user visits a website or opens an email.
Combined with an **invisible tracking pixel**, which allows the attacker to see if the email has been viewed by an email client.

![[Pasted image 20250210144921.png]]

**The following data can potentially be acquired and analyzed using a tracking pixel.**

- The operating system used (gives information on the use of mobile devices).
- Type of website or email used, for example on mobile or desktop.
- Type of client used, for example, a browser (webmail) or mail program (email client).
- Client’s screen resolution.
- Date and time the email was read.
- IP address (gives information on the Internet Service Provider and location).

------

## Credential Harvester

Credential harvesters are arguably the most common phishing emails out there because they are targeting human weaknesses to attempt to retrieve valid credentials which can potentially be used to gain access to numerous services and accounts as a result of credential stuffing attacks.

Credentials harvesters are sometimes tailored to impersonate login portals for the organization that is being targeted.

![[Pasted image 20250210145146.png]]
Below is a list of key points that often apply to credential harvester emails.

- **Imitates commonly-used websites and services** (such as Outlook, Amazon, HMRC, DHL, FedEx, and many more).
- **Entices the recipient to enter credentials into a fake login portal.**
- **Uses social-engineering tactics including; creating a sense of urgency, and using false authority.**
- **URLs may be completely random or attempt to copy the legitimate domain name of the organization they are masquerading as.**
- **Often have small spelling or styling mistakes, something that is extremely rare with legitimate emails coming from big brands and organizations.**

----

## Social Engineering

Social engineering is the practice of exploiting a human as opposed to a system, using psychological methods in order to get them to complete actions that they wouldn't normally do.

**Commonly used social engineering tactics in phishing emails include:**

- Convincing the recipient to reply to an attacker's initial email (recon emails).
- Convincing the recipient to transfer money by posing as the CEO, CTO, CFO, or another employee on the executive board.
- Convincing the recipient to provide the attackers with information that is confidential or private by posing as the data subject or someone in a higher position within the company.

----

## Vishing and Smishing

#### Smishing 
is a kind of phishing attack, where the attack vector is a text message or SMS. Below would be a profile that a smishing attack could follow:

![[Pasted image 20250210145606.png]]

#### Vishing
is a kind of phishing attack, where the attack vector is through a phone call.  This method relies heavily on the social engineering aspect of phishing by having direct voice-to-voice contact with the victim.

----

## Whaling

These emails will be refined typically using information gained from open-source intelligence sources, making them more believable for the intended target, and increasing the chance they will interact with it.
Whaling is one of the most difficult types of phishing to detect because they are sent in very small volumes and are tailored to appear legitimate and not generate red flags that could alert the security tools or team.

---

## Malicious Files

Along with credential harvesters, emails that convince targets to open malicious files are the most common phishing email classifications. 

**Be carefull:**
- MS Office documents such as Word and Excel offer the ability to include macros.
- Hosted Malware - convincing users to click on a hyperlink, download a file, and then run it.
- Executable attachments: exe, .vbs, .bat etc.

----

## Spam

messages that are unsolicited, unwanted, or unexpected but are not necessarily malicious in nature. Examples of spam emails are:

- **Newsletters that the user has unknowingly signed up for**
- **Marketing emails trying to promote products and services**
- **Update announcements from companies and services the user has registered with**

