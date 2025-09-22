To get Splunk ready, we'll open a Terminal using the icon on the bottom toolbar and enter in the following command: `sudo systemctl start Splunkd`. After a minute we'll open Firefox and visit `127.0.0.1:8000*`. Next we'll click on the ‘Search & Reporting’ app on the left-hand side of the Splunk homepage.

We need to make sure we can see all of the logs as they were generated back in 2020. To do this we'll click on the timeframe selector on the far right and select OTHER > All time on the right.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6bc46e36ea3fa18a10dec6ca24f08fa8f399c8e162d4d6070f40ff7c5988078c8d4fb2f380fdef711b3659470f4e.PNG)

Whenever we conduct a search we want to start the query with `index="botsv1"` to ensure we are loading the right data.

We're ready to get started with the lab questions!

---

**Question 1 - Click on Dashboards and go to Splunk Investigation 4. How many Suricata alerts are there, and how many Fortigate alerts are there?**

First we'll click on Search & Reporting App, then Dashboards at the top of the page. At the top of the Splunk Investigation 4 dashboard we can see two panels being used as counters for both Fortigate alerts and Suricata alerts.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2ec53a9a950276931a86f95a982f69b0bbd0317f9d41353b46c0587b66bc71adaec4f5c7859795f1ada5b157bcb7.PNG)

---

**Question 2 - Edit the dashboard and look at the search query for the Fortigate Alerts counter. What is the full query used to generate this number?**

To see the search queries that are powering dashboard panels we first need to Edit the dashboard in the top right corner. Then we can click on the magnifying glass icon of a panel, which is the ‘Edit Search’ option.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4aee17e9e1a4c75d2a7f7b100f318cd2d31db719e7a76604b7137a55e93c7689276987c4370156bcfe3fa77482d0.PNG)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f82788d61c2bedf2c7372cb91dd3eff6d57d22e61f17b575921b0aae45532caefa3ce33e37af677d41c509cfab1a.PNG)

---

**Question 3 - What is the full query used to generate the Suricata Alerts counter?**

We'll take the same actions as we did for Q2, and click the magnifying glass icon on the Suricata Alerts counter panel to see the search query behind it.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4c70cabe928e34ce8d1f85b1676c8e2aff4ad69b64eff718a0326dc661bf98bfbff68226434711982fd887323a20.PNG)

---

**Question 4 - Click on the Suricata alert titled 'Information Leak' to see the associated events. What is the source IP address, and what is the destination IP address?**

We can find this alert category on Line 6 of the Suricata Alerts (Categories) table.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/968dcc2c2c56f2b2dd84919cad0992114e2f11106f48731fd04efd76cf775891815592386c6b2846c3b7b35eeaf2.PNG)

Looking at the 2 events, we can see the dest_ip and src_ip are shown immediately, giving us our answer. The external IP 40.80.148.42 is connecting to our internal system which is hosted internally on 192.168.250.70 on port 80 (HTTP).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0fb64d8e7617254887ef535b8a84618d0dcb0a5fa7505a7d04563755f36adf3b23e430b77a0138ce0b0c63d1cfdd.PNG)

---

**Question 5 - What action did Suricata take after observing these events?**

Just looking at the events in the screenshot above, we cannot see any fields that would tell me what actions Suricata took, so we'll click on 'Show as raw text' at the bottom of each event to change the displayed format. We can now see a field called ‘action’!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/16b94746706d6d209b2b0514d67d861891be0021a3517e9e19161f45ddb15401a783239d0c1ded286866026ea66a.PNG)

In this case, both events were allowed by Suricata. If this tool is deployed in Network Intrusion Prevention System mode (NIPS) as opposed to Network Intrusion Detection System (NIDS) then it could take actions to stop malicious connections, such as applying the ‘block’ action to end the connection!

---

**Question 6 - We know the alert category is 'Information Leak', however the specific signature can provide us with more information about this activity. What is the signature shared by both events?**

