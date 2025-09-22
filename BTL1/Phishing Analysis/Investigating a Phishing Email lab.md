**Lab Overview**

In this activity, you will be manually collecting artifacts from safe phishing emails. The Mozilla Thunderbird email client can be used for viewing, as well as the Sublime Text 2 text editor for looking at the .eml files directly Manually collecting artifacts using a client and text editor, is a core skill for phishing analysis, as not all organizations will have access to tools that can automatically retrieve email, web, and file-based artifacts.

The only tools you need to use for this lab are the Mozilla Thunderbird email client and Sublime Text 2. Launch it and drag the emails in (or right-click an email and select 'Open With'), then select either of these two tools.

**If you are prompted to log into Thunderbird, close this prompt and you'll be able to use it without an account.**

---

**Question 1 - Email One - What is the sending address?**

Opening the email in Sublime Text we can use the Find feature (CTRL+F) to search for “From”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c29d138b22bd83eb3dbc058078d6909d16ea478a4778abc8e96b5d35bd4e683f90f565e67274f69c3618bca1f1af.PNG)

---

**Question 2 - Email One - What is the recipient address?**

For this question we'll look for the “To” field and its value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a2e6cabef06eb995e8d0afdc865286e36f918160e83a5658a1d719008b5ace0adc0e7838d8f5189d00b63768ec8c.PNG)

---

**Question 3 - Email One - What is the subject line?**

For this question we'll look for the “Subject” field and its value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/67550c8ca23ee77f3836587dfaf220b04bdd3e132fbdda6ecaafcf389f5bcc9cea47e5cb4750dcf2531be556df86.PNG)

---

**Question 4 - Email One - What is the date and time the email was received? (Retrieve this via text editor. Format: DD MonthName YYYY XX:XX:XX)**

For this question we'll look for the “Date” field and its value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2d2da11fd2589431d692777f821cf72814489822cd9ea0ca8eb98917d27b5367fd5a5f60d7b87e7770791d41e29e.PNG)

---

**Question 5 - Email One - What is the sending server IP address?**

For this question we'll search for the “X-Sender-IP” field and its value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5bad9ccf9a122c71977a476f33f8a6e64b4f9b7116acd51a6e60b5cfe40fd0f80c25e6b95059a4c8f3f913e7c9eb.PNG)

---

**Question 6 - Email One - What is the hostname of this IP address? (Reverse DNS Lookup)**

Taking the IP from the previous question we'll open the site [https://whois.domaintools.com](https://whois.domaintools.com/) and perform a search. We can see the resolved hostname below.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6450e251ebd6b77937fb4a39aa4079608e679c0b825d8d892b0731846d8cce68ef1a0d79a1386e66c051f9693646.PNG)

---

**Question 7 - Email One - What is the full URL hyperlinked within this email?**

The easiest way to retrieve this artifact is to (carefully) right-click the hyperlink when viewing the file in an email client, and select ‘Copy Hyperlink’ (or a similar option).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c62789480d6b9624cf464b1c9fac1db8b4734ae95d822ed700858f3636457cc3b8a9caafbef5ae3e2eb0fc7bdd46.PNG)

---

**Question 8 - Email One - What is the root domain of the URL?**

To find this we can either right-click the link in the email and select ‘copy link location’ and paste it into a program such as Notepad to see the URL text, or search for ‘http’ or ‘https’ in the email file until we find the right link. The ‘root domain’ essentially means the domain name of the URL, not including the specific resource. For this email, the URL is hxxps://www.thiswouldbeamalicioussite.com/index/2020/j411/NetflixLogin.php? (we're replaced https with hxxps to stop it from becoming hyperlinked), so the root domain is ‘thiswouldbeamalicioussite.com’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/65a63d5262e78a5af01c7137ad5d696ad363396ceaea5cafde17b2a89c4f01a2ff6970a13d3c396df523e14fa6fb.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ebac7eb38943825eeca0e238f8b3498d041a5581d7ca0c9ec133f5bb86bba09731d4d71ad73ce16037e736396af8.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c961a3248ef6d5005c6bcc171823403a1a99367de5cee337aa441c7ff09cc04f0781234649d659b032d618163fc8.png)

---

**Question 9 - Email Two - What is the sending address?**

Same as before, we'll use Find and search for “From”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/54bd12eeb34fed06c44b7b52c5d191ccab8e3996764152afc988d4d68930d8aa6985c11328d284715856f398ab13.PNG)

---

**Question 10 - Email Two - What is the recipient address?**

Searching for the “To” field and value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/24f700c0102a36ab7a536d1b9a8d93a6cc8390c75db389a61afdf08fd70aa115952b890481d9a0ef88b1081be071.PNG)

---

**Question 11 - Email Two - What is the subject line?**

Searching for the “Subject” field and value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c9332658e7328bf2d322fd2660ef2355da7281e81036f8deb558742d3f2709e96aaa4bb382806f2bbcfebfda29b1.PNG)

---

**Question 12 - Email Two - What is the date and time the email was received? (Retrieve this via text editor. Format: DD MonthName YYYY XX:XX:XX)**

Searching for the “Date” field and value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/814ce34a8446b41ba7e8a650703f5379f83ff006c43738cbe998c91d9323d3d2e9bf7c466a74564bbe0bf5cf8b30.PNG)

---

**Question 13 - Email Two - What is the sending server IP address?**

Searching for the “X-Sender-IP” field and value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b8f46e23c75b02d06356ba61d8e768e342ac4b0d2ee5e245266535185f566c4fa6441a5d0e9374aa5c769244e464.PNG)

---

**Question 14 - Email Two - What is the hostname of the sending server IP? (Reverse DNS Lookup)**

Using the IP from the previous question, we'll submit it to https://whois.domaintools.com.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7c9026b6b7448e650ce2269c4b3f68bb06180260941ddde12bfadf29f0d1c3a943f5325302b74597e6a2dea7572d.PNG)

---

**Question 15 - Email Two - What is the full file name? (name + extension)**

There are two ways we can get the file name. From within the text editor we can search for “filename”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1ad38a2bbed8db1c349a97f3114cbf9b1488af6b04afaa089d64292d21ccd3a4639693daf7f0d42793997ee15eca.PNG)

And within an email client we can see the attachment name somewhere in the interface. The location and style will vary depending on the client, but Outlook for example will show the attachment details at the top of the email. In Thunderbird, we see this at the bottom.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/82d00b520d7dfb4f8553c96185e737e971ba785bdfa1bfe7e756397d307b2da9e4f64ff81d3cfcaefdd7c0b73709.PNG)

---

**Question 16 - Email Two - What are the MD5 and SHA256 hashes of the attached file? (Format: MD5 SHA256)**

In Thunderbird we can right-click the attachment and click Save-As, then save it to the Desktop. We'll then open a PowerShell window and use the Get-FileHash cmdlet to retrieve the MD5 and SHA256 hashes. As SHA256 is the default hashing algorithm we don't need to state it, however we must do this for MD5.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4c72a1863ca9b7e1e32e642b48cfdc7c24a16d28e682be280f6f1797aba61e11c3a5b25ae59e8d1f8b7e8d6752fe.PNG)