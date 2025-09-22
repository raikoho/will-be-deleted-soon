After opening Autopsy, found within the ‘Autopsy For Disk Analsis’ folder on the Desktop, we'll be asked if we want to open a case, or create a new one - click on Create New Case. You'll be asked to provide some information, you can name the case anything you want.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/13f9edd4c729e15c595cd2199e6b0703a01ea836299bca63ea0a331650403e02f938a0fa6a2451565acf51858b21.PNG)

We need to select a Base Directory for our investigation, which needs to be an empty folder. Click on Browse, go to the Desktop, then click the icon in the top-right to create a new folder.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5d34bf297cfe83965d5c7a803acd1395d0646ab8227c9d40ee611cc9760be7c11302f9d2c54a4e8f82df4c7416c1.PNG)

After clicking Next we'll have our case created within Autopsy. We need to click ‘Add Data Source’ in the top-left corner. When asked to select a host, leave it as the default option (first option) and click Next. We are now asked to import an image, leave it as the first option and browser to the Autopsy For Disk Analysis folder, then Laptop Image, and select the below file.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/39492c9e84c80f0c0fe6176f75eb3e7d357244565e64db93668175ff7206677fb2027603b2b9b3d097236523e788.PNG)

For Step 4 we're asked what Ingest Modules we want to run on the disk image, to help us quickly retrieve interesting information. Click Deselect All, and tick the two modules shown below.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fb2583fa8fe48aa217531565c9dae4f3ef077d811e0a8e573f5f72ea0a1b96387e1cd24152b913c9f6da00a6d9f6.PNG)

Autopsy will now begin importing and processing the disk image and ingest modules. Leave this to run for about 10 minutes, then you'll be ready to start answering the questions!

---

**Question 1 - What operating system (and version of OS) is the suspect laptop running?**

To find the Operating System of the device we can look under ‘Data Artifacts > Operating System Information’. Scrolling to the right within the table in the left panel, we can see the OS listed as ‘Program Name’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1be2a1be291a99f3c17fcd219bb8ea939f28492bfa453aae6dbcdb9ff706c20aded629a6fe86f2e3d2f364d3133b.PNG)

---

**Question 2 - What is the hostname of the system?**

On the same section as above, towards the left of the table, we can see the Hostname listed as ‘Name’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/86b49231cdca4045fb384a813423cfd8824b554d1a13992ec9ef4a292b44ac387bffafd8db54fe04a85f89e3f8ef.PNG)

---

**Question 3 - Look at Web Downloads that have been retrieved from the disk image. What file was downloaded at 2013-12-18 20:05:57 GMT?**

Still looking at the ‘Data Artifacts’ heading on the left panel, we have been asked to investigate Web Downloads. In the table on the right we can see ‘Date Accessed’, so we need to find the row that has the date from the timestamp in the question!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/98e263d93f3005b866b084c2d0ad0188c13ddb9bc854fdea5a3d6a321720039930ac5f82eb4a8489e13524c2b40f.PNG)

---

**Question 4 - What is the full URL of the file that was downloaded at 2013-12-18 03:02:50 GMT?**

Looking in the same location, we need to find the row in the table that matches the timestamp in the question. After finding it, we can see the full URL in the column titled ‘URL’.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fbed000932dc3e33e95733c1e60cad9bfa0c81a1e299283bc0cbadbd3f45ce6cd6b3d28003751ee56e47746e5257.PNG)

---

**Question 5 - Looking at Recent Documents, what is the full path for the file Pier.jpg?**

Remember LNK files, that we covered earlier in this domain? Files that are used as shortcuts to the real file located on disk. We can use LNK to identify when files have been accessed, and where they are stored. The sample applies here! Looking at the ‘Recent Documents’ menu item, we can find the Pier.lnk file, which is used to represent Pier.jpg - we can get the file path from the ‘Path’ column.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/cf87f0f201455b719ab993a4ce4e35372f076228bd4e338591ef614607688e65ca8902f24608bcd1f26ce575def7.PNG)

---

**Question 6 - Double click on vol2 to enter the virtual filesystem. Navigate to Program Files > GIMP 2. What is the file size of the directory named "lib"?**

Let's view the virtual file system, as if we were on the computer itself! Double-click on vol2, the largest partition within the filesystem.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e35f317e223a0c36ca9a7dc152987cf8843c0724b58442b5ccf542f0dac10faeba99d2625e349cc671ff9bd86e5b.PNG)

Moving to Program Files, GIMP 2, we can see the folder we're interested in. The file size is shown as a column at the end of the highlighted section!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/83c0a4401f11a2cd594e7ec40d723250bbf3a598cccc90449430ce33d655fb78a99605e57df29b18c2f8a380aa74.PNG)

---

**Question 7 - Go to the OS Accounts tab. When was the local administrator account last accessed? (Format: YYYY-MM-DD HH:MM:SS)**

Looking under the ‘OS Accounts’ section, we can see every local user that is on this computer. At the bottom we can see the Administrator account, giving us the time it was last accessed.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7c416bfdae41f2a64e72ec29580c5c90997afc79988bc143825a91e0556d2e30a0c9a85c5ebbd5187af93dd7d628.PNG)