**Launching TheHive**

We are provided with steps to follow on the ‘Instructions’ tab of the lab client.

We'll open a terminal from the bottom taskbar and enter the command `sudo docker run -p 9000:9000 btl1-thehive5`.

We can see from the header of our terminal window (or using the ifconfig command in a new terminal, and looking for the ens5 adapter's IP address) that the private IP of our machine is 10.0.2.26, so we'll open Firefox and visit HTTP://10.0.2.26:9000. We can now see TheHive login screen! The instructions tell us that we need to login using BTL1@securityblue.team and password.

---

**Question 1) How many cases have been recorded within TheHive?**

From the Cases page, we can see that there are 6 cases present in the platform.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9e4d2830f596e003190d2557b579962bd5c24cc95ce72965028f44301978b4a5e545b551b7a2a0dd1f9d310dd008.png)

---

**Question 2) How many cases are open, and how many are closed?**

There are a few ways we can get this answer, one of them involves clicking on Quick Filters, which gives us the open and closed count.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/cf531d557269ba0c908d8ea66721f8fc79f0ed84d6b88353a4b5d094f9f6298325dc583c8abdad6a8af4afe81715.png)

---

**Question 3) Investigate the #5 case. What tags have been assigned to this case?**

From the list of all cases, we can see the second column has a heading of “#NUMBER”, so we'll click on the title of the #5 case.

From the General tab, we can see there are two tags applied, “phishing” and “email”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/194185c4df5edc6e648b3f63adc8668b2b1602bd6ce2c7c5a6c286c4c27008592e2336f0aa5c24b99b539a603f02.png)

---

**Question 4) Look at the task related to taking defensive measures. How many blocks have been requested/conducted?**

Navigating to the Tasks tab and clicking on the ‘Take Defensive Measures’ task, we cab see that the analyst has requested/conducted 2 blocks, one email block and one web block.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/55aea566d10d8015f77cdc51d5e018f2fee7c8d2cde9490a3103ca91be9aa3ea194a7e0be339862542173d734d7a.png)

---

**Question 5) How many Observables have been created for this case?**

From the Observables tab name, we can already see there is (8). If we click into the tab we can also count them ourselves.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/15b92fb27692ae843dd548345bdc00d2260b1386071b0e816a36907bc95236bb00cdb91b9711641db9630979cde3.png)

---

**Question 6) There is an Observable with the data type 'ip' that begins with 54. What is this IP related to?**

Clicking on the IP data-type observable for 54.240.48.89, we can read the description and see this is related to a “sending server ip”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/85f0c27217f56e8e8affcf7559d1b12868f49be7bb55f2fb4b5cb89080a320c5b2ebf53742040d1d6e2e9cc131f9.png)

---

**Question 7) What is the size of the attachment within the case?**

Heading over to the Attachments tab, we can see in the SIZE column there's a value of 24.66 KB.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c5793f03c710acc0e458e09bce480bfc4a2bccb248fa63dfb2dcfb17407f5c10f4d6fb0902c6451311acf56de338.png)

---

**Question 8) This case was closed. What was the Status, and was there any Impact?**

Looking at the left column with the case properties, we can see the Status is TruePositive, and the Impact is No.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0e44149d67f2c10ddcae0bbddb3aa933078f95f1799a387ee02f6208ccf83cf400be2d0153f61ba74a7368a1f811.png)

---

**Question 9) Case #4 is missing something important to the case. What tab is missing this important information?**

After looking through the tabs that we've been trained to use (case properties left column, General, Tasks, Observables, Attachments, Comments) we can see that this case is referring to a file, but there are no attachments! It's important to make sure files are attached.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eb60b1fd201deac5a63acce505cde03b0aa45f86190a03b14f0beaceae44f4c022ca1811cc23377a1cbe19c128c5.png)

---

**Question 10) What is the name of the Security Incident Response Team member that assisted with this case?**

To understand the case, we want to read the tasks to see what is happening. From this, we can gather that Jason Smith from SIRT has been asked to assist.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/60a4e563744af871cb84d3611dffb7f5ac0a34cf13d3deb408cdbd69027c4f63d04a2afd817046c2fab32f0ea7a0.png)

---

**Question 11) How many tasks have been marked as complete?**

There's a few ways to get this value, but we'll click on Quick Filters and then Complete tasks, where we can see there are 14 results.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5f1dcfdd7cbc78024a30cf02e1e2aeb5af648aa631c151d87d24ca34ae1c83155157f4d1660793df9fab9547b1fc.png)

---

**Question 12) How many tasks have a status of Waiting?**

We'll complete the same actions we did for Q11, but select ‘Waiting’ from Quick Filters instead. There are 9 waiting tasks.

---

**Question 13) Looking at the Operations Dashboard, how many cases have a severity of Low, Medium, and Critical?**

Moving to the Dashboards page we'll click on Operational Dashboard. In the donut graph on the right (Case Severity) we can see there are 2, 3, 1 low medium and critical severity cases.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/be2339f78e35c3c7a18a781606258fd0b8a43db2fb44179323828a6a3b1ae5f47601e50075b6361f5c7751ad74c9.png)

---

**Question 14) How many case templates are available for use by the team?**

Looking at the middle dashboard graph we can see there are currently 5 different case templates ready for use by analysts.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/06f374606933d729df52db2175420ffd4ecaa537e89173a55e02731ae755c059be999da7330fa63c2150279424a9.png)

---

**Question 15) Go back to Cases and open #4. Look at the left-hand column of the case, and notice the red "1" icon in the bottom left, called "Related Cases". Click this. What is the title of the related case?**

Going to the Cases page then select case #4, on the bottom of the left column we can see the following:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6cd63cd8bbbd8732794414402e9df7c95fbed8f7714098f20d6b8c3cdf2911d040b04a5cac130f68bc7ca4f2a6f8.png)

Clicking on this icon will change the middle panel to show the related case, and how it's related.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/93e54b776704c74761031569e5c600be3f179d41079533547d5d67557eee54a5a37efd8be1e843df606e2cd7d0e4.png)

---

**Question 16) What is one of the two linked observables that are shared by both of these cases?**

We can see the two linked observables in the right-hand column. Submit either of these.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/93e54b776704c74761031569e5c600be3f179d41079533547d5d67557eee54a5a37efd8be1e843df606e2cd7d0e4.png)

---

**Question 17) Don't forget to play around with TheHive! Once you're done, you can type "complete" below to finish this last question.**

When you're done with the lab, type the text “complete” into the answer box.