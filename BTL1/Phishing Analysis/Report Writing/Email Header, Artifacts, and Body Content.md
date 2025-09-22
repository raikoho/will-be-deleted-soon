Analysts tend to fall into two traps: writing too much, including unnecessary details that bloat the case, or not writing enough, so later individuals need to re-investigate certain parts of the case in order to fully understand what’s happened. Both of these waste time.

### Email Header, Artifacts, and Body Content

The first things we gather from a malicious or suspect email are artifacts (also referred to as IOCs). We use this information to try to link attacks together into campaigns, identify malicious actors behind the attacks, generate metrics, and perform trend analysis, allowing us to predict what will happen in the near future.

We need to include these in our report in a clear and concise way, so they can be found quickly, and other analysts can copy and paste them into different tools or services if needed (such as IOC reputation lookups, internal tools for searching, or sharing with other colleagues).

**Email Header and Artifacts**

From the analysis section of this domain, you should feel confident retrieving the following artifacts from reported emails:

**Email Header**:

- **Sending Email Address** (Ex: J0hnSm1th@gmail.com)
- **Reply-to Address** (Ex: F4keacc0unt2421@gmail.com)
- **Date Sent** (Ex: 20th October 2019, 9:34 AM)
- **Sending Server IP** (Ex: 40.92.10.10)
- **Reverse DNS of Sending Server IP** (Ex: mail-oln040092010100.outbound.protection.outlook.com)
- **Recipient(s)** (Ex: jason.s@domain.com, kirsty.p@domain.com, brian.b@domain.com)
- **Subject Line** (Ex: Payroll Update – URGENT!)

**Email with URLs:**

- **Any relevant URLs** **(Sanitised)** (Ex: hxxps://Healthcare-United[.]com/wp/index/2020/PAYPAL/lure.php?)

**Emails with Attachments:**

- **File Name(s) + Extension** (Ex: PayrollDecember_UK.exe)
- **MD5 Hash(es)**

### Email Body Content

In whatever platform you’re using to store investigation notes, we would attach the email file directly to our case (in either `.eml` or `.msg` format, provided if it allows it) so that we have a copy of it for as long as needed. 
It’s good practice to include a brief description of the email and a screenshot in your case notes, saving other analysts the hassle of downloading and opening the email file in a client themselves. Whilst how the email looks isn't hugely important when it comes to taking defensive measures, it is still important as it can be used to identify trends or targeted attacks, and generate metrics about the type of malicious emails received.

You should aim to write approximately 1-2 sentences describing what the email looks like, and what it’s trying to get the recipient to do. We cover two examples below that’ll give you some guidance on how this information, as well as the artifacts, should be presented in a clear and concise manner.

# Example One

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fe174418fe57e5da5da264c64d9a3bb0fc919638c425a000530691cc5564d077b87670425022e06e783c7908839d.png)
## **Artifacts Retrieved**

- **Sender:** bobtom112233@gmail.com
- **Reply-to:** None
- **Date:** Monday 16th September 2019 17:33
- **Sending Server IP**: 209.85.167.42
- **Reverse DNS**: mail-lf1-f42.google.com
- **Recipients**: contact@dicksonunited.co.uk
- **Subject**: Hello
- **URL:** None
- **Attachments:** None

## **Email Description**

- This email contains no malicious URLs or attachments and is attempting to get the recipient to respond, either to engage in a social engineering attack or to see if the recipient mailbox is in use so it can be targeted in future attacks. Email classed as Recon.

---
# Example Two

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ca1aa1aabd62c323be48745d0046d127f4f026defe63262963f770157de617e24cf6cc41faa7ff33e9af7631ef10.png)

## **Artifacts Retrieved**

- **Sender**: amazonsupp0rt@outlook.com
- **Reply-to:** no-reply@amazon.co.uk
- **Date:** Monday 16th September 2019 19:25
- **Sending Server IP**: 209.85.167.91
- **Reverse DNS**: mail-lf1-f91.google.com
- **Recipients**: claire.shelley@dicksonunited.co.uk
- **Subject**: Suspicious Amazon Order Alert
- **URL:** hxxp://maliciousdomainexample[.]com/
- **Attachments:** None
## **Email Description**

- This email from an Outlook mailbox is posing as Amazon using effective styling and asks the user to click a link to reset their password claiming that the user’s account has been hacked and used to purchase an order of £329.99. Using a sense of urgency is a common social engineer tactic, used to make the user rush and not think about what’s actually happening. The email contains a malicious URL, as it is not pointing to an Amazon-owned domain. Email classed as malicious / credential harvester.