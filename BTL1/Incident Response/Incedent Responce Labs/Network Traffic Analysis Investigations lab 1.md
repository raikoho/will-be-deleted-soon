**Question 1 - PCAP 1 - Identify the first evidence of host discovery scanning on the network (prior to TCP). What is the IP address and what is the protocol used?**

Opening the first PCAP we can immediately see Address Resolution Protocol (ARP) traffic.  Based on the ‘Info’ column we can see that 192.168.56.1 is broadcasting on the network, asking every IP in the subnet (192.168.56.2 to 192.168.56.254) what their associated MAC address is. This is a form of network enumeration that allows an actor to identify online systems within the network when they reply to the ARP request with their MAC address.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/35f8d257952ebd1da76152c17eba253e95e235cc96a9b0d4481b55062c518f303effdef564dc1d833e2904b4a4c2.png)

---

**Question 2 - PCAP 1 - What IP address is being port-scanned by the malicious IP?**

In the question we're told that one system is being port-scanned. Based on this information it is highly likely that the attacker's system is attempting to connect to a target system on a large number of ports. Going to Statistics > Conversations we can see that the source IP 192.168.56.1 (column 1) is connecting to random destination ports (column 4) on destination IP 192.168.56.111 (column 3), where each of these conversations is two packets long (column 5). This is clear evidence of port scanning where the target is 192.168.56.111.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/564dc69f35b8ed82dcda2e3ab66c913b29da35777950f6f2b46f6ecdfe86d6642f4c504e45ba002615ab7c4a9d16.png)

---

**Question 3 - PCAP 1 - Take a closer look at some of the packets associated with FTP traffic. How many users are allowed to connect to the FTP server at once?**

Filtering on FTP traffic only using the filter “FTP” we can see a few response packets that provide informational text to the requesting client. Clicking on one we can see in the bottom pane there is text that mentions how many users can have active sessions at once.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7f8bddb4388f5ab34c65ae0947f2c82b24f2aec8e0dd4365c257bc3ee37c6627d316b2829bde0f380453bc602027.png)

---

**Question 4 - PCAP 1 - The attacker tries to log into the FTP server using the username "anonymous". What incorrect password is supplied?**

Keeping our filter just looking at FTP traffic we can see a request is made by 192.168.56.1 to the FTP server running on 192.168.56.111 with the username anonymous. It's important to remember that FTP is an insecure protocol, meaning we can see usernames and passwords in plaintext. We're asked to find the password supplied during this authentication attempt - we can either keep scrolling down the packet list, or we can right-click the highlighted packet and Follow > TCP Stream.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8273f75b4217fe6490a68a29f1983bd5e6e02c66d6bdc405c83e5d7754623999e228ee7180280bde02f1dfab315a.png)

In the below screenshot we can see that the client provided the server with the user ‘anonymous’ then the password ‘IEUser@’, which resulted in a failed authentication.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/51db7f0a079d7c98d1afad329d8aba9e7eedbf9f2b896013478de631fd8d3319aa7d033efd2d1046a62f5dcf4144.png)

---

**Question 5 - PCAP 1 - Export the robots.txt 404 page from packet 4612 as a HTTP Object and open the text file. What is the version number of Apache running on 192.168.56.111?**

We're provided with the packet number, and based on the question we know it's HTTP traffic, so we'll filter using ‘http’ then find packet 4612.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c8b69597fd421ced2178ba345cd850974899db685b11a920f4aef427d6c6c9a6260a03f4d099fa3e07496f99a7b0.png)

In this packet the system running a web server (192.168.56.111) is sending a 404 page not found response back to the requesting client (192.168.56.1). Using Wireshark we can retrieve the HTML file used to generate the 404 webpage that the client will see. Going to File > Export Objects > HTTP we can see HTML pages captured in the PCAP and export them.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3f95dbe09df43c390e368681d902acddab77c56f886f406331958119b34fd7b23a45a393ef8405a3f50930eb2ec7.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/918b902b2e2d984f2c6cde747d56a2939ce6694de7135c4373b847743426b7f655b08798dd66a28f75180ecc76a6.png)

