**Question 1 - Run DeepBlueCLI from a PowerShell window, and set the target evtx file as .\evtx\password-spray.evtx. How many accounts were targeted in a password spray attack, and what is the MITRE ATT&CK Technique ID for password spraying?**

Running the provided command we can see that 41 accounts were targeted in this password spray.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/362b8bd9c926fd67ded3ef0dba512bc1288264b58cff43b86097ab0ce528f63af45aaf3142b40d413ff168820409.png)

Searching Google (or the MITRE ATT&CK website directly) for “password spray”, we find the following sub-technique page:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1c2f0ed4bbce1774cf770cdd2a062f8d9ca7f4dc214406c26ae817d35d19a7db1518d6dc8b753ca6b884e1c890da.png)

---

**Question 2 - Still looking at password-spray.evtx, what is the responsible user and hostname of the system?**

Looking at the output of the command, we can also find the username and hostname.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8c95a2110f9a2e054b8f1f214bb1f71405e2cf4f493e1089a4b22a0527e9a5012d6b0abddafb7ace91f8f8ab0227.png)

---

**Question 3 - Investigate new-user-security.evtx. What is the username of the created account, and what group was it added to?**

Looking at this new evtx file, we can easily find the username and the group they were added to.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/50d2c90a722c4e79377b2d10e57ff2402429e9039efa386222e9cd61de394f55a91b5c8d905662d9ab5327f6448a.png)

---

**Question 4 - Investigate powersploit-system.evtx. What is the MOST RECENT file that is being downloaded using PowerShell's 'Net.WebClient' functionality? Provide the full URL**

Running DeepBlue against this .evtx file shows two detections for downloads, however, based on the question we've been asked to find the most recent one.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c37bd519e1dafb2d74aee0ec99150c9e9cf454a3b9b44ba5d9a421908710aacbd74387e97aab98ce984012495001.png)

---

**Question 5 - To look at all of the event logs at once and export it to a text file, we can use the following argument "./DeepBlue.ps1 .\evtx\* > output.txt". Lots of open-source offensive tools are stored on GitHub, which means attackers can download them using PowerShell. Open the created text file and use CTRL+F to search for "githubusercontent". What is the .ps1 script that is downloaded?** 

Following the steps, we run the command which will create ‘output.txt’ in the DeepBlue folder on our Desktop.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c68a81f3e752dcf3629448b7d3e944c496d0e94f267bcf719246b4396b22603b4d8672412d21b37a5dcbe88bcfa2.png)

Searching for “githubusercontent” there are 3 matches, all of which are for the same file download, but at different times. This gives us the answer to the question.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fc0bf61ae96e9e893775829a74ca771ce660bf1fdde6d00569951fd4409008888427a64400789c7a4eb285d2a808.png)

---

**Question 6 - Search for the name of the tool on MITRE ATT&CK. What is the Software ID given to this tool?**

Searching on Google for “Mimikatz MITRE ATT&CK" we can find the Software page for this tool.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e2dbe906b1345253ca15154ed0df854ea0eeacea7ac801878c0138837e44aff593bcb4807e2eb0a0e4ad6f96d5da.png)