In the below screenshot, we have showed two different ways to view this field within the Suricata logs. This signature is a lot less generic than the category, and can provide context to what is actually happening.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fe089f3c42376b7429de71778b6e875bd4ea9a0086efbfefa4b91d47f1f05504ba701f55113bf59c31e41b4dbd37.PNG)

---

**Question 7 - Based on the logs, combine two fields to understand the full website addresses being accessed by the attacker (Remember, in some logs a "/" character must be escaped by putting a "\" in front of it. You should not reference the "\")**

Looking at the logs we can see two fields that will help us answer this question: hostname and URL. Using these we can see the two targeted full URLs were:

- imreallynotbatman.com/phpinfo.php5
- imreallynotbatman.com/phpinfo.php

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f16e045bd197b8054901509d24cf619d8ddacd0aad466fc547efe9a5b1a64951b8ae971956417c4fe86748960efb.PNG)

---

**Question 8 - What HTTP status code is returned to both of these requests, that tells us this attack was not successful?**

Looking at the logs we can see a field named ‘status’, where the value is 404 for both event. This tells us that the attacker tried to reach these URLs, but there is nothing there (Error 404, Not Found).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/56390c14164aa9897275572d78be97d4bc7c536e97230c319b41d6a7b474f417ab604868503b74b5774feddc058a.PNG)

---

**Question 9 - Return to the Dashboard and click on the Suricata alert titled 'A Network Trojan was detected' to load this search. Modify the search query to show count of every signature field within this alert category. How many unique suricata signatures are present?**

Looking at the Suricata Security Alerts (Categories) table we can see the category we want on line 3.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/84a06dd1a9b7e33db435039e5f0a2162f6e96cc91c77a6ce2ce1812cef2f63508306893b48445a891d212d03b541.PNG)

We're being asked to identify how many signatures are found within this category of alerts. To do this we'll add the following to our search query to get the count of signature values: `| stats count by signature`. Looking at the Statistics title, we can see there are 12 unique signatures that have been observed within logs for this category.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eae2e68841e948e14568d4a305438731598a77bfecb7889bdd445dd5ecccea9ee1cce3ce11d650cf671c67a87648.PNG)

---

**Question 10 - Search manually through Suricata logs where the HTTP status code is 200, then perform a count of each signature field to find two signatures that reference a vulnerability CVE identifier. Search this CVE on the National Vulnerability Database.- what is the CVSS Version 3 Score?**

Okay - there's a lot to do in this question, so let's go step by step. Firstly we'll build our brand new search query for Suricata logs, specifically alert logs, where the status code is 200. The query will look like this: index="botsv1" sourcetype=suricata event_type=alert status=200.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ddfca9935016e5b6f46e897f16e0bba01e27bbd140fec5f34e86428131f5c99e3c8740c5d63ab8f01f428be3f962.PNG)

Great, next we need to get the count of values in the signature field. We'll add the following to our search: `| stats count by signature`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/000bc37a079dc6690b7a2b2673aae1bd1ceb03348681e02e6c11901944aa2919b22e52c85317e5e867130bb51167.PNG)

Great, we've found the reference to a Common Vulnerability and Exposures identifier, used as an identification method for vulnerabilities. Next we're asked to find the score of this vulnerability, so we'll search for it on Google using the search “CVE-2014-6271 national vulnerability database”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/847fea0ae2f511c8723bf5554894970666e7266a807c46049136029e6e4fc6c3382d2012972f4e977e4a0433bc94.PNG)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f7c28098c5da161780d7e8efa0089be643d4d903f658c5499f47f41350f3cc0ba0567c0c7058479f670e39d3cf24.PNG)

---

**Question 11 - On the Fortigate Security Alerts dashboard table click on 'MS.Windows.CMD.Reverse.Shell'. Identify the internal IP within this event, and use your SIEM skills to identify the name of this system.**

We can find the associated Fortigate alert category on the final row (13) of the dashboard table.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2f7e0395fdbf0c507830365319abaf8d8e7281524ee7e22127f47f75b64e3ad9af8bb317ed2c1c203a0ece3058b2.PNG)

