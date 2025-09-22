There are a lot of techniques that can be used to make emails seem legitimate, increase the chances of targets interacting with malicious elements, bypass security features such as email scanning or make it harder for security teams to take defensive measures and stop malicious emails being delivered to employee mailboxes.

--------
## Spear Phishing

Spear phishing is when a malicious actor spends time before the phishing attack to gather information about their specific target, to make the email more effective. By tailoring the email to the target, it makes it more convincing. 
This type of attack requires planning and good use of open-source intelligence (OSINT) sources to gather information. 

The attacker will look for websites that the target uses, any hobbies or interests they have, and even record family members, colleagues, or friends. All of this information can be used to create highly effective emails that seem legitimate. Let's cover a few examples.

--------
## Impersonation

Impersonation is the act of pretending to be somebody else. This can be used by malicious actors to trick their target into thinking they are someone they know, making them more likely to open and interact with a phishing email. 

A malicious actor could pose as a friend, a colleague, or even someone higher up within the organization, such as a manager, director, or even the CEO.
![[Pasted image 20250210153909.png]]

------------
## Typosquatting and Homographs

**Typo squatting** is the act of impersonating a brand or domain name by misspelling it, such as missing letters or including additional ones. Below are some examples of domains that are typo squatting the real SBT domain, securityblue.team.

- **securltyblue.team**
- **securitybllue.team**
- **securtyblue.team**

A **homoglyph** phishing attack is virtually impossible for users to spot. This attack exploits the fact that many different characters look exactly alike. These characters are called homoglyphs, and the problem is with how the characters are encoded using Unicode.
![[Pasted image 20250210154043.png]]

-----
## Sender Spoofing

Sender spoofing is the process of making the sending address in an email look the same as a legitimate email to make the recipients believe it is coming from a genuine sender. 
This is typically used with credential harvesters where the attacker wants the recipient to believe the email has actually come from the impersonated company so they will be more likely to enter in valid credentials.

--------
## HTML Styling

HTML styling is where code and images are used to style an email. This is used by legitimate emails to provide a more visually attractive design, making the email appear more professional. 

This is a screenshot of a legitimate email from Amazon, which uses styling to produce a branded and eye-catching email. We can implement logos, hyperlinks, different colored text, buttons, tables, and more. HTML styling is typically observed with credential harvesters, as they are trying to impersonate an organization, and legitimate emails from these senders use branding and email templates to keep everything neat.

![[Pasted image 20250210154528.png]]

**It can be ENCODED:**

![[Pasted image 20250210154643.png]]

--------
## Attachments

In phishing campaigns, we will typically see three categories of attachments:

- **Non-malicious files that are used for social engineering** (such as invoices, letters of appeal, and images)
- **Non-malicious files that have malicious hyperlinks** (such as PDFs that contain a link to a malicious site)
- **Malicious files** (such as malicious scripts, or more likely Microsoft Office documents with malicious macros, such as Word or Excel)

**social engineering**
If an attacker is posing as a member of the Human Resources department at the target organization, they could try to extract information from a legitimate employee by sending them a form as an attachment that they need to fill out to assist with a payroll system change or any other bogus pretext scenario. 
This can work well with other tactics such as sender spoofing to make the sending address look like it’s actually coming from the HR department of the organization. 
The below example is playing on social engineering principles such as urgency, stating that if the employee isn’t quick, they might not get their salary this month, in an effort to rush them, giving the target less time to think about what they’re being asked to do.

![[Pasted image 20250210154853.png]]

**Lure Documents**
Inserting hyperlinks into a malicious email is common, and can potentially be detected easily by email security tools that retrieve URLs and sandbox them to see if the destination is malicious or has a bad community reputation. 
A way to prevent this is by including the hyperlink in a document, such as a PDF or Microsoft Word file.
This means that the attachment itself isn’t inherently malicious, but the hyperlink inside can be. In the below example, this file is a lure document to direct users to “view an invoice online”. The destination URL could simply take the user to a malicious domain that downloads malware to the system.

![[Pasted image 20250210154945.png]]

**Malicious Files**
The most common form of inherently malicious files is Microsoft Office documents that are utilizing macros to run malicious code on the system that opens the document. 
They can download additional malware to the system by reaching out to domains on the internet and retrieving files, then executing them. 

