**Question 1 - What is the name of the file that was attached to a phishing email?**

Looking in folder for Lab 3 on the Desktop we can find the file. Right-clicking it we can go to Properties and copy the filename. We also need the file extension, which we can see on this panel is ‘.html’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/edc718e32d68c04c7c1e03452bd65ea587b21d1ee058ac0f5b11ddc659e022daf100a2b17444b7ae62a4a4d0173a.png)

---

**Question 2 - What is the SHA256 hash value of this file?**  
We can hold shift and right-click in the folder that contains the file to select ‘Open PowerShell Window Here’. Then we'll use the command Get-FileHash MICRO (then pressing the Tab key to auto-complete the filename).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ebaa234416efbc896ef220a143721bb1854ab479cfe3688f99597721f7713ca68b7b8043c2aeff1747fe5d56b279.png)

---

**Question 3 - What is the file size in KB?**

We can get this value by right-clicking the file, clicking Properties, then looking at the Size property.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8aba5e2905ca4ad086b9f1593d768bef90f86da2b0350528b51b9909855c6dfc1dd83a671a64bebdd94910a798d3.png)

---

**Question 4 - Open the file - What company is the presented web page trying to impersonate?**

Based on the Website Title property and the design, this web page is imitating Microsoft's Outlook / Office365 login portal (even though the logo image isn't loading, because the lab has no internet connection).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a16eb29db784da99024568f50a7b59e3eb5c2dc22877a7e134808951705d191ceba2e6f9ce55f6cf00d5d623fe15.png)

---

**Question 5 - Based on the email address that has been auto filled, what recipient was this phishing email targeting?**

We can see that the email is already set in the web page as contact@securityblue.team.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/101c907e70eee18d6e0bc2d6a5502702db0bd36db3b63ca6c8a699b7d20e66fd7bb0f9045eda61fc9ee7e2f16a12.png)

---

**Question 6 - Right-click the web page within Chrome and select View Source. Press CTRL+A to select all of the text, then CTRL+C to copy it. Open up CyberChef from the folder on the Desktop and paste the text into the 'Input' box in the top right. Drag 'URL Decode' from the left-hand panel into the 'Recipe' tab to decode it. Search for "logo" - what is the filename of the Microsoft logo used?**

Putting the source code in CyberChef with the URL Decode operation, we can see the contents of the web page clearly.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d3fc53e98f17fa780c059713beb26987f0ae003b2adf083c310fb979adbc92386afee777024a00bacf88379e6653.png)

Using CTRL+F we can search for ‘logo’ and find the URL and filename we need to answer this question.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6aa78c1f8ee39f50fb0635ff44e6d7ef1542e2c44f6a79c27cb2d88d197376f5814a698aedffbdd1542e7d394049.png)

---

**Question 7 - Open Developer Tools (see instructions if you're unsure) and go to the Network tab. Enter in the password 'test' and click Sign in. Click on the off.php entry - what is the request URL being used to send the email and password to the web server?**

Opening Developer Tools then going to the Network tab, we can see any network activity on a website. Submitting the password ‘test’ will result in the following URL being visited on a malicious domain, which is how the attacker receives the credentials. Copying this value will give us the answer for the question. Notice how the email and password are in this URL!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a6c9593d2a579aff29564e66a7eea7edd12a7216687a75658e048207e017ccfc5848fdfcfb136c09934a8e6b4f9f.png)