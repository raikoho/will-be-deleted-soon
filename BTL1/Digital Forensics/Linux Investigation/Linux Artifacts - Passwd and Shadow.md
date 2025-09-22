## What are ‘/etc/passwd’ and ‘/etc/shadow’?

Traditionally, the **/etc/passwd** file is used to keep track of every registered user that has access to a system. All users will have read access, but only super users will have the ability to write to the file. Why is this useful? Because it gives us information about every user on the system. In a forensic investigation maybe the user has a secret second user account that they have disguised to look like a service account, or maybe during an incident response, an attacker gained access to this Linux system and created an additional account for persistence.

Below is a screenshot of the passwd file on our Kali Linux virtual machine. We can see our account “root” at the top on the second line, with a lot of other entries below. These are all service accounts created by different programs to manage and run daemons. You can see how a second user account could get lost in all of this mess, and identifying it could uncover a lot of digital evidence.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a8383f8f5d484e587c992dbb143735fcb7a167fb9e51d73acdacbeff95307bbbbd366519f6565f926faf5e10519b.png)

On the second line where we have our current user “root” we can see an X next to the username. This is the account password. Well, it’s really just a variable, because the password is encrypted, and stored somewhere else. The second file we’re going to cover, called `/etc/shadow`, contains encrypted passwords as well as other information such as account or password expiration values. The **/etc/shadow** file is readable only by the root account to prevent standard users from grabbing the contents and then using a tool such as hashcat or John The Ripper to brute force, perform a dictionary attack, or use rainbow tables to crack the hashes and reveal the plaintext passwords.

Let’s read the contents of this file using `sudo cat /etc/shadow`. We can see that next to our root account there’s an encrypted password value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/283d7967c1ddbfa0dc5893bf3a88c0f592041e9eb6bade95d8267f5c940ab4046f866e3abcee993c005536cd7fd6.png)

The **/etc/passwd** file stores user account information such as the **username**, **user ID**, **group ID**, **home directory**, and **login shell**. This information is essential for determining which users have access to the system and their level of privileges. The file is often used to identify which accounts have been created or deleted and when they were last modified.