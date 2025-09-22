This lesson provides a step-by-step guide on how we would approach this situation and answer all the questions!

---

**Question 1 - Analyze the .LNK files in the Shortcuts folder using Windows File Analyzer - What is the full file name of the PlagueRat file?**

Open Windows File Analyzer by right-clicking it and selecting ‘Run as Administrator’ `(C:\\Users\\BTLOTest\\Desktop\\Windows Investigation One\\WFA.exe)`, then choose **File** > **Analyze Shortcuts...** and choose **C:\\Users\\BTLOTest\\Desktop\\Windows Investigation One\\Shortcuts** folder.

Next, look a the row (marked in ==**red**==) and look at the file name (marked in ==**yellow**==).

We can see that ‘Plaguerat' is found in the Filename column. Looking along the row we find lots of useful information.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/377d6c38d33e0e479f7b2d71d1cafd0be7efa102f38bb10f3c1e954455ae323a76bef22a338988b070514f32b767.png)

---

**Question 2 - Analyze the .LNK files in the Shortcuts folder using Windows File Analyzer - What is the name of the ZIP file that PlagueRat was found in?**

Keep WFA open and look a the row (marked in ==**red**==) and look at the file name (marked in ==**yellow**==). We can see that this file was previously stored in the following ZIP file.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8db35051debddfbbade4cb0179daac350b18baddd2e453e8556eb8a2516c5cdf24959e556cbbe1843c6b6a6a82d1.png)

---

**Question 3 - Analyze the .LNK files in the Shortcuts folder using Windows File Analyzer - What other file or files were in the ZIP file?**

Keep WFA open and look a the row (marked in ==**red**==) and look at the file name (marked in ==**yellow**==). Looking at the Linked path column we can see another file that has the same file path, telling us it was in the same ZIP.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5a4dc07db241e67895b063ba5d1f41d8278b6cce17ec746bb3fe02812e72f8048f9df1b5b1787e1215609f600cd9.png)

---

**Question 4 - Analyze the Prefetch files using PECmd.exe - What is the full file name of the PlagueRat file in CMD.EXE-89305D47.pf?**

Open a command prompt and move to the location of PECmd.exe using `cd "C:\Users\BTLOTest\Desktop\Windows Investigation One\PECmd\"` , then run the following command:

`PECmd.exe -f "C:\Users\BTLOTest\Desktop\Windows Investigation One\Prefetch\CMD.EXE-89305D47.pf"`  

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d5382da18f1538f312576f73ff188044845b639a73b27eae71b269d177f3e5e8ca165550e63c1bf86684673fe6a9.png)

Look for PLAGUERAT in the output on Line 13, where the file is found with the extension ‘.bat’ - a batch script file.  

---

**Question 5 - Analyze the Prefetch files using PECmd.exe - What is the full file path of the PlagueRat file in CMD.EXE-89305D47.pf? (Starting with \USERS\)**

Using the above screenshot from Q4 we can see the full file path listed on Line 13.

---

**Question 6 - Analyze the Prefetch files using PECmd.exe - Open all .pf files by pointing PECmd at the /prefetch/ directory using the -d flag. Add the following to your command -k "plaguerat.ps1" to highlight rows that mention this string in red - What two applications were used to open PlagueRat.ps1?**

Open a command prompt and move to the location of PECmd.exe, then run the following command:

`PECmd.exe -k “plaguerat.ps1” -d "C:\Users\BTLOTest\Desktop\Windows Investigation One\Prefetch\"`

Because we've used the -k flag to highlight string matches (PECmd.exe will also match certain strings by default, so not every red-highlighted line will be relevant to us) we can look for red lines to see if they contain ‘plaguerat.ps1’ or not. Going from the bottom of the output upwards we can find our first match:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b800388979620efa5ee3acc27c22cd6486f513a07d7c8d4d54bf29848b0e5602602f3916dc7b0d364a7ea85716a6.png)

Scrolling up, we find what prefetch file, and therefore the executable name, that interacted with our suspicious file:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7f90241e4473ad042767f90cc7f080f79de324513808ee63891fb5eee113cc15401c1f64181379b578dc82219475.png)

Going up again, we find another result:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/54129d4ce3792545467f462fccfbf2e49139fdd2d7b1517518ce57406d3d8aa51440669e3a77be425c844bb0e75c.png)

Finding the top of this section, we can find the executable that ran it:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d79af53fca0ed21865549d71ec2320ee1c00bf19a61f58d2196f2c25200f8fec82e158b5c4a306250b2ec0c14e32.png)

---

**Question 7 - Analyze the Jump List using JumpList Explorer.exe - Find the website that was accessed by the user. What is the domain they visited?**

Since we are looking for a website, the best thing to look for is a browser. There are two entries for Microsoft Edge. In the bottom left panel we can see that a visited website is listed.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e1f647214ddc6af5e3c8328416f5c5ff837823e1d129a8b7c12805ef361c599f664e347e50ff99ebd2548eb82c35.png)

---

**Question 8 - Analyze the Jump List using JumpList Explorer.exe - What browser was used to access this site?**

Based on the previous question, we know this was Microsoft Edge, or Edge.