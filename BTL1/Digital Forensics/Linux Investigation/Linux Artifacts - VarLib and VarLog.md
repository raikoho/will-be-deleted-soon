In this lesson we’re going to cover two locations that may be of interest to forensic investigators, `/var/lib` and `/var/log`.

## var/lib

### Installed Software and Packaging

On Debian-based systems, we can find a very useful file at the following location: `/var/lib/dpkg/status`. This file includes a list of all installed software packages, and can be a gold mine if you’re looking to see what programs the user has installed to the system. Let’s take a copy of this file and move it to our desktop, and then open it in a text editor, and see what installed applications we can find!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/049e2a623da96353b7ee3b2e51f7ceec42bea50bb678972560ad08af1044108dfd18c1f34c9be839fe648adeb0f9.png)

In the below GIF you can see that we’ve opened the `status` file, and searched for some different programs. We would see that this system has the following installed:

- **steghide**
- **exiftool**
- **nikto**

If forensic investigators or incident responders were looking for specific packages, they could use the search functionality (CTRL + F) to search for what they need.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a5dd99b693a677629162be549822b4375b67f3911ef906237b878162f392dcaf2f9a50cf7285c7b22c33841c172b.gif)

Alternatively, we could open the file in a terminal, take every line that contains `Package` (as we know this holds the package name), and save this to a text file so we can look at it without the noise of all the extra package details. The command for this would be:

`cat status | grep Package > packages.txt`

- cat status will read the file.
- grep Package will search for any lines containing ‘Package’
- > packages.txt will output the results to a text file called packages.txt

---
## var/log

The log files present in this directory are sometimes dependent on the linux-based operating system that is being used, so you may not see all of these listed below. We're focusing on the main ones that are relevant to us as cybersecurity professionals, and that provide us with useful information and artifacts, however there are lots more out there.

### Operating System Logs

1. **/var/log/auth.log** – Contains system authentication information, including user logins.  
    ![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d334a78e3f10942aa70f8c93855db0b9f8ae0bb97834cbec73c33a9b3d9bc74336f8057286fb4f8d49e50fc4b8c8.png)
2. **/var/log/dpkg.log** – Contains information that is logged when a package is installed or removed using the ‘dpkg’ command. This is similar to the packages command from the var/lib section above.  
    ![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/278766abf71b4e40c0dd1881bcdf02afe7d4284c5b4576201c8709cbe67cff785429ddeb14d6ca120111aca067d5.png)
3. **/var/log/btmp** – This file contains information about failed login attempts.
4. **/var/log/cron** – Whenever the cron daemon starts a cron job, it logs the information about the cron job in this file. [This is useful because cron jobs can be abused for persistence on a system](https://attack.mitre.org/techniques/T1053/003/).
5. **/var/log/secure** – Contains information related to authentication and authorization privileges. For example, sshd (the daemon used for the SSH service) logs all the messages here, including unsuccessful login attempts.
6. **/var/log/faillog** – Contains user failed login attempts.

### Web Server Logs

Linux-based systems are often used to run web server frameworks, such as Apache and Nginx. Focusing on Apache, we can find an extremely useful log in 'var/log/apache2/access.'log' that provides us with information about requests made to the web server including values such as:

- The client IP address making the request
- The resource they are trying to access
- The HTTP method, which will most often be GET (to get a resource, such as images in a web page)
- The user-agent used by the client IP (this should typically be a browser user-agent, such as Chrome, Firefox, etc)
- and the timestamp of the request

Let's look at an example.

`52.50.100.106 - SBTUser [27/Jul/2020:15:30:00 -0600] "GET /logo.png HTTP/1.1" 200 379`

1. 52.50.100.106 - The IP address of the client making the request to the web server
2. SBTUser - The userid of the account making the request (if they are logged in and the website is using accounts)
3. [27/Jul/2020:15:30:00 -0600] - The timestamp of the request
4. “GET /logo.png HTTP/1.1” - The resource that is being accessed, in this case the IP is retrieving the logo image file so it can be displayed on a page
5. 200 - The HTTP response code. In this case it is 200 OK (successfully accessed). In other cases it might be 404 if the resource isn't found.
6. 379 - The size of the file sent to the client (in this case, the size of logo.png)

We can perform analysis on these access logs to identify activity such as vulnerability scanning, exploitation, and more!

In the below screenshot below you can see some real-world examples of Apache access log entries.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e364ecb8a3b2bfcb02b4da5426277d41aef55acff7e3658a20eb9cc307b8b7ce138812b328a2003505bf8b14ff01.png)