Clicking on the row will take us to a single Fortigate_UTM log. We can see that the internal IP address is in the ‘dstip’ field, and is 192.168.250.70. Because this log is from a Firewall, Fortigate has no idea what the hostname is for this system, so we'll need to use a different log source to find this.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0dd824908848e21d5b7659b73517ac0fce1c547b83c421a7faee503d7935603d7f6b30c6d6d44928afb561ecfb51.PNG)

Let's be smart about this, this alert is about abuse of the Microsoft Windows Command Prompt. It is possible that the internal system is running Windows, and should have Sysmon logs enabled (xmlwineventlog). Let's change our search query to look at that sourcetype and free-search the IP (without declaring a field name, as we don't know what format it will be).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/912bed2646a14c95c4774ed2d8bd405705cadf2dd3c6ea16512ac0a18ee143c2d7fc6fb85e10a64d66c840c9c1c7.PNG)

Here is another proposed method of solving it—which many students find easier:

Filtering by the IP 192.168.250.70 will indeed yield multiple hostnames.

![](https://i.imgur.com/ItPzB7O.png)

However, if the user includes the attacker's IP address in their search, they will obtain a single result and the answer to question 11.

Filter: index=* sourcetype=xmlwineventlog 23.22.63.114 192.168.250.70 | stats count by SourceHostname | sort - count  
 
![](https://i.imgur.com/tEykE5l.png)
**Question 12 - Go back to the Fortigate Security Events table and click on 'Apache.Roller.OGNL.Injection.Remote.Code.Execution'. Find the reference field in the log and open the URL on your host machine. What is the Affected Products text, and the CVE identifier?**

We can find the relevant Fortigate alert category on the 10th row of the dashboard table.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/22d85d66cb49ec1b3e029161df1d3fcff3517bb905419cd2a77f9a85036d94160acb45f7e8cf718297822243aa34.PNG)

Looking at the event we can see there is a field titled ‘ref’ which contains a URL.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fbf8827e17af046ac436551946c0d770f334f4af98622c0a6ab5f7480968af431c3cb8a535f35f318d0d36f7dc4c.PNG)

Unfortunately, when trying to visit the URL, we get redirected to FortGuard's homepage. In the top right we can see there is a search bar, and clicking on it offers us the ability to change it to an ‘ID Lookup’ search. Let's try that with our VID number!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/61d8980d755c1884bf6da210d6c7b67a4bc89115e35c885f165a48e53925e62503f75aec7ee13f7f48155cc0e55d.PNG)

Next we want to click on the right search result, based on the name of the category we saw in Splunk:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a81ca357af6e96b1ac2fbac40db15f601bc0a49d2bb08171155cff0f8031730c836ed4c0b76e3e375d75d70da502.PNG)

Here we can find all the information we need!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9399b3db39968e19297d8dd5aae6c5da50e6e2227868a4b380a406e6c4a49960d49f257011d81aa69347f0a7c362.PNG)

---

**Question 13 - On the dashboard consider the Fortigate category with the highest number of events. Try to find the version of the scanning tool being used, looking at Fortigate logs then Suricata logs.**

We can clearly see from the Fortigate alert table that ‘Acunetix.Web.Vulnerability.Scanner’ is the attack type with the most events generated. Let's see if we can identify what version of this tool is being used!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5d4c57d5bb544688f9587b828e4870bba3dc9f57a597548edb2b8aa1cb4f08002daae653a44f16d84df84fa07cf4.PNG)

Looking at the logs, there's nothing immediately obvious that tells us the version of this tool. There is a reference field so it's worth seeing if this will tell us the version.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d9df113128a81412bbb5be132f608ce2a79843f3d84ec7d08289816a62c6f089ac1fd93aac5be501d6f8d620a88f.PNG)

However after searching it online, it doesn't give us any version information.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e3c51d158139c1c4317d204d969d04358f8cddbfd5c97c97b66e74f7b64444591157eb7a10060a3a525cff7fce9d.PNG)

