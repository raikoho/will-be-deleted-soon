There are some great places we can look to collect information, and potentially identify digital evidence. Some of these locations can also be great for using digital forensics skills during incident response. We will look at:

- **.bash_history**
- **Hidden files and directories**
- **Clear files and directories** (Desktop, Trash, Documents, Downloads)
- **Steganography**

---
## Bash History

#### **Location**

The file .bash_history resides in a user’s home file. Can you see it?

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/97eafcb7afc611e515ceb1cf1c054589564c2656f7f1a08df3f4fb47d56225f0ecf6ac8c8c64a8c887744bda37e5.png)

No – you can’t, and that’s because it’s hidden. Sort of. If we use the command `ls -a` instead of the usual `ls`, we see that we have identified additional hidden files.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/14561b149f0f90ac06fdda3b3f49f194186ebc2c2420d1c2bfcc4764f80fc7d6a5d9144585a03a19d445dcdc6f3c.png)

Files or directories that begin with “.” are not displayed using the conventional ls command, or in the graphical browser. This is used by system files, but can also be utilized by individuals to hide files (more on that in the next section).
#### **Why is it Interesting?**

This file includes a list of commands that have been run by the specific user. We have done two things in the below screenshot:

- The **LEFT** part of the terminal is the output of us printing the contents of `.bash_history` to the terminal.
- The **RIGHT** part of the terminal is us using the `history` command in the terminal.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ab0f13730df1d8576e0934ea4985a1fb6f364feaa402af06c3d9d75abca3cc0ef9e4c34b47a5fa69bbbe125b2708.png)
  
They’re the same, because the terminal is writing any commands to the .bash.history file. So what’s the point of reading the history file if we can just use the history command? Because users can execute the history -c command, which deleted all history from the terminal. On the right, when we run the history command again, it’s all gone.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0519b1e8754c2c45ba311b306af9cc471545042f46e89916b4ad0104f88df45350958b0c3acdc0437566d8ea985d.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7d9db71d9cd419af81911d2c5415dd491b9660c8e70e8273b87b44e016f001cece68f814d0a010ba3545a741b1a3.png)

But when we go back and read the history file using cat .bash_history we can see that we still have a record of the commands that have been executed!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/281de5a9ceabbe23a64960c0bdee6d704a64ae349bac00e9a36d53ac53a393fe22c29b30205070d0fa6b682676d7.png)

Looking at the above command history, we can see that this user has been launching some nmap scans, and has also been reading the `/etc/passwd` and `/etc/shadow` files, which we’ve covered previously. An important note, as you may have seen in the above screenshots, that some commands are missing. This is because the terminal where the commands were entered needs to be closed before the commands can be written to the history file!

---
## Hidden Files

As covered above, the bash_history file begins with a period “.” – and in Linux systems this results in the file being hidden from immediate view. While it’s not a fool-proof way of hiding files or directories, it could easily be missed as it’s hiding in plain sight. In the below screenshot we can see that this seemingly empty directory actually contains some hidden files, and other directories.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/abb9822efc0f94a836e0fe4d8004fbf29436885dab26eff64f27d4b537203346eddf517b71fc0c3823269d2d7c94.gif)

So what’s the difference between `ls` and `ls -a`?

- **ls = list directory contents**
- **ls -a = list directory contents and do not ignore entries starting with .**

So make sure to always be using `ls -a` where appropriate to ensure you don’t miss any files hidden using this very simple technique.

---
## Clear Files

Let’s start off by defining what we mean by “clear files”. These are any files that are accessible through standard means, such as the terminal or the graphical browser. This includes areas such as:

- **A user’s desktop**
- **A user’s default directories, including; Downloads, Music, Pictures, Public, Templates, Videos**
- **The Trash Bin**

These areas can simply be looked through normally using a terminal or file browser, and may contain useful files if the suspect hasn’t bothered to hide them. However, innocent-looking files can contain hidden data, which we will cover below.

---
## Steganography

