# Visualization Tools

This lesson will cover tools we can use to visualize a malicious URL without actually having to visit the site, as it could be highly malicious. The tools we’re going to cover are URL2PNG and URLScan.
#### URL2PNG

URL2PNG is my go-to tool for visualization. You simply enter in a URL, hit go, and it’ll provide you with a screenshot of what the webpage looks like. Let’s go through a couple of examples. The screenshot below shows me entering a malicious URL for a real-world Outlook Web Access credential harvester into the tool:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/96948c32cd7d9154559f704554b5d290a3f4e409b9810180d8da08541d5c0a4aa2c0b72d4fe46fca0df6ed9a820b.png)
#### URLScan

URLScan, amongst other information this tool gathers on a searched URL, has the ability to provide a screenshot. In this example, you can see a screenshot has been taken on the right-hand side, allowing us to see what the destination web page looks like. In this case, it is an Outlook Web App credential harvester.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0b7ff456127eb24e09bde4a218733da2ea3b78d204a513c744ab4a967a221d9befcd680ca4d7d6379309a14d935e.png)

-----
# URL Reputation Tools

This will cover how to perform reputation checks for potentially malicious URLs, helping us to decide if they are actually malicious or not.
#### VirusTotal

Head over to VirusTotal and you’ll be met with the simple web GUI. Click on the URL tab, and you’ll see the same as the below screenshot. Here we can enter malicious URLs to retrieve reputation scores.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ff16c2227a3f43843a845af4b9cf1d058ab26b2f9402c14b56c51de62d8079e179096a7bc9de098bfcca03486933.png)
Now I’m going to enter in a URL that I know goes to a live Outlook credential harvester. We can see that the URL has been recognized as malicious by a number of vendors, including Kaspersky, ESET, and Fortinet.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8cfca44a7e9dfa52c4fa6e6d1fcf743d07b89015a7c615bb724d3f4f885d4b1cf01d51c11d3febf5c26dfec57e8a.png)
#### URLScan

URLScan is a service that can provide us with **tons** of information about a URL. To walk you through this tool, we’re going to enter the same URL that we just saw was flagged as malicious on VirusTotal.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/aef22dacb89f1e88a088f075095398549d02c10770352226b34f3e8f5d7c80e887659dcbac3390170e53c2b3ae53.png)

As you can see, we’ve been presented with so much useful information. From a reputation score to a screenshot, web technologies are used on the site to the domain and IP information.
#### Threat Feeds

There are a number of public threat feeds that can provide security teams with intelligence regarding phishing attacks and malicious artifacts that can be used to power blacklists for email security products.

Firstly, let’s look at the [URLhaus Database](https://urlhaus.abuse.ch/browse/), a huge collection of malicious URLs reported by researchers. In this screenshot, you can see the date the URL was added to the database, the malicious URL, the status showing whether this resource is still available on the internet or not, and tags that show at a glance what the malware is (in these URLs we can see they’re hosting Quakbot), and the final column shows which user reported these URLs.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0e0d0fac0ecb9a417993325554e6600ed920a20cd6f53eb32517be297e3e4ea236cde343fd1cdf08001c94352c3a.png)

URLhaus offers a number of [threat feeds](https://urlhaus.abuse.ch/feeds/) that can provide specific information, and as mentioned above can be used to generate blacklists of malicious URLs that can be blocked proactively to prevent users from visiting these known malicious sites.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/66831a090130b0aa75580239200e8c158debe0e101b59c2d810329739582afe6405df4759d1e657a405434fbd3e7.png)

[PhishTank](https://www.phishtank.com/) operates like URLhaus and allows users to submit phishing artifacts which are then verified by the wider community. In the below screenshot you can see what looks like the URLhaus database.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/411c4d90d29e55fc4151ecf18fc073c10ab44b1740e55c5c97fa0d63d29389ca81b6ea55b82b20f617681a5447e5.png)

-----

# File Reputation Tools

will show you a couple of the many online services where you can upload suspicious attachments or their associated hashes in order to see their reputation within the security community.
#### VirusTotal

The feature we’re interested in is the file upload function, where you can upload any kind of file to see more information about it.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/41a5af172b4c432e73d3b5bf7a19614cf63078e71b516d009a848484e3bb54767b742d737238bad3c3d487bbcc10.png)

In this example, we’re going to upload an old piece of malware, which we know will be detected by a number of security vendors – this will allow you to see what malicious files look like once they’ve been submitted for analysis. 
In the below screenshot you can see that 63/72 vendors have detected this file to be malicious. In the top bar, it tells us that the file size is 402.33 KB and is a .exe file. 
If you upload a file that has even a few engines/vendors in red, then the file is most likely malicious in nature and defensive measures should be put in place (we’ll cover this later).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/abc578134a50d96a45a2232aceabf080a296613dee834024f0cc4f225412bd30fa3eacd32ccda95174d8b91cd7e9.png)
#### Talos File Reputation

This service allows us to search for **SHA256** strings against their reputation database to determine if it has been classed as malicious by their products: AMP, FirePower, ClamAV, and open-source Snort product lines. 
This database of information is called the “Talos File Reputation system”.

In the previous lesson, I covered how to retrieve file hashes in both Windows and Linux operating systems. So I’ll generate a SHA256 hash using PowerShell on my Windows host, and plug that into Talos File Reputation. 
I’m using the same piece of malware that I submitted to VirusTotal, so we’re expecting to see that it is recognized as malicious straight away.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b2cb1785933c687ecc47801e9f2646cebb7b9ded7cf00d3cc7cf930e6a46263be0a34a706e38fbaa926b547147f6.png)