As mentioned in the **Malicious Files** lesson of the previous section, macros are now disabled by default, so the attacker needs to convince the recipient to click “Enable Content,” allowing the macros to run. This diagram should be familiar, but it’s good to show it again here.

![[Pasted image 20250210155022.png]]

----

## Hyperlinks

A hyperlink is a webpage URL that is embedded into text, a button, or an image. When clicked, it will open the recipient’s default browser, and navigate to the webpage for them. 
Hyperlinks are used when the attacker wants to direct the target to web resources, such as a malicious file download, a page with a fake login portal acting as a credential harvester, or other content as part of their phishing attack.
![[Pasted image 20250210155129.png]]

----
## URL-Shortening Services

A tactic for disguising malicious URLs, and preventing some aspects of automated security analysis, is the use of URL shortening services such as Bitly and Short URL. 
These services work by keeping a record of full URLs and generating short versions that simply redirect to the full URL. 

**Analyzing Shortened URLs**

One good option is to use the online service WannaBrowser, which lets you simulate any browser (kind of like using a virtual machine, but just for the browser). Visit [https://wannabrowser.net](https://wannabrowser.net/) and paste the shortened URL before clicking on “GET”.
![[Pasted image 20250210155410.png]]
We can use a URL visualization tool URL2PNG to search for our short Bitly address. When we attempt to view the link, we can see that it is actually showing us the error page on the Security Blue Team site!

![[Pasted image 20250210155508.png]]

----
## Use of Legitimate Services

**Email Delivery**

Phishers will make use of legitimate services such as free email providers, to bypass defensive measures that can be implemented by defenders. Whilst we will go into detail about email blocking in the Defensive Measures section of this domain, organizations will typically not block webmail domains, such as:

- @gmail.com
- @outlook.com
- @hotmail.co.uk

**File Hosting**

Malicious actors can also host malicious files, typically Microsoft Office Word and Excel documents with malicious macros, on free platforms such as **Dropbox**, **One Drive**, and **Google Drive**, and then send links to download these files in phishing emails.

-----

## Business Email Compromise

A business email compromise is a phishing attack that can target any organization but focuses on those that are likely to transfer large amounts of money to either purchase goods or pay other parties such as vendors. 
The malicious actor will monitor their target over a period of time to determine which companies the organization pays, and when they have found a relationship between the company and a supplier, they will either compromise an email account belonging to a member of the executive board or a high-level employee, or spoof the address so it appears legitimate, and will instead direct the relevant employees to transfer the money to a different bank account that is under the malicious actor’s control. 

Below we will cover 5 different real-world scenarios where business email compromise is featured.

**Email Compromise & Vendor Attack**

In this scenario, a legitimate email account belonging to an employee who handles payments to vendors is compromised via credential stuffing, a key logger, or some other initial vector. The attack creates an invoice that is branded to look like it has come from the compromised organization (potentially even by retrieving legitimate invoices and editing the text). This will be sent out to any vendors that are in the address book of the compromised email account, and vendors will potentially pay into a malicious actor-owned bank account.

**Email Spoofing & Alternative Payment Attack**

In this scenario either a legitimate email account is compromised or the malicious actor will spoof an email address from the initial organization, and send an email to the target company, offering an alternative payment method for any future payment. If the vendor doesn’t discover this is a spoofed email, they may pay any future payments into the malicious actor’s bank account.

**Email Spoofing & CEO Fraud**

In this scenario, the malicious actor is posing as a member of the executive board, such as the CEO, CTO, CFO, etc, and either contacts employees in the finance department, or either the financial institution that the organization uses to hold their money. They use social engineering tactics to create a sense of urgency, and convince the employee they’re communicating with, that they are in a time-sensitive situation and need money transferred to their bank (actually a malicious actor-controlled account) immediately.

**Email Spoofing & Data Theft**

Malicious actors will spoof an employee, and request to see what information is held on them or request tax invoices. This will allow the phisher to get detailed information about an employee, such as their home address, payment information, contact information, and more. This will typically be used for further spear-phishing emails, as they will be extremely effective as they are using real information about the target. This information could also be sold on to other hackers so they can conduct further attacks themselves, such as blackmail or impersonation.

**Email Compromise & Zombie Phishing**

Zombie phishing is when a malicious actor compromises an email account, replies to old email threads between one or more contact, and inserts a malicious URL into the email. This is more likely to be clicked, as it will have come from a sender that the recipients are familiar with, and have previous legitimate email communication with. This can be extremely effective if done right.