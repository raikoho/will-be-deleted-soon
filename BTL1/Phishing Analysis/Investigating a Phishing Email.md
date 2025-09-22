retrieving email, web, and file-based artifacts using manual and automated methods so that they can be analyzed at the next stage of the investigation.
# Email Artifacts to Collect

#### Sending Email Address

This is where the email has come from or appeared to come from. During the Tactics and Techniques section, we covered spoofing, and how malicious actors can alter what the sending address looks like to make it appear legitimate. Regardless of whether this has obviously been spoofed, we need to record the email address that has apparently sent the email. We can use this as a search term in email gateway security products to identify any other emails that have come from, or been sent to that address.
#### Subject Line

The subject line is a very useful artifact for both searching for other associated emails by using it as a search term in our email gateway security product, or for blocking incoming emails that are in the same attack and using the same subject line.
#### Recipient Email Addresses

We need to identify which mailboxes have received this same phishing email, so we can inform them not to interact with it. Usually, the malicious actor will enter the recipients into the Blind Carbon Copy (BCC) field, so that recipients can’t see who else the email was sent to. To identify recipients we would typically check our email gateway, and search for emails coming from the sending address and including the subject line we have observed, which will give us a list of any other mailboxes that received the same email.
#### Sending Server IP & Reverse DNS

We need to know the address of the server that has sent the email, as this will help us to identify if the sending address has been spoofed. Once we have collected the IP we can perform a reverse DNS search on it using online tools such as [Reverse IP Lookup by MXToolbox](https://mxtoolbox.com/ReverseLookup.aspx), which will provide us with a hostname that should give us some more information about the server.
#### Reply-To Address

This is the email address that will receive any replies to the original email. In some cases, this value will be different than the sending address, as if an attacker has successfully spoofed “support@amazon.com” any replies would go to that address, which the attacker won’t have access to. Instead, they can insert an email address of an attacker-controlled account, so now replies will go to “flamingo91591@outlook.com”.
#### Date & Time

It’s good practice to record the date and time an email was sent. Searching for a period of time on either side of the observed time could allow for other emails to be identified that are a part of the same attack or campaign. This can also be used as a metric to see at what times the organization receives the most malicious emails.
## SOLVING:

We can use email clients to retrieve common indicators very quickly and easily. Viewing our example email in Microsoft’s Outlook client we can immediately retrieve four artifacts:

1. **Subject Line =** Hello
2. **Sending Address =** bobtom112233@gmail.com
3. **Date + Time =** Monday 16th September 2019 at 17:33
4. **Recipient(s) =** contact@dicksonunited.co.uk

![[Pasted image 20250210162121.png]]
There is additional information that we need to collect such as the **Sending Server IP** (which server has sent the email), and the **Reply-To address** (where any replies to the email will be sent – this may not always be the initial sender). These can easily be obtained by downloading the email in either .eml or .msg file format and opening the file with a text editor.

![[Pasted image 20250210162410.png]]

The first thing we want to collect is the sending server **IP**, also referred to as the **X-Sender-IP**. Press CTRL + F (or your OS equivalent) and search for “IP”. The first string that you find should be the **X-Sender-IP** (if not, keep clicking “Find” or “Find Prev” until you find it).

Now that we have the IP, we need to convert the **address** into a **hostname**. 
We can do this by performing a reverse **DNS lookup**. We recommend you use the free online service by Domain Tools – [https://whois.domaintools.com/](https://whois.domaintools.com/). 
If we input the sending server IP we just received ([https://whois.domaintools.com/209.85.167.42](https://whois.domaintools.com/209.85.167.42)) we can retrieve information about the server.

![[Pasted image 20250210162501.png]]
In the above screenshot, we can see that the host is **mail-If1-f42.google.com** – a Gmail sending server. Sometimes the sending address domain and sending IP might not match up. If the sender is **bob@gmail.com** but the IP address belongs to **Outlook**, we know that the sending address has been spoofed. We’ll cover this in a future lesson.

Next, we need to retrieve the **Reply-To** address. In the below screenshot, using a different example email, we have used the search function within Sublime Text 2 to look for the string “reply”. We have now identified the address that would receive any replies to this email.

![[Pasted image 20250210162558.png]]

So, Full artifacts list will be:

- **Sending Address**
- **Subject Line**
- **Recipient(s)**
- **Date and Time**
- **Sending Server IP**
- **Reverse DNS of Sending Server IP**
- **Reply-To** (if present)

-----
# File Artifacts

#### Attachment Name

The attachment name is a useful artifact when it comes to defensive measures, as depending on the uniqueness of the name, it can possibly be blocked using an organization’s Endpoint Detection and Response (EDR) platform, using the filename as an indicator of compromise. This should always include the file name and file extension.

#### SHA256 Hash Value

A hash, the unique string generated from a file, needs to be recorded as it represents the file in its entirety, and can be used for reputation checks using online tools such as [VirusTotal](https://www.virustotal.com/gui/) and [Talos File Reputation](https://talosintelligence.com/talos_file_reputation). MD5 and SHA1 hashes should no longer be used, as they have known hash collisions, so SHA256 is the current security standard for file hashing.

## Solving

- Powershell:

```
Get-FileHash -Path "Apply Music Invoice 13313a.docx" -Algorithm MD5

Get-FileHash -Path "Apply Music Invoice 13313a.docx" -Algorithm SHA256
```

- Linux CLI:

```
sha256sum <file>
sha1sum <file>
md5sum <file>
```
# Web Artifacts

#### Full URLs

It’s important that when investigating a phishing email that contains a URL that it is copied properly, and not written out by hand, as this can lead to mistakes that will impact the investigation during the analysis stage. The URL should be copied either from the email client by right-clicking the hyperlink and selecting “Copy Link Destination”, or by copying it from a text editor.
#### Root Domain

Whilst this artifact isn’t necessary if you have the full URL, sometimes the root domain can be an important artifact, as it can help show if the site has been created for malicious activity, or if it is a legitimate site that has been compromised.
## Solving

The term “web artifact” is used to describe a hyperlink in an email that will redirect the recipient to a domain, an IP address, or a specific URL. These can be used to host fake login portals that steal any entered credentials or pages that host malware which is downloaded when the site is visited. We are looking to retrieve:

- **The full URL** (the complete web address as it is sent in the email)
- **The root domain** (only the domain name, not including specific pages)

In this phishing email, we can see that this section of text is hyperlinked, and the user is told to click on it. By hovering the mouse over this text we can see the URL, which definitely doesn’t belong to PayPal.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e6dca46efc84ae8f0d3aebbf6e43a2f9f3e884943ecf50db0f7bce262c30f05b2d4d64d79eb17ae8d4d4b80cc44d.png)

We can right-click the URL and select “Copy Hyperlink” to send the URL to our clipboard, which we can post elsewhere.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6232f465fdcee00e78f3db329aeb6b56a7bda4ccd2e6d33aaf529d0a9882d6e0f33796955871b4a8e72a1cbece41.png)

Although this method is much faster than using a text editor, there is always the risk that you could accidentally click on the malicious URL and end up visiting the page. 

**Text Editor Exfiltration**

In a text editor, we can use the CTRL+F keyboard shortcut to enable the “Find” feature. There are three quick ways to find the URL(s) we want:

- **Search for “http” as this will identify any http or https addresses being mentioned within the email.**
- **Search for anchor HTML tags `<a>` which are used to perform hyperlinking.**
- **Search for the text from the email body that is a hyperlink, in this example, we could search for “you can cancel it”.**

We’re going to use the last method.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f9ce96791ef590595330b7014be6a407fc1b7ecf07d7fcb0ed4bef82e5322b1355f42d722fa12340bc8aa52802db.png)

And there we have it, we can see the URL within the `<a>` HTML tags, and can copy it without fear of accidentally clicking on the link and being taken to a potentially malicious site.

-------

# Automated Collection With PhishTool

PhishTool provides a forensic analysis console, giving individuals the power to forensically analyze phishing emails, tag malicious artifacts, and generate investigation reports.
### Example One

On the analysis console homepage, you’ll be presented with the view as shown in the below screenshot. This is where we can drag-and-drop a malicious email, or browse of file system and upload it.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/16bee07544ac7f6593243e23230014aa7960893427827e29467267b8ddc9bcad661aa68ca1a48082acd0d3453d96.png)

In this case, we’re going to click the Browse button and find the email we want to submit for analysis. In this case, we’re going to upload this Amazon credential harvester!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/bcb2b2061c3fd5ea428eee862a009b87c72b50123e414fd5a82bab90c767ee416debc41a09acb11f06091b1cac58.png)