Looking at the Packet column we can find 4612 and select ‘Save’ then save it our Desktop. Opening the file we can see the web server framework, Apache, and version, 2.4.38.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c6ecf61cff9e35e2460640254887adaf2bdae18b131bfd33c95512882abe2e75f8ca2f76e71eca0e7a8ab96bcfc1.png)

---

**Question 6 - PCAP 2 - What IP address downloaded the ZIP file?**

Moving to PCAP 2 we know that a ZIP file was downloaded, and the most likely protocol is going to be HTTPso we'll go to File > Export Objects > HTTP. Looking at the window we can see there is a ZIP file based on the Content Type column showing ‘application/zip’. If the ZIP didn't show up here, we would go to File > Export Objects, and look at the other options such as SMB, SFTP, etc.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e0c6af3074256d20ae0d454b7d70bc89f1d05ad2264ea2c476004b71a43c3d7b1e7b7b3b1277f79865d75e2297ca.png)

Clicking on the row in the popup will take us to the correct packet within the capture, so we can now close this window and look at the main window. We're looking at the 200 response from the server (source = 192.168.56.1) back to the client that is requesting to download the file (destination = 192.168.56.111).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6d6fe137fca910d7c9713dd567649daae5769577a8c8730a8056841ce638bacae9a7811c356bbb43f0f2bba4c0f5.png)

To view the entire conversational better we will right-click the packet and select Follow > TCP Stream. We can now see the red section that shows the GET request from the client at 192.168.56.1, and the blue section that shows the OK 200 response from the server at 192.168.56.111, and then the file contents are transferred to the client.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/070d30a0225b306b2b02885ec6ffe95fe8cd05c74fcefc911791300f69809f935f818148263e00617c8fb414aec2.png)

---

**Question 7 - PCAP 2 - What is the source port (server) and destination port (client) for the file download?**

Continuing on from Q6 we'll select the packet where the server provides a 200 and sends the content of the ZIP to the client (if you've lost the packet go to File > Export > HTTP > click on the ZIP entry to select it, then close the popup window).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7d4ded8503a0a53e9a0d07bc89eff0a47c0d30c878bfffcb713cee9d4005e6f81bfa8b44f952fe1de539d0b1618e.png)

In the above screenshot we can see within the TCP layer the source (server) and destination port (client).

---

**Question 8 - What is the filename of the downloaded zip file?**

Based on the analysis we've done in the previous 2 questions, we know that filename is cr4ckx0r.zip.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/31763f84159f1047154c0d899e6c310da7eb7fcde7bb08200d06efa6057494d18ea4d14c3bc7336690510e0577d4.png)

---

**Question 9 - PCAP 2 - Export the ZIP file and save it to your system. What are the first 5 characters of the MD5 hash value of the ZIP file?**

Using File > Export > HTTP, then saving cr4ckx0r.zip to the Desktop we can open a terminal, use `**bash**` to get a bash shell, then run `**md5sum cr4ckx0r.zip**` to get the hash value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6da2bc317a861bc5cfbd52190365d7b1e52fe6103c0597c4136b81649af17a0c56782bf9f48921adfd8e6e4aee57.png)

---

**Question 10 - PCAP 2 - What is the name of the file inside the ZIP? (without file extension)**

We can view the files inside the ZIP by simply double-clicking the ZIP icon which will open it in xarchiver. We can see that the file inside is named ‘hashcat', a popular offensive/auditing tool used to crack hashes and passwords to reveal the plaintext versions.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7befebb15793c9e4e281f4868f1ae8137d21837474bc01de524f4417df59658141676484a213fe34c72ddbee38f6.png)

---

**Question 11 - PCAP 2 - What are the first 5 characters of the MD5 hash value of the file inside the ZIP?**

We can extract the file by right-clicking the ZIP icon and selecting ‘Extract Here’ to save it to the Desktop. We'll then open a terminal, type `**bash**`, then use `**md5sum hashcat**` to get the answer we need.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5db6f94771c325e876a933c39f8ad8d34997ab54c6f0053b8df9fd3c43cdace31e6332baaeabf6d459bde58e6178.png)

