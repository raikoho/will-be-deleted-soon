## Protocols:
#### Simple Mail Transfer Protocol (SMTP)

Simple Mail Transfer Protocol works on TCP port 25 by default, is a communication protocol for electronic mail transmission. Once an email is created it is sent to the organization's SMTP server, which transports the email to the next server, before it eventually reaches the SMTP server of the recipient organization.

However, the world is moving away from port 25 and the new standard is becoming TCP port 587. This port, coupled with TLS encryption, will ensure that email is submitted securely and follows the guidelines set out by the IETF.

#### Post Office Protocol 3 (POP3)

Post Office Protocol (POP) is an application-layer Internet standard protocol used by e-mail clients to retrieve e-mail from a mail server, with version 3 (POP3) being the most widely-used version on the internet. POP works by contacting your email server and downloading all emails from it. Once they are downloaded onto your system, they are deleted from the email server. This means that after the email is downloaded, it can only be accessed using the computer that downloaded the emails, and trying to access your emails from a different device will not work.

#### Internet Mail Access Protocol (IMAP)

IMAP allows you to access your email wherever you are, from any device. When you read an email message using IMAP you're reading it from the email server. As a result, you can check your email from different devices, such as a laptop, desktop, and mobile phone. IMAP still allows for emails to be downloaded, but you must manually click to save the email locally. This method for accessing emails is a lot more common than using POP, as it allows for better accessibility.

In the below diagram, we will be following a scenario where John Smith working at BlackArch Solutions is emailing a friend, Aimee Faren at DicksonUnited. We will cover which protocols are used to deliver emails, and make them accessible by clients.

---
## Anatomy of Email

#### Email Header

**Header Fields**

The **message** itself, is made up of the two following elements: the **header fields**, a set of lines describing the message's settings, such as the sender, the recipient, the date, etc. An email includes at least the three following headers:

- `**From**`, showing the sender's email address
- `**To**`, showing the recipient's email address
- `**Date**`, showing the date when the email was sent.

**Optional Header Fields**

It may also contain the following optional fields:

- `**Received**`**,** showing various information about the intermediary servers and the date when the message was processed
- `**Reply-To**`, showing a reply address
- `**subject**` showing the message's subject
- `**message-ID**`, showing a unique identification for the message
- `**message body**`, containing the message, separated from the header by a line break

**Custom X-Headers**

X-headers are called such because their name must begin with **X-**. 
For example, some anti-spam software programs mark messages as unwanted using the following header: `**X-Spam-Status: YES**`.

#### Email Body

An email body is where the information written by the sender is displayed for the recipient. This can be purely text-based or it can include hyperlinks, images, and HTML styling.

----
## Phishing

In short, phishing is a type of email-based attack, where malicious actors are actually attacking humans instead of computer systems, in order to get them to do something they normally wouldn't. 
Examples include giving out their account credentials, downloading malware, transferring money, disclosing information, and more.

