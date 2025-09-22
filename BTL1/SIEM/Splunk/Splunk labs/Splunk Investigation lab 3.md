To get Splunk ready, we'll open a Terminal using the icon on the bottom toolbar and enter in the following command: `sudo systemctl start Splunkd`. After a minute we'll open Firefox and visit `127.0.0.1:8000`. Next we'll click on the ‘Search & Reporting’ app on the left-hand side of the Splunk homepage.

We need to make sure we can see all of the logs as they were generated back in 2020. To do this we'll click on the timeframe selector on the far right and select OTHER > All time on the right.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6bc46e36ea3fa18a10dec6ca24f08fa8f399c8e162d4d6070f40ff7c5988078c8d4fb2f380fdef711b3659470f4e.PNG)

Whenever we conduct a search we want to start the query with `**index="botsv1"**` to ensure we are loading the right data.

We're ready to get started with the lab questions!

---

**Question 1 - OSINT can be extremely useful in almost every investigation. Perform a Google search for osk.exe - what is the full name of the Windows feature associated with osk.exe?**

Searching for “what is osk.exe” on Google tells us that this is the file used to run the On-Screen Keyboard feature from Windows.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c3a1dafc02451164b8584c22f06dca45115a0957ed7b9b758aeb889ac1e8612008c606475672df433ba8a890c1cd.PNG)

---

**Question 2 - Continue with your OSINT research. What is the expected file path for osk.exe? (Path to the folder, or full file paths are accepted)**

The screenshot from Q1 also tells us where the legitimate file is stored; in `C:\Windows\System32\osk.exe`.

---

**Question 3 - Filter on Sysmon events (sourcetype=xmlwineventlog) and search for the suspicious executable name. How many events are returned based on this query?**

Based on the sourcetype provided in the question, we know our full query will look like this: `index="botsv1" sourcetype=xmlwineventlog osk.exe`. When the search completes, we can see there are 49,608 events found.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/224fae72cb580bc8c36376602a253dc63cb3c121c8905163d75cb852b059ba21425953ae4801ea12d8d9d329b011.PNG)

---

**Question 4 - What is the full file path of the suspicious executable?**

Looking at these logs, we can see under the ‘Image’ field that osk.exe is NOT being stored in the C:\Windows\system32\ folder where it should be. What does this mean? This is not the real On-Screen Keyboard binary, but is trying to hide by looking legitimate!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c46993ad7ae3fb9560ffbaae6be35dc115de99323de0ab4c62c3917c6751463b7207355f210d96eda22a9e1bb7fe.PNG)

---

**Question 5 - What computer is the suspicious file running on, what is the internal IP address, and which user account is running it?**

Now that we've found something suspicious, let's gather information about the system this file is running on. In these logs we can find three useful pieces of information; the system name, the IP, and the user account:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3efe7a62ca870de13372ccb70369c77f68e8d95a76f7afa562a9c4e8cd1e4532e685052d45b5702964c0932fb475.PNG)

---

**Question 6 - To scope our next searches only on this executable, find an appropriate field + value pair to add to your search query. Next it's a good idea to see if there are any network connections - what destination ports is this file connecting to?**

Currently, as we're just using “osk.exe” in our search query, it will find events that have this string in any field of an event. To narrow this down within the Sysmon logs, we can include the Image field with the full file path value in our search query. We'll click on Image in the Interesting Fields panel and click on the path to the suspicious osk.exe.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2f2f5f5ee480e1ee033295460583f073ee9c7c13754e3843fd3e3fed56a911c151381b25ec9106b240a22d709832.PNG)

Now that we've updated our search query, we see that the number of matched events has gone down from 49,608 to 49,594 - only 14 less, but this search is still neater!

Looking back to the Interesting Fields, we can see DestinationPort exists, with 2 values. Clicking on it will show us the destination ports observed.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/bbf661b083edee781d2f57d970dd6e926caccb9ddc7e19265669d577ed4f457846de7dabac6cd3a799e756561393.PNG)

---

**Question 7 - Adding the destination port with the highest activity to your query, use 'count' functionality to identify the number of unique destination IP addresses this file is connecting to**

