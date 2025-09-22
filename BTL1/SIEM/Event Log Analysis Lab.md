On the Desktop we can find a folder called ‘Event Log Analysis’ which contains a single file, ‘Security Investigation.evtx’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2c21e93795df4ac86ad0b992ff34bb8b0c89d5ae74a425dbbdfdfb6582e7b831a46d89e330cb1d695f10863d9aea.png)

After double-clicking this file, give Event Viewer a few minutes to load and show you the event logs.

---

**Question 1 - At what time is the first Special Logon event?**

One approach to this question is to filter the logs based on the date and time they occurred. By default Event Viewer will show the most recent events at the top, so if we left-click on the Date and Time column once, it'll show the oldest logs first. From here we can see that the first log recorded is a 4672 Special Login. We can take the date from the log, and make sure it fits the expected format.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1b9aa3ce831327c778093eb51df3d41a2d88883b8e2940199cd8d86f3db44707595989aa7f346fbd67e76c1dceeb.png)

Alternatively, when looking at a much bigger export of event logs (as this capture only has 11 logs), we can use a filter to only look at specific event IDs, which in this case would be 4672. This can be achieved by clicking on ‘Filter Current Log…’ on the right-hand panel of Event Viewer. We have added 4672 to the input box half-way down the popup, and after clicking ‘OK’ we'll see our results.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/869946d746fc864a33dd76c7cdb7d78797ffb72709e82892e0b4d3328bfb01df9889ceabb1217e389639bc1600b4.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f190a847ee8084deb853c23f5f46356d94cd1786b434a6ab1d871ac17a8b22b9f70269b7f522241a9d50e1ee32d7.png)

---

**Question 2 - At what time does Jeff create another user account?**

Following the time-ordered chain of events, we can see a ‘User Account Management’ event (4720). Within the log details we can see the person that took the action (Jeff, the Subject), and the new account created, SteveE. We can take the date from the log, and make sure it fits the expected format.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0019ef65603ddc2dd23ee0a34549685fe9d6abc805ccfc72a71f38e093124466a2a9770460c1415c0af3691391e4.png)

Alternatively, we could create a new filter to look for 4720 event IDs.

---

**Question 3 - What is the name of the new account?**

We have already recovered the new user's name in the previous question!

---

**Question 4 - What is the Windows event ID for the creation of the new user account?**

Based on the previous two questions, event ID 4720 is used for new user creation.

---

**Question 5 - What are the names of the three user groups that the new account is in, listed alphabetically?** 

When users are added to Windows Security Groups, 4732 event IDs are generated (Security Group Management). Looking through the log details we can see the group that the target account was added to. In the first event the account is added to the default group ‘Users’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a82f7614208ab66bf55c00ac7b716e4be46993a19e589d7fcf7997618ec2e90099c7d24ac625b52cf80607af667f.png)

In the second event the account is added to the ServiceAccount group.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a40a03e975f937d019be485d252800d4ece7e360b61a97bdd89eb37b263e885757c71dca28a0bf2a2063a7e7c5bb.png)

And in the third event the account is added to the Administrators group.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4a44256a0616224de807e43fc75ea29ecccbca6cb01abb4703122f5324ad2d99bfe6dbe57710a983f5ff130b30b6.png)

---

**Question 6 - At what time does the new user account log in?**

To find the answer for this question we can create a new filter for 4624 (normal logo) and 4672 (special logon) event IDs. Looking through these events we can find a special logon that involves the new account, SteveE. Remember, this is a special logon, not a standard logon, because this account is in the Administrators localgroup.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/05624d909432098bedec743601f6f9bd0d51e9ef9d19658300922df7c816dd115106aea38786255f93e66f238dbb.png)