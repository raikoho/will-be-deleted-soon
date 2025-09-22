![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/92bdfe8f7d26ea943108da0957590f5356867153f8992765e623ac7342e7231f6de4d1f4f7288b2b1380e76ddb63.jpg)

**Autopsy** is a forensic-grade tool that is used by the military, law enforcement, and corporate examiners to investigate what happened on a smartphone or a computer. 

Autopsy has a plug-in architecture that allows the user to find add-on modules or even develop custom modules written in Java or Python, providing additional functionality and automation. 
This awesome tool comes built-in with Kali Linux, and can also be downloaded and used on systems running the Windows operating system for free.
## Autopsy’s Main Features

- **Multi-User Cases:** Collaborate with your fellow examiners on large cases.
- **Keyword Search:** Text extraction and the index searched modules allow you to find the files which mention specific terms and find the regular expression patterns.
- **Timeline Analysis:** Displays system events in a graphical interface to help identify activity.
- **Web Artifacts:** Extracts web activity from common browsers to help identify user activity.
- **LNK File Analysis:** Identifies shortcuts and accessed documents.
- **Email Analysis:** Parses MBOX format messages, such as Thunderbird.
- **Registry Analysis:** Uses RegRipper to identify recently accessed documents and USB devices.
- **EXIF:** Extracts geolocation and camera information from JPEG files.
- **File Type Sorting:** Group files by their type to find all images or documents.
- **Media Playback:** View videos and images in the application and not require an external viewer.
- **Thumbnail viewer:** Displays thumbnail of images to help quick view pictures.
- **Robust File System Analysis:** Support for common file systems, including NTFS, FAT12/FAT16/FAT32/ExFAT, HFS+, ISO9660 (CD-ROM), Ext2/Ext3/Ext4, Yaffs2, and UFS from The Sleuth Kit.s.
- **Tags:** Tag files with arbitrary tag names, such as ‘bookmark’ or ‘suspicious’, and add comments.
- **Unicode Strings Extraction:** Extracts strings from unallocated space and unknown file types in many languages (Arabic, Chinese, Japanese, etc.).
- **File Type Detection** based on signatures and extension mismatch detection.
- **Interesting Files Module** will flag files and folders based on name and path.
- **Android Support:** Extracts data from SMS, call logs, contacts, Tango, Words with Friends, and more.

## Autopsy Walkthrough

### Starting a New Case – Importing a Data Source and Running Ingest Modules

Firstly we need to open Autopsy. When you’re presented with the below screen, click New Case.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/180d723ef89b9fb27432cbaae8d9c44362391ddd7f0bd0030c4c3a8f51a087f829c207b73ff928618dbb52de9d91.png)

Here we need to provide a name and a base directory to store all our files. We have selected the name “BTL1AutopsyWalkthrough” and saved it to a directory with the same name in our Document folder.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/1faa0dc77704213d2fdee325026ecbec06a597a770b1b97398882009ddbe685ff294827b53672541e18e35aaf574.png)

The next screen will ask us to input some optional information about the investigation. We don’t need to use this, but this is how security teams and law enforcement will add investigation-related metadata to Autopsy.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3cd1fd757e33ef5fbc2c65a525bf0951895dd31e27316202eef5b6d14fc52c4bc50acbf2559aa10a1af8ade02796.png)

Autopsy should then prompt us to add our Data Source, in this case, it is a disk image, so we need to select “Disk Image or VM File” and then click Next.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a063c6c89257631bf6f5825254b4630ef5e5da6420a7a669467b628d036169734192819394e056722e7a17c5af67.png)

We'll click Browse and select the .E01 disk image file we're using for this walkthrough, then click Next to add this as a data source for our investigation. Next we’ll be asked if we want to run any ingest modules, these are automated actions that can be conducted against a data source to retrieve information that is useful to the forensic examiner, saving them time. For this walkthrough we want to select “All Files, Directories, and Unallocated Space” from the drop-down menu, as this chooses the targets that ingest modules will be run against. Then you should select the following:

- Recent Activity
- File Type Identification
- Embedded File Extractor
- Exif Parser
- Email Parser
- Encryption Detection

Note that some of these ingest modules may change names!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/acbbd2a2822ab61a22d6f9074f07b02b4b750375feae59327a9c6d6ddc7ef77fdf3b0116c28b4789918025c60910.png)

In the bottom right corner you will see a progress bar that will let you know when each ingest module has been completed. Give Autopsy a few minutes to complete analysis of the data source. You should also notice that the values on the left-hand pane increase while the ingest modules are running, because they are discovering important information and placing it into the artifact tree to make it easy for the examiner to take a deeper look.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/f8cf0e75240def3a0fbe5e0db77dc82ac8a5ed4a9adcb5d3c2c7c818e004973bc85b2700ef0439186b8e275824be.png)
### Analyzing Ingest Module Results

By now all of the ingest modules should’ve completed, and you won’t see the progress bar in the bottom right corner of Autopsy. The navigation tree in the left pane should also have numbers next to the headings, showing that information has been found and sorted into different categories. Next we’ll walk you through some of the information that Autopsy has pulled from the hard drive image.