First let's add the destination port 6892 to our search, because this is extremely suspicious. Why does an On-Screen Keyboard feature from Windows need to connect to ANYTHING over the network? And even if it did, why is it connecting to high-numbered port 6892, which is non-standard. This is more evidence helping us to confirm that this file is likely malicious. We'll click on the ‘6892’ port in the DestinationPort popup from Q6.

Our search query is now:`index="botsv1" sourcetype=xmlwineventlog osk.exe Image="C:\\Users\\bob.smith.WAYNECORPINC\\AppData\\Roaming\\{35ACA89F-933F-6A5D-2776-A3589FB99832}\\osk.exe" DestinationPort=6892`. If you want to get into the habit of keeping your searches neat, you can remove the ‘osk.exe’ after the sourcetype, as it's no longer needed because we are referencing that file using the Image field.

Looking at the Interesting Fields panel we can see that DestinationIP has 100+ results. As the number of unique values in this field is above 100, we can't easily get the count from just looking at it - we'll need to run our own search.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/da0f969d03010cf5a87bfc5b191b731a9f8692a63f1343a9a603b50efbf1eef48298eebd3457a0a51d0126f1f30b.PNG)

To look through all of the 'DestinationIp' values and only retrieve unique values, we can add the following to the end of our search query: `| stats count by DestinationIp`. We can now see that this file has connected outbound to 16,384 IP addresses… wow.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b743f9a65332cb99fad5fe58147266b9aefee300b0e5dabe98b755115a5fbb54b1fa6a265d2d38f4e22b405627c1.PNG)

---

**Question 8 - Sysmon EventID 7 logs contain the hash values of files (ImageLoaded field) that are executed. Use this to find the SHA256 hash of the suspicious osk.exe and submit it**

Let's start with a new search query, as we're focusing on a specific type of Sysmon log. Based on the information present in the question, and the fact we're still looking at osk.exe, we'll run the following search to see if it works as intended: `index="botsv1" sourcetype=xmlwineventlog EventID=7 ImageLoaded=*osk.exe`.

For this specific question, we only need one relevant log to get the answer, so as soon as events are found we can stop the search using the square button underneath the search bar on the right-hand side.

In the below screenshot, in the highlighted section you can see that the ‘ImageLoaded’ field is using the full file path value for osk.exe. After this field we have the ‘Hashes’ field that holds multiple values, but the one we're interested in is the SHA256 hash string.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/831358b4b23159852499b65d9e8dd5d0b29806282ae8d15e583b0223ee1b518dd47c3b05fca3f263228ce03c8026.PNG)

---

**Question 9 - Outside of the lab, submit the SHA256 hash to VirusTotal. Based on the results on the Detection page, what is the potential name of this malware?**

Copying the SHA256 out of the log in Splunk, then copying it from the Clipboard tab of the lab client, we can easily paste it into VirusTotal. Looking at the results, we can see a lot of mentions of ‘Cerber’. This appears to be the only ‘name’ referenced on this page, as almost everything else is using generic or descriptive names.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c173b827b967d944b01e79078b46c3e5ec88fa41013ecfa2107485c1f7d1ae722632eee4b6e510f40d936eb8a758.PNG)

---

**Question 10 - Sysmon was useful, but let's investigate the network traffic coming from the suspicious file out to thousands of IP addresses. To do this we'll look at the Fortigate Unified Threat Management logs. Find something all (but one) of the osk.exe sysmon logs have in common regarding network traffic and use this in your search query. What is the category of malware dedicated by Fortigate?**

From our previous searches, in Q6 we found that two destination ports were contacted, with 1 single request going to port 80, and all of the rest went to 6892. We'll use this as the indicator for this traffic, because 6892 is not a standard destination port, so we are very unlikely to get other non-related events included in our search (if we wanted to be extra safe, we could even include the source IP of the system making these connections, just in case another system was also making requests to destination port 6892). Our search query will be: `index="botsv1" sourcetype=fortigate_utm dest_port=6892`.

Looking at the results, we can clearly see lots of useful fields from Fortigate that tell us about this threat. According to the ‘appcat’ (threat category), ‘app’ (threat), and ‘msg’ (message) fields, the values tell us that Fortigate has flagged this for Cerber botnet activity. Therefore the category of malware reported here is a botnet.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2bb305aa8f73fa4774c5d4d29816b63df7e33a3922cda96a8b13d244b4614f976dfd8065c7cee07d1d1df4050800.PNG)