---

**Question 12 - PCAP 3 - What IP address is running an FTP server?**

Moving to PCAP3, to look only at FTP traffic we'll use the filter `**ftp**` to remove any unrelated noise. We're looking for the server's IP address, so we need to pay attention to the Info column to understand what's happening, and then use the Source and Destination columns to get the server IP.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e5e8bb9a9565434961153e975ce0c0d2c2eb43b83e9016f16946c795eedb3e220bf001afd0aaad93c954a64ab462.png)

In the above screenshot we can see a number of FTP packets containing `**Response: 220**`. In the screenshot below we can expand the FTP section and get more information about what the 220 response code means.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/90675813dd3258b0b95c7eececc71a265fa04a184a55c6ae3bdadade9095c095a4d905e9306fedb7d5c2a4641b56.png)

So know we know that this packet represents the FTP server sending a response message to a client that is attempting to initiate a connection. From this information we know that the source IP must be the server, because it is sending responses to requests. The FTP server IP is 192.168.56.118.

---

**Question 13 - PCAP 3 - At what time does the attacker send the first password in a dictionary attack against the FTP server?**

Scrolling down the packets with our ftp filter still applied, we'll come across packets that contain ‘PASS’ followed by a value, which represents a password submitted to the server.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/be619ab510adedab2d1df03b856ebff58eaeef16cdebc5d1778f0c18c044e13b9c3e967fddf868d48e88ab9c2faf.png)

But, looking at the Time column, we can see the value is 0.46195… - this value is the time elapsed since the first packet was captured. As the question is asking for the time in the format YYYY-MM-DD HH:MM:SS we need to change how this column is formatted. We'll do this by going to `**View > Time Display Format > Date and Time of Day**` (first option at the top).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f31020402eca912ab1dd731688953d9fe4b5d994861e379fb1109dc68c7ff2e93c5a655dd3c4f86947844843e990.png)

Following the requested format, the answer is 2020-05-26 14:51:19.

---

**Question 14 - PCAP 3 - At what time does the attacker successfully log into the FTP server?**

Looking through the Info column, we can see a Response from the server, `**230 Login Successful**`. We can get the answer by looking at the Time column and matching the requested format of YYYY-MM-DD HH:MM:SS.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ff089ec39451053fefa64d061ba9e513ffe29a4e68b69d94eaed821ea2404ec52cd3e2145e3b46c243ea12b9010e.png)

---

**Question 15 - PCAP 3 - What credentials allowed the attacker to log into the FTP server?**

We can get the USER and PASS by looking at the packets previous to the 230 Login Successful, reading the Info column, or we can right-click the 230 Login Successful response and go to Follow > TCP Stream.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/28a3f831fade2897bb41fd7ec672ba7f989e8ebe0f35e6ad18c8fe9bb243749d918d6176a8632aaad2cecdea4489.png)

---

**Question 16 - PCAP 3 - What is the name of the file downloaded from the FTP server?**

The easiest way to see what actions were taken in an FTP session is to right-click a 230 Login Successful response and follow the TCP stream. Completing the same actions as we did for Q15, when we can see everything in the TCP stream window. In the below screenshot you can see the RETR command, an abbreviation for Retrieve, which tells the server to send the requested file to the client. We can see that the user Chris logged in to the server and downloaded password.backup.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5be072f499818f9e1a61d132b5c58c9ddc293ccd0fddaac039534ed092cc8005ec483287a1af8f7546439bdb1f58.png)

---

**Question 17 - PCAP 3 - At what time does the attacker send the request to download this file from the FTP server?**

Looking at the TCP Stream for the 230 Login Successful from the previous questions, we can actually click on the line that references ‘RETR’ which will take us to that packet in the PCAP. We can now close the Stream window and grab the Time value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5dce016ee6086c51e2d2ceaeecabf23b907ff88c735dea4b1d0ffdabda5996b07adecc4b9981634cb4444a7fcf40.png)