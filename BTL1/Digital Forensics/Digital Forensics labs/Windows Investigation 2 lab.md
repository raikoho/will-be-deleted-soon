**Question 1 - What web browsers have been used by the employee, listed in alphabetical order? (Use simplified browser names)**

Firstly, we'll open Browser History Viewer (BHV) inside the Windows Investigation Two folder on the Desktop. Once it has loaded, we'll go to File > Load History.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5a24e8413213154e2d55474455cdaee04eaa18dc1ffbb2bb37eed78f22740c986503faabaeba2196adcd8aef1f86.PNG)

When we're prompted to load history capture, we'll click on the “…” button, and find the Capture folder.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/30b4e9a667391b8e7214aa0a8ba7ac4b47d0ed05fb7848b9cbb5c19d2dfec75d46b38b4095eb05ff77bcc36c3bd5.PNG)

Once BHV has imported the data, we can begin answering the questions!

On the first screen we can see the column on the far-right is titled ‘Web Browser (Profile)’. Using this we can identify the web browsers that have been used on the system. We simply need to read through the list and take note of the browser names. It's very important to note that there are 4 pages, which can be navigated using the arrows on the left-hand side of BHV. As the question is asking for simplified names, instead of ‘Edge Legacy’ we would enter ‘Edge’. We're also asked to provide them in alphabetical order, so we'll make sure we enter them correctly.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/32310ba5b570b3e527c09b89991bd4656e6530b926f48efb35fd052deb079c212dc25ed72e3e8a5763b2b423ad06.PNG)

---

**Question 2 - The company has a policy against employees visiting social media on corporate devices. What sites has the employee visited, listed alphabetically?**

To answer this question we need to focus on the ‘URL’ column, where we can see exactly what web resources have been visited by the user. This is a case of going through them all to identify the names of social media websites.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d1232cea6f1bb786622e46f29a0152fedf2a8c176c9cc185436ad2a54be3a920904bc64cf51f97c8ae59a8ae4b92.PNG)

If you're not sure whether a platform is considered social media or not, a quick Google search can help you understand. As an example:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1aa5fe99295a8878f2deca07b964ccf6db7a40c4301404bdf052628ef60cca62433d965f2d62b506c162d3c2a8be.PNG)

To help you answer this question, there are 5 sites that we deem to be classed as social media. Make sure to put them in alphabetical order! We accept multiple variations for this answer.

The correct answer is Discord, Facebook, Reddit, Twitter, YouTube.

---

**Question 3 - Looking at Cached Images at (UTC) 19/06/2020 12:12:10 with the filename "everything-in-one-place-scenario-base[1].png", what is the subject line of the third email?**

For this question we're provided a date to help us identify the file of interest. We have two ways to find this date, which is stored in the ‘Last Fetched’ column of the Cached Images tab of BHV.

- Option One - Click on the header for Last Fetched to change the results to show in time ascending or time descending order. If the timestamps are in order, it'll be easier for us to find the correct timestamp.
- Option Two - Use the ‘Filter by date’ section on the right-hand panel. For this lab all of the results are on the same day, however in a real-world scenario, there would most likely be days or weeks worth of data, so this feature would be useful to look at specific days of activity easily.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9e13c17213d4b1643f104849d4b84914cd35ceda3e8c9c8dde0a6cd39d12100cbe9f301fa2d873361951e1b523df.PNG)

Using the Last Fetched column, we find the right time and file (based on the Filename column).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d5b1693f47819cb23ccff09c4511acb74479295bc3efb4e2a9cc1276806201db6c95bbac9406e73b55c6d82110a5.PNG)

Looking at the bottom panel of BHV, if we select a file in the table, it will highlight the associated image. We can double-click the image to show it full size in a new window. Here we can get the answer to this question.

---

**Question 4 - What is the full URL of the music video the employee is listening to on Youtube?**

For this question we're going to head back to the Website History tab in the top left. Instead of searching through all of the URLs to find YouTube ones, we can use the ‘Filter by keyword’ search box in the top-right. If we type in YouTube, we'll only see URLs or Titles that include the string ‘youtube’.

After searching for this, we can quickly find the answer to the question.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d2b7999aa32870c459bb33f7c234151530801315bd8f5f1e5acb0965795b70a10d9c6fb64cbe83bf0c06b40d0ea3.PNG)

---

**Question 5 - What is the name of the malicious file that was downloaded by the employee?**

To approach this question, we have three primary methods:

- Option One - Manually review all URLs until we see URLs that end in a filename, highlighting a download URL (such as securityblue.team/downloads/file.exe). This method will be time-consuming depending on the volume of records, but you could also identify other activities of interest during the search.
- Option Two - We could utilize the ‘Filter by keyword’ search box to look for file extensions, searching for phrases such as ‘.zip’, ‘.exe’, and others. These searches will reduce noise from records that don't contain file names, but we would need to go through every file type until we find what we're looking for. If we forget to search for a file type, we might miss the related activity.
- Option Three - All downloaded files in BHV are prefixed with “file:///”. We can use this to see the name of the file, and where it was saved on the system. This is the quickest way, and once we have retrieved the filename, we can then use that in the search box to find where it was downloaded from!

Using option three and filtering by most recent Date Visited first, we find a ZIP file with an unusual name. This is definitely worth investigating further!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b1ea4ba61281d08b0e4e455cc575d2f7731dc73b35b7e74365927296923bbaacfda17448a99bf782b5d7ff1fb9d3.PNG)

---

**Question 6 - Based on the employee's browsing history around the time of the file download, what is the likely source of the malicious URL?**

Now that we've found the suspicious file, we can start to look deeper. While the URL that's hosting the file is interesting to us, looking back further in time we can understand exactly how they got there. Searching for the filename we can find the hosting URL.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e8d60e60b558ee781435cd69abdc761b766e34241c56e2e62f4d674f02ebd9bb9575833fa5fa0f35069faf22b2f7.PNG)

So we know that the user visited that URL and downloaded the file to their Desktop at 12:14:09. Let's clear all our filters by clicking on ‘Reset’ on the right-hand side. Next we'll use the Date Visited column to find the timestamp 19/06/2022 12:14:09, allowing us to see the records that occurred before this download event.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/97c0fa62eb6529af895244109fa1e9d5ae4eb0691799e6541f75a3fb67e57bbba98467989202fd2e6f43a22e3fd3.PNG)

Based on the information above, we can infer that the following journey was taken by the user:

- 1) User goes to Outlook's login page.
- 2) User successfully logs in and goes to their email inbox.
- 3) User downloads the zip file, most likely from an email in their inbox. The file is downloaded to their Desktop.

It's worth mentioning that we cannot be 100% sure that this activity represents a URL within an email, without actually having access to their inbox to confirm this finding. It is completely possible that the user logs in to their email account and then manually types in the URL within a browser to visit it. However, based on the information available to us, and the timestamps that are all very close together, the most likely explanation is a link within an email.

Therefore, the answer to this question will be the domain shown in the highlighted section 2.

---

**Question 7 - What is the domain name where the malware was downloaded from?**

Utilizing the process above, look at the **third** box. We see a strangely worded zip file being downloaded from the hxxp[://]secretbeauty[.]ge website.

**Disclaimer:** The website above is defanged for illustrative purposes. When submitting in the lab, the format should be **domain.tld** (non-defanged).