“_The practice of concealing messages or information within other non-secret text or data.”_ An example of this would be having a text file that contains secret information, where the text file is actually hidden inside an innocent image file. If this image file was sent as an email attachment, the recipient would receive a normal image file. However, using the right tools, you can recover the hidden file. You can also insert hidden messages in the form of text strings within a file’s metadata. We suggest you read the following [short article](https://searchsecurity.techtarget.com/definition/steganography) that explains what steganography is, written by TechTarget. Steganography has been described as a counter-forensics technique, as it works to make data harder to find by hiding it in plain sight.

## **Hiding ZIP Files Inside Images**

Let’s go through an example where we want to hide a ZIP file inside an image file. On our Desktop we have a text file `secretmessage.txt`, the same text file but inside a ZIP container `secretmessage.zip`, and an image of a dog `Dog.jpg`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/229ac3520c77d0631daa338eeaecec9b64caae02a25a75c76f286364ae77c515e93a59058cc72c28137a90082c29.png)

Using the command `cat Dog.jpg secretmessage.zip > Dog2.jpg` we can insert the ZIP file into the image of a dog, creating a new file named Dog2.jpg!
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/737459da62145cb7caf30e1ba614eb822c79fd58e9497bdb57d477966d68150210a225eedfbb2458d1ca9272ddb1.png)

Without any technical knowledge, you’d just assume that this image is legitimate, and it can still be opened like a normal image file. But, if we use the `unzip` command on the image file, we’ll retrieve the files that were inside the hidden ZIP file.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9186bda72eeae91c45d899dc6899232e4818ac10c0ee2976bb123bd5f618eeb9964eb46be042e22fdd9e2c6e3ab3.png)![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/db621a6c39a969d734521671d6b2f7a35deb780ec0723eb2078b0765e3a56eea0d7ede36ef4ef3e71001df3ec9a1.png)
## Using Steghide to Hide and Retrieve Files

In a similar way to what we achieved with the `cat` command, we can do the same using Steghide, but this time we can password protect the file we’re hiding data inside, known as the cover file. We’re going to hide secretmessage(.txt) inside Dog.jpg using this tool. 
The command we want to use is 

`steghide embed -cf Dog.jpg -ef secretmessage`.

- **steghide** – summons the tool we want to use
- **embed** – selects the operation we want to use, in this case embedding a file in another
- **-cf Dog.jpg** – the ‘cover file’ flag is where we state the file that will hold the hidden file
- **-ef secretmessage** – the ’embed file’ flag is where we state the file we want to hide inside the cover file

Once we’ve entered this command, we’ll be prompted to enter a password, we’re going to press [Enter] twice to not use a password.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/003695c1310eedf2380d4643b00dce68ef477bd46978b97cc5a03e67386ff4c41b6d1ccee7312113c0b54c24a908.gif)

Great, it worked! Now let’s delete secretmessage and try to recover the copy we hid inside Dog.jpg. We want to use the command `steghide extract -sf Dog.jpg`.

- **steghide** – summons the tool
- **extract** – selects the extract operation
- **-sf Dog.jpg** – the ‘steganography file’ flag is used to tell steghide which file we believe contains data hidden via steganography, which is our cover file from above.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8d82e9ab1f9823094b714c884ed0ae50f6799035a3a3c1d18ffbe9050eb93a2995ff7ef145d272fbfdd46a7bdb63.gif)

Obviously hiding files in this method with passwords makes it harder for forensic investigators, as they’ll need to know or retrieve a valid password to retrieve the file. But tools exist that allow for the brute forcing of passwords to recover hidden files, such as [https://github.com/Paradoxis/StegCracker.](https://github.com/Paradoxis/StegCracker)
## Hiding Strings in Metadata

Another way to hide information is to insert text strings into the metadata of a file. We can embed and extract strings using a tool called ExifTool. Run the command `exiftool` on your Kali system, if it is not found, use the following command to install it: `sudo apt-get install exiftool`. 

We’re going to embed the phrase “Super Sneaky!” into the metadata of Dog.jpg using the command 

`exiftool -Comment="Super Sneaky!" Dog.jpg`

Below you can see that when the command has completed it will generate a new file using the name of the original file, and replacing the original with `<filename><.extension<+_original>`, in our case the original file is renamed to `Dog.jpg_original`.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/38f8901434b9000480e38f1970b8accbe8bec613e819f4974cd04aa0380f6a7e53179a5b0b615328ee1f6ac61bd4.png)

Now if we use exiftool on the new file, Dog.jpg, we can view all the metadata from this file, including the new comment we just added.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a5caa2608f52ff542ceb0e98c68e1f6e25d38f1c4a8d628bd3280b8311d9ed4dc217c86bdc94e51fb318646ae5da.gif)

To add a few more seconds to an investigator's day, this text string could be encoded in formats such as Base64 or Hexadecimal to make it less immediately obvious.