The first thing we want to look at are the volumes of the hardrive so we can collect information such as allocated and unallocated space, the size of these partitions, and the format or formats that are being used. At the top of the navigation tree click the + icon next to Data Sources, then the + icon next to Craig Tucker Desktop.E01, and you’ll be presented with three volumes; vol1, vol2, vol3.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4ad70e23ef7a24d39b2b658783e3812ff21263396f3b1f673a67d2bf7bd5cad46153f7ba25e2bfe535bb93b308e0.gif)

If we left-click on Craig Tucker Desktop.E01 in the navigation tree, the right-hand pane will now show information about the detected volumes. This is known as the Partition Table.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c84fff9b8d7b43b42e5b217ab7dfe8c50fd9c58fe6f884a881723aa1e952c77578922535ab9324a4fe29b1d0e27e.png)

In the above screenshot we can see that vol2 is formatted with NTFS / exFAT, and that it starts at sector 2048 and the length is 125825024. This is the main section of the hard drive, and is where the file structure sits. Everything from users to documents and downloads will be in this volume. If you double click vol2, we are presented with a read-only file structure so we can browse files as if we’re actually sat at the laptop!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/086233e0c6af9557146fd8feab71949b171b991e7b5e5abad996ff58869dbc69143038f9bc44419ea63787641d06.png)

Spend a minute playing around looking through the directories to see what you can find. It’s good to be familiar with navigating forensic images this way, as individuals that use Windows on a daily basis will likely be familiar with navigating the file structure.

Now that you’ve had a look around, it’s time to see the results of the ingest modules, which are located on the navigation tree under the **Results** heading, shown below.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2661942374aec7bd4667f073429f5518a05df3a16542ff9f214b03f86a38795e8da97cc257e86109c79e6f20fe5f.png)

Let’s look at a few of these results. To start, click on the Web History near the bottom. This will show us the sites that have been visited on the system including the date accessed, the page title if available, and the program that was used to access the web resource. For example, the highlighted line shows that a user has visited 4chan.org/rules via the Chrome browser on 2013-12-18 02:35 AM GMT.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/beba0fd2f910eff76cd59b87c658e39f9695ccaaf42bf4be363c9de0bb6f68337b8ff1e5cf8942d03c2db9e9a93b.png)

This is a great way to view the browsing habits and sites accessed by a suspect. Timestamps also help us to create a timeline of events that have occurred and can be used to prove that a user visited resources on a particular day, which could aid an investigation.

Now let’s see what files the user has deleted by going to the Recycle Bin in the navigation tree. On the right pane we can now see that the user has deleted three files, and we’re given their file paths, the user that deleted them, and the time the file was deleted. This can be a quick-win if we’re looking to identify files that have been deleted and gain information about them.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8d803dcd13a1bd0f3fff9257d39832d934d004ce2051bf4ba43fc4b5280a5dd4f8e9b18d4060031fa4cb3242c598.png)

We can actually export these files to look at them (this isn’t limited to files in the recycle bin, we can actually do this with any files identified in the disk image!). Right click the path for “Underage_lolita_r@ygold_001.jpg” **(don’t worry, this image isn’t anything explicit, this is just an example name for the investigation scenario)**.


![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ebd36cf300ebf76754a97cb1933f3836577feec31ca78e8380454dd06b3aa9c2a19ce1b801d90f945beb44e6d94c.png)

Select the destination that you want to export the file to, and go ahead and open it. Below is the image that we have just extracted from the disk image.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/992a82be00788abe2524ea0c3a2bd2b2809db000bcb5b72eb0fadd608c94c090bcdf45e0b74037826ed9fd17df0e.png)

This feature can be useful if the investigation was regarding child exploitation, allowing the forensic examiners to identify potentially explicit images, export them, and confirm whether the material can be used as evidence in a legal prosecution against the suspect.

Moving on, let’s take a look at the Installed Programs section to identify what software has been installed on this system. Left-click on the heading, and on the right pane we can now see a list of installed programs. From here we can determine when programs were installed and their names, with some entries including WinRAR, GIMP, WinZIP, and Google Chrome.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/eaa4e728e4f657814ff349a5aa50ebcda5c5de3ea7b9fa093b45d72c3a9bd910105fc2801c75f4794434f93f8ff0.png)

Let’s go through one more section together, “Accounts > Email” right at the bottom of the navigation tree. Here we can see a list of email files that were downloaded to the system, typically through an email client.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/05f5004f01650964dc06788fb0a73cb7ebfbf726af8999b41553cad0125dbd930a8d2e3b548f85e4e8748b0bd31d.png)

Now that you understand how to export file by right-clicking, let’s export the highlighted email file and take a look (you’ll need an email client if you want to view it as the sender and recipient would see it, such as Mozilla Thunderbird or Microsoft Outlook App. Alternatively you can read the contents by opening the email with a text editor).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/d020278000d0df4dfe822feeaf8ce520915e60fed5aeff1a76e9f040aaa5669b5e37634929660915a4ff492b0453.png)

Reading a suspect's emails could help to collect evidence regarding the case for a legal investigation, or for incident response purposes we could look to identify malicious emails that were present on the system around the time of the compromise. We could then analyze these to collect indicators such as:

- Email Sender
- Email Recipient
- Date and Time
- Subject Line
- Sending Server IP
- and more!

----