---

**Question 11 - What is the name given to this specific malware by Fortigate?**

As mentioned above, the category for this malware is botnet, and the name given is Cerber, something we also saw on VirusTotal earlier.

---

**Question 12 - Conduct another OSINT search for the name of the malware. What is the primary function of this malware? (Submit the malware category, different from Q10)**

A simple Google search for ‘Cerber Malware’ shows us results from high-profile security companies, clearly stating that Cerber is a type of ransomware. The reason that Fortigate is flagging it as a botnet is that it also includes that functionality, and if you read some of these posts, you can learn about it in more detail!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eb9d98385b5f76aef67b244ee34d944784c77bbeb1442f3f7d6a2f1e53f206b2e26d401d302ac0f354d9cc540732.PNG)

---

**Question 13 - Finally, let's investigate the single connection from osk.exe to a remote IP address on destination port 80 HTTP. Find the IP from the Sysmon logs and use it to search in the suricata logs - these logs have different event types, and we're interested in 'alert'. If Suricata has alerted on this activity, what is the signature value?**

Based on the fact we're tasked with looking at suricata logs, we know that our search query is going to start with index="botsv1" sourcetype=suricata. Because these are just network intrusion detection/prevention system (NID/PS) logs, we most likely wont see any reference to the file generating this traffic, osk.exe, so we need something else to search on so we can find the relevant events.

We can use destination port 80, but this search is going to bring back a huge amount of events, because we aren't being specific enough. We could include the source IP of the system running osk.exe, but this search is also too wide, because we would get results related to any HTTP traffic over port 80.

To be as specific as possible, let's run one of our old searches again so we can find out the destination IP of the single event of osk.exe reaching out to port 80. We'll use the query `index="botsv1" sourcetype=xmlwineventlog osk.exe`. We will click on the DestinationPort field under the Interesting Fields header on the left and this time click on “80”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/309d5ab1d24653fd6c3ddd4ae9d7fc9da334b5647cf7b37e0f30ac41318eeccf0a0149ef4ac82f8728f604cd337a.PNG)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8418a20b2061bb998b50b9bd5bd46e29f89a0cc7cec81078c7ca18a21b2b6e54d748eea75fcf7137723decb62667.PNG)

Looking at the single event, we can retrieve the source IP and Destination IP values from the log. We'll use these to narrow our final search to make sure we're looking at the right Suricata logs. We need to remember that while Sysmon logs use 'SourceIp' and' DestinationIp' field names, we cant be 100% sure that Suricata will use those same names, so to work out what those fields are called let's jump in with a wide search using `index="botsv1" sourcetype=suricata`.

After a few events show up we can cancel the search. Looking at the Event Details panel we can easily see the format used by Suricata for its logs:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0eadf6a20a9f51fc958c4c6842daa8d04c82764ec83d3d9e38467723b703202428d39464e5fd41eb2652013a376d.PNG)

Now that we understand the formatting, we can build our full search query to identify the suspicious port 80 HTTP traffic from osk.exe using Suricata logs: `index="botsv1" sourcetype=suricata src_ip=192.168.250.100 dest_ip=54.148.194.58 dest_port=80`. After a few seconds we can see that 4 logs match our search query! This question also tells us that we're interested in the event_type ‘alert’ - as there's a very small volume of logs, we can look through them to find the right one(s), however if there was a large number of events, we could add it to our search query using `event_type=alert`.

After finding the right event we can click on the “>” arrow in the top-left of the row to see all fields and values (some information may be hidden when looking at the Event Details panel, because this sometimes is used as a preview instead of the full raw log).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d6240ebc77588d773470a26edf49652fb0fd8c8e8ab90c8da8455f66f98510bd67082f3be99c1bd793b113b4c6d6.PNG)

Finally, in a field that is not configured to show on the Event Details panel, we can see the alert.signature value for this log is related to an external IP lookup, an action that is conducted by attackers or malware to identify the public IP of the machine or network, helping them to understand what company they have compromised (based on indicators such as the IP range owner, ASN owner, WHOis contact details, and more).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/bdab04a9aa2b53ad41821e730ebf7f25c5fe9226ea33a217be18d848a8ee00c6d05aa8d75c07260acc371d148572.PNG)