As we can't find anything helpful in the Fortigate logs, let's pivot to the Suricata logs instead. To do this we'll change our sourcetype to Suricata and free-search for ‘Acunetix’ as this is the name of the scanner.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/63f94326d0dde55aa91fef0b1fa9460db54b272b80abd1d48d84134b7f4cab659150b1ea5373b33ad903c5b34ef3.PNG)

---

**Question 14 - Investigate Suricata 'alert' logs to understand how they present the severity of the alert. Create a search query that gets the count of events based on each severity rating. When you having a working query click on 'Save As > Existing Dashboard' and select the Splunk Investigation 4 dashboard. Edit the dashboard and click on 'Select visualization' on the panel you just added to change it to a pie chart (feel free to add an appropriate title!). Hover your mouse over the 'High' section of the pie chart, what is the count%?.**

We're told we need to look at Suricata alert logs, so we'll perform our first search using: `index="botsv1" sourcetype=suricata event_type=alert`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/66a06262a3657230cd3d97ff0f66c3bdda325bc301b9f15ca86fb9b648b352e7151b1ae994d5e4e92095015f3a1b.PNG)

Now that we know the severity field is called alert.severity, we could perform a stats count for each severity. Interestingly, there is another field called ‘severity’ that is using low, high, medium ratings, which is easier for us to understand than numbers, so we'll use this instead.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3c6dc2ef74bd2e33889bf57c79928d844cdbccdd58cd4f212261cb77c9d5dd51bc48106a06cc613daa59f218443b.PNG)

Now that our search works, let's save it to our Splunk Investigation 4 dashboard using the ‘Save As’ button.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/79bb67cc368e2b5626554281f714b08c55cffb7dc167e2ab524cdc5ee309d0ef653af650ff9375ce6ce529cd938a.PNG)

We now see the search at the bottom of our dashboard, however by default it is in the Table visualisation, and we want to change this to a Pie Chart. We'll click ‘Edit’ in the top right of the dashboard then click on the ‘Select Visualization’ button of our new panel.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/326b4ab40560c3a01ac21e3e783703c68667c315d08f71ea8cedc55635dccd5804715f0de54a349c8b0934b3a688.PNG)

Next we'll select Pie Chart from the list.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/695e2425bb04fe93320ee3e7c7202fbf7758035e4b170fa73282538bdaa22344d30b146f53ef3f07b15552b7b4e7.PNG)

And we'll see that the graphic has been updated! We're going to set a sub-title (2nd title field) as “Suricata Alert Severity”. We can now click ‘Save’ in the top right of the dashboard.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d55f15ae397e67d8e082cef0268c7a08b7fbd474258f04871a29cf2e9ab83d7fcc7eeb473487d584d1203591cbfd.PNG)

Hovering over the High section of the chart shows us the count% value we need to answer the question.

---

**Question 15 - Complete the same steps above but for Fortigate_UTM logs, creating a pie chart based on severity. If you want to keep things neat, you can drag your new pie chart next to your Suricata one! What is the count% of critical alerts?**

First we need to understand the field name that holds the severity rating for these logs. We'll perform a generic search for fortigate_utm alert logs, and quickly find a field called ‘severity' - perfect! Let's create a search to get the counts per severity value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7586d240fad8162bb3677f68fc85bcd13acb5498081e77f95bdc7c6d2f8d542118e582bcd27806008a1b34e9d1d2.PNG)

Now we'll save it to our dashboard and convert it to a Pie Chart, same as before.

While editing the dashboard, we can click on the ::::::::::::::: border of a panel to drag it around and resposition it. Let's drag our second Pie Chart (fortigate_utm severity) next to our first Pie Chart, and save the dashboard.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a219ef0f104b3a472f3f1ef22020a7c59db2ddf74bc50ae399860fa767874e77125593eb7df34f75c36578ac7653.PNG)

Hovering over the Critical section of the chart (or the critical text itself, which is easier!) shows us the count% value we need to answer the question.