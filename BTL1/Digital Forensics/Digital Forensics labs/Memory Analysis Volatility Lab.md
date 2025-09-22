The first thing we're going to do is turn our shell into a Bash shell by simply typing ‘bash’. This will allow us to use functionality such as [Tab] autocomplete, using the up arrow to go to our previous commands, and more.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e9ca4a37050c1eeb90859484c9cc4cd608ec5126561a0be0ea57106b5b881fdc4e14130664389731a92eab6c999d.png)

Reading the Instructions tab of the lab provides us with the following information: ‘_vol.py is located in the root file system directory (/volatility/) - you should open a terminal in this location and call vol.py directly, providing the path to the memory dumps (/home/ubuntu/Desktop/Volatility Exercise/)_’

Using our open terminal session, we'll move to the volatility file using `cd /volatility/`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/470466dffd4570b83979aaee87a31c1d823f758b336dd4d21e879f94c64a7f9ad1e10641a68f20b878d6c8c8603a.png)

---

**Question 1 - memdump1.mem - Image identification 1 - In order to start a memory analysis with Volatility, the identification of the type of memory image is a mandatory step. Identify the suggested profile that you should use with that image (use the first one suggested by Volatility)**

To identify the profile we'll use the command `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump1.mem image info`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/258f17b0924c3947b538c68e0dd4b3e4c9d41237ad26e6b37dbdc72936356bfc1d127b95740a43e53a20e46e2598.png)

---

**Question 2 - memdump1.mem - Image identification 2 - How many processors are identified by Volatility?**

In the highlighted section we can see that the host system had 1 processor.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7133a3e73d0a4b81c2278e98f44f001ae6534070568603de4d162d9bbef3679f4395d4ef020e2eb083df6f8638ce.png)

---

**Question 3 - memdump1.mem - Image identification 3 - Identify the address value of the KDBG (short for _KDDEBUGGER_DATA64) structure that will be used by plugins, such as pslist and modules**

Looking at the line above the highlighted section in the screenshot from Question 2, we can see the KDBG address value.

---

**Question 4 - Generic Question - Process list 1 - What is the plugin command used within Volatility to list the processes of a system?**

This question is asking us what command-line argument we would use to list processes using Volatility. The answer is the ‘pslist' plugin.

---

**Question 5 - Generic Question - Process list 2 - What is the plugin command used within Volatility to view the process listing in tree form?**

This question is asking us what command-line argument we would use to list processes in a format that shows parent-child process relationships using Volatility. The answer is the ‘pstree’ plugin.

---

**Question 6 - memdump1.mem - Process list 3 - How many processes with the name "svchost.exe" are running in that system?**

To achieve this, we'll use the ‘pslist' plugin to list all processes that were running on the system at the time of the memory capture. As we're only interested in svchost.exe processes, we'll pipe our Volatility output into grep and search for lines containing svchost.exe, printing only these to the terminal. This command looks like this: `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump1.mem --profile=Win7SP1x64 pslist | grep “svchost.exe”`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9743343f25e626c65646b47832be22573798d6fe9a5dc75c66a5f34fbd37320d2ceb912bd69fdca3c63a843e1672.png)

By counting the number of svchost.exe occurrences, we get the answer. Alternatively, we can pipe the grep output to wordcount using the lines flag (-l) to count the number of occurrences that grep has identified: `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump1.mem --profile=Win7SP1x64 pslist | grep “svchost.exe” | wc -l`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/cc40cbe50ade09c47f427be5e35f43123f4a1638df411a9da61eae23f3d8ac04b2547ad637e801f61f62882752c0.png)

---

**Question 7 - memdump1.mem - Process list 4 - One of the svchost processes is malicious. What is the PID of the strange svchost.exe process?**

To provide us with more context than simply listing processes, we'll use the ‘pstree’ plugin to show parent-child relationships between processes. We can see that the first svchost.exe process creates a cmd.exe child process, where the ping command is used, because we can see the ping.exe process being used. This is definitely unusual activity!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/545be0170ad5167923528d8ed5c422f7bc8c1b88b6797d262fa225b4408e55dfa392e9ce795496b8426cdef15e03.png)

---

**Question 8 - memdump1.mem - Process list 5 - What is the command line of the process with PID 2352?**

Using the ‘cmdlist' plugin and pointing Volatility at the specific pid using the ‘-p’ flag, we can extract the command-line arguments this process was using. `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump1.mem --profile=Win7SP1x64 cmdline -p 2352`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/725a36255f0a0515bcc1d0aa7c9bcfdfb2b1d41d9d23114b3e2318aa258f630550a40c70e16717b7d1e3c9693a8e.png)

**For the next two questions, we'll be analyzing memdump2.mem instead.**

---

**Question 9 - memdump2.mem - Network connections - This memory dump correspond to a machine we suspect has been persistently infected by some type of malware. We need to identify the harmful IP related to the malware.**

For this question we're going to use the ‘netscan’ plugin and look for the presence of unusual Foreign Addresses (public IPs), especially those that are being connected to from unexpected processes. `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump2.mem --profile=Win7SP1x64 netscan`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/813314e08be09af2910ad3b54a29446722d7e695493fc79f5d001d09784c400062bdc0c2dac3cf16a91ac3084f54.png)

Looking at the bottom line of the output we can see that the process WINWORD.EXE (Microsoft Word) was communicating to the Foreign IP 65[.]111[.]166[.]58 on port 80 (HTTP). Based on knowledge of phishing attacks, this is very likely to be a malicious Word document macro that is downloading malicious software from the mentioned IP address over HTTP.

---

**Question 10 - memdump2.mem - Process dump - Dump the process with PID 2940 and calculate the MD5 hash. Submit the first 5 characters**

Using the ‘procdump’ plugin and providing the PID using -p, we can extract the file. We'll then use ‘md5sum’ to get the MD5 hash value. `python vol.py -f /home/ubuntu/Desktop/Volatility\ Exercise/memdump2.mem --profile=Win7SP1x64 procdump -p 2940`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eb4e8460c4b7155959d296b2bd195f71c82a726a3dfa1121e47f745a83fa474c76d90d752394511d807393480941.png)