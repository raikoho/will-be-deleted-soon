I used:

`RBCmd.exe -d "C:\$Recycle.Bin" --csv "C:\Users\BTLOTest\Desktop"`

**Question 1) What is the FileName value of the largest deleted file detected?**

First, we'll type CMD into the Windows menu and right-click it to run as Administrator. We'll then cd into the Recycle Bin directory.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5c4d97bdb26665b60ad43698adbf9a16fbffd0832f60136bebc14195f3080ec40974e3efc73c167d37f8f3241639.png)

Next we'll run RBCmd using the following command:

`C:\Users\BTLOTest\Desktop\Recycle-Bin-Analysis\Tools\RBCmd.exe -d . --csv C:\Users\BTLOTest\Desktop\`

This will run RBCmd.exe in the Recycle Bin directory, and generate a CSV inside an output folder on our Desktop called “Output”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b884d36a88540b8d1cfac6d9dd859fad741b56f82d806594c3c1bb93a7f41ace74d8deaf70fb20824491483c1130.png)

Next we'll open the CSVQuickViewer application from the folder on the Desktop.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d3571a279386e9477917196543fbc05d23dcae08051606d89bb0090fd9c128fd27be46b2fa908fb73b3bd6cdb4e0.png)

If we receive the Search for app in the Store? popup, we can just click Yes to launch the program anyway.

Click Open File in the top-left corner and select the CSV within the Output folder. We can now start to triage the results!

Clicking on the header for the FileSize column twice we can have the results ordered by highest-to-lowest, showing us the largest deleted file.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2cceddc2c3f46b4e45c5ad80bcea571950142d3b477c09945d5532dab194f83298bd32bee9da62a642782be62824.png)

---

**Question 2) Which user account had the most deleted files present in the Recycle Bin, and what was the total count?**

To get the answer for this one, we need to count the number of times a user account is present in the FileName column (as this is easier than counting SID occurrences). If you're still sorting FileSize from highest-to-lowest, click on the FileName header as this will filter this column and group results based on the filepath string, making it easier to read users by grouping them.

Simon.Leeves has the most deleted files with 8.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1ac8466a5f49f158693fc425696304fe7965b2eb7ac7065beb3f0d3cb4a5d82173950aaaf66cb4cd53460f459897.png)

---

**Question 3) At what time was the file "2023 Rebrand Design Brief.pdf" deleted?**

Looking for this file name in the FileName column, we can then identify the DeletedOn timestamp value.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6c988cdff4ec6be7a09c320d4dd7a07a17d75c9cd7c7dc71fb08921cf62183ccfe547367083d51c13782482b2438.png)

---

**Question 4) What user account deleted a file that was 542812 bytes in size?**

We can look for this value in the FileSize column, then use the FileName column to identify the user account.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ce463f3e87b2fc797e224c6522de82f031a8d36b1695ca63882c22eee2fa54c13f61c52968a80015dd98b52b5ca1.png)

---

**Question 5) Simon Leeves was accused of downloading confidential files, removing them from the database, then deleting his own copies. What are the names of the files that support this argument?**

There are two files that support this theory, based on the location at the time they were deleted (the /Downloads/ folder for this user account), and the expected file contents based on the filenames.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1728658239d8bcf1fcce600cf61ae895ac6a9aec0c0182192fcad4d7581e807f181b02f367715e611a0d65597d48.png)

---

**Question 6) How many deleted files have been identified in total?**

Counting up all of the result rows in CSVQuickViewer, there are 24 results.

---

**Question 7) What are the last 4 digits of Rick Ranchez's SID value? (Format: XXXX)**

Based off a result row that has Rick.Sanchez in the FileName column, we can assume his SID ends in 1013. Remember, we can check this using wmic if we wanted to!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4273063665106c353caaa32e2727b4c263e3134fbf81559eee0bce382b6e703a9d52c1a40e14da4aaf17bca33307.png)