_Using PowerShell on Windows to get the SHA256 hash using the “get-filehash” command with the “-algorithm sha256” switch._
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/da47e8bd2ce3aa9b7d61fe1a7fef0fce915bf933c44fbe501395688ea3529c6b5c67f186bfd1614be7783e2f6790.png)

_Using Linux Command Line to get the SHA256 hash using the “sha256sum” command._
  
Now that we’ve retrieved the SHA256 hash value we can upload it to TFR to check the reputation of the file. The results clearly show that this file is malicious, with a score of 100 (left side). We are also provided with the file size, the type of file, the name used for detection, and other aliases used to track this specific piece of malware.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/768c669330fc59cc14358a0ebfe670bd825a4f30037d3a4a510a6bc4d7b4658c38cb1eba71784f1bfd5642988e98.png)

----
# Malware Sandboxing

Sandboxing is the process of detonating (running/executing) a piece of malware in a contained environment, and closely monitoring exactly what the software does, allowing security teams to collect indicators of compromise
#### Hybrid Analysis

Hybrid Analysis is an online malware analysis platform that lets you upload malware for instant cloud-based analysis, providing you with a detailed report about the observed activity.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5a2b7422867f1bf41f5e0982dbf133df6ec84b31f3bb4fbf0d1eb2d83ee6bc48b4128b5c767fb5f67cac26cdb4ac.png)

First, navigate to the Hybrid Analysis website. Here you can drag-and-drop, or browse for the file you want to upload.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/163462ffffcdb44083cb4fd0f34266c9bf0e4d43b46cf272a6ccfeef4b10ded3d708f18e859daaeaa2864a75ae5c.png)

Next, you can choose the operating system that you want to detonate the malware on – this is perfect for malware that only targets specific operating systems. For this activity, we’ll just use the default Windows virtual machine.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9eed6ad9d9a624492e896bb64f2ea2a035341885d42337865e1743af5043e1476bf27fc35c736fc0b88d1dee8c83.png)

Once you’ve clicked “Generate Public Report” you will be directed to the report page once the analysis has been completed. You can see this below.
#### Analysis Results

Below is a screenshot of the results provided by Hybrid Analysis after we uploaded the piece of known malware. You can also view the report yourself here – [https://www.hybrid-analysis.com/sample/240387329dee4f03f98a89a2feff9bf30dcba61fcf614cdac24129da54442762](https://www.hybrid-analysis.com/sample/240387329dee4f03f98a89a2feff9bf30dcba61fcf614cdac24129da54442762)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/980fe647578a7a24a09022111b1c85c66f190632f5c9d436cdc0004f0a72331a8d838a997dc844c05ae98cf80b55.png)

---------
# Automated Artifact Analysis

you can analyze artifacts from the PhishTool analysis console, including: WHOIS checks, VirusTotal reputation checks for MD5 hashes and URLs, and URL visualization.

### File Artifact Analysis

PhishTool will automatically retrieve the file name and MD5 hash from any email attachments, and the console has a button that allows us to search for the hash value in VirusTotal straight from the console. If the submitted email contains an attachment, click the following button on the right-hand side to submit it for a reputation check.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6b9dc59c3f7cf88e68bf1c532425181db985cc0621c64fcdf533278522d1fce510bcc86aa36d9508a9d885503cad.png)

This will automatically generate a VirusTotal search query for the MD5 file hash and open it in a new browser window.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/912dc6a64ffafa3f9892c43e0d1e141735e44204d414e44a040e31fe35f55b707d05e7558da7ea92ac21fbfc2681.png)

### Web Artifact Analysis

Similar to how we use URL2PNG to visualize what is at the end of a URL, PhishTool has the ability to generate a live screenshot of a URL. If an email is submitted to PhishTool that includes any URLs, whether malicious or not, a web capture can be viewed by clicking on the URL and selecting Web Capture.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c4c11e7552194a744798ea3b5e70eb3e9a6f70644ffcec1ce0a0470370301c460518e4fe45f40927befead8492ff.png)

This feature also kindly provides us with the HTTP requests made, and headers from the site.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8fab708a9e1416b367d80fd3ef277f81911878b588fce0d8523f8de3c6acb6253a4e1cabdc5e6e8fb93d9cfaf0c9.png)

Another analysis activity we can perform from within the PhishTool console is a WHOIS lookup, providing us with information about the domain such as where it’s hosted, who owns the domain, how long it has been alive for, and contact information. Let’s try a WHOIS search on a different URL from another phishing email.

  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/43e4892033a887d0aa6ab4ad8cef889e6232045e58d606310ab918555a75287d90a5ac20f3da3f16666dc771d3ae.png)

Below is the sidebar that will come from the right-hand side of the analysis console, and provides us with valuable WHOIS data. From this we can see that the domain has been alive for 2643 days, the domain name was registered with Domain.com LLC, and we have some contact email addresses.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ae1a2d44c46c19785d5e3d7904d89890756b7898f8fa8a10f8cd5ccf8fb1882ad433ab69dab92c74b2d5567d8d8d.png)