Once the analysis has been completed, you will see a screen that looks similar to the following screenshot. This page holds all of the results from artifact extraction and analysis procedures. 
You can click the clipboard icon next to artifact names to copy them.
 

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f596782503e865c87e7f482be207f0dae9e4c6df92aa6812efffcdd4cc8aca159232c95417b81df7343cac52cbfb.png)

The artifacts we’re interested in are:

1. **Sending Address**
2. **Subject Line**
3. **Recipients**
4. **Date + Time**
5. **Sending Server IP**
6. **Reverse DNS**
7. **URLs** (if applicable)
8. **File Name** (not applicable)
9. **File Hash** (not applicable)

So let’s gather these from the PhishTool analysis console! In this **Basic Header** section, we will be able to retrieve artifacts **1, 2, 3, and 4.**
 ![](https://i.imgur.com/KRxVDmO.png)

Below this, there is a section for **Detailed Header** that includes the X-Originating-IP and the reverse DNS results, which gives us artifacts 5 and 6.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6c733ba84cc714c4865f88256c59f1c0fba1b4fa6a26885831634b1220d50201571bb11b306a90c919278a4a4204.png)

And finally down at the bottom, we have a section for **URLs**, where we can retrieve all hyperlinks that were included in the email.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/07da3f81c5a92fb73fabe031e5af328b135c1b27a19a0202f5301fb7b28f4602d5d2613b04be81c79dc226321c4a.png)
### Example Two

In this second example we’re going to submit an email that has a potentially malicious attachment, so we can show you how to retrieve file-based artifacts using PhishTool. Below is a screenshot of the phishing email we’re going to analyze.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b12d7af6dd3cbb3b2f8a721b25bc9f7fc28aee00be4ab5ddd595cb9219a4b6035bd63fef1086bc25900744f8d6cc.png)

After submitting the email to PhishTool, under the Basic Header section there is a section titled **Attachments**. This provides us with the MD5 hash of the file and the file name! We can also click on the VirusTotal link to automatically submit the hash for analysis and retrieve a community reputation score.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/038b3de090d25d12368a104d5698c21de91fae5b11ac7d1c117ad7f89e06622fd9d3b24232db8e57ee9796215600.png)