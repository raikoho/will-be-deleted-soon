Includes areas such as various file systems, storage media fundamentals, data representation, metadata and file carving, memory analysis, and Order of Volatility.
# Hard Disk Drive Basics

Hard drives are typically where a lot of digital evidence is stored and collected, so understanding how hard drives function and where data can be hidden is important, allowing you to collect artifacts in future lessons. This lesson will cover the following HDD basics.

- **Platters**
- **Sectors**
- **Clusters**
- **Slack Space**
## What are HDDs?

A hard disk drive (HDD) is a non-volatile memory hardware device that controls the positioning, reading and writing of the hard disk, which furnishes data storage. Hard disk drives are commonly used as the main storage device in a desktop computer or laptop. HDDs will typically store an operating system, software programs and user-created files such as documents. Hard disk drives are commonly found in drive bays and are connected to the motherboard via an ATA, SATA, or SCSI cable, and also connected directly to a power supply unit (PSU).
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/50b4187a7c6b04e9edc7351d14bb9a502f5f4ec491555a076282ea56e6098a862c202cfed8dfc279ef302a336eaf.jpg)
## Platters

A **hard disk drive platter** (or disk) is the circular disk on which magnetic data is stored in a hard disk drive. The rigid nature of the platters in a hard drive is what gives them their name (as opposed to the flexible materials which are used to make floppy disks). Hard drives typically have several platters which are mounted on the same spindle. A platter can store information on both sides, requiring two heads per platter.
## Sectors

In computer disk storage, a **sector** is a subdivision of a track on a magnetic disk or optical disc. Each sector stores a fixed amount of user-accessible data, traditionally 512 bytes for hard disk drives, while newer HDDs use 4096-byte (4 KiB) sectors.

The sector is the minimum storage unit of a hard drive. Most disk partitioning schemes are designed to have files occupy an integral number of sectors regardless of the file’s actual size. Files that do not fill a whole sector will have the remainder of their last sector filled with zeroes. In practice, operating systems typically operate on blocks of data, which may span multiple sectors.

In modern disk drives, each physical sector is made up of two basic parts, the sector header area (typically called “ID”) and the data area. The header may also include an alternate address to be used if the data area is undependable. The _address identification_ is used to ensure that the mechanics of the drive have positioned the read/write head over the correct location. The data area contains the sync bytes, user data, and an error-correcting code (ECC) that is used to check and possibly correct errors that may have been introduced into the data.
## Clusters

A cluster, in the context of a hard disk, is a group of sectors (described above) within a disk and is the grouping by which disk files are organized. A cluster is larger than a sector, and most files fill many clusters of disk space. The hard drive is able to find all the clusters on a disk because each cluster possesses its own unique ID value.
## Slack Space

Slack space is the leftover storage that exists on a computer’s hard disk drive when a computer file does not need all the space it has been allocated by the operating system. The examination of slack space is an important aspect of computer forensics as we can find the remaining data from previous files allocated in the same cluster. For example, if a user deleted files that filled an entire hard drive cluster, and then saved new files that only filled half of the cluster, the latter half would not necessarily be empty. It may include leftover information from the deleted files that we can retrieve, and may potentially include evidence.

---
# Solid State Disk Drive Basics (SSD)

A solid-state drive (SSD) is a new generation of storage devices. SSDs have evolved beyond traditional mechanical hard disks by using flash-based memory which is significantly faster, allowing SSDs to speed up computers significantly because of their low read-access times and fast throughputs.

SSD basics:

- **Garbage Collection**
- **Trim**
- **Wear Leveling**
### Garbage

Garbage collection is a process used by solid-state drives to optimize space and improve efficiency. The goal of garbage collection is to keep as many empty blocks as possible so that when the SSD needs to write data, it can do so without waiting for a block to be erased. The SSD’s controller looks for any pages that are no longer being used, such as deleted data and modified data. It then moves used pages to new blocks, leaving behind the data that is no longer needed. The controller then erases the block so that it’s ready for use. This is a background process, handled by the SSD controller and the operating system.

Why is garbage collection important in regard to digital forensics? If we have crucial evidence on a system, there’s always the risk that garbage collection will identify the blocks either legitimately or illegitimately as unwanted, and the controller will erase the blocks in order to free up space. If a computer is using solid-state drives, it needs to be powered off immediately to prevent this from happening, either with a hard shut-down (holding the power button until the system turns off), or by pulling the plug so the power supply unit (PSU) receives no electricity. Shutting down the system via the operating system could execute a malicious script that works to destroy data contained on any attached drives, and could ruin an investigation (but we need to remember volatile evidence, which we’ll cover later!).
### Trim

When files are sent to locations such as the Recycle Bin, they are not immediately deleted. Moving them to this location tells the operating system that it is ok to overwrite these files, as they are no longer wanted by the user. If a deleted file is 174192 bytes, and a new file is only 121 bytes, then there will still be 174071 bytes of the deleted file available, so we can recover this and attempt to fix the file so we can see what it was, even with some missing data. However, TRIM operates similarly to Garbage Collection, and instead of telling the SSD to make the size of the deleted file unallocated (available for overwriting), TRIM on an SSD will simply select the data and clear it, removing any chance of forensic investigations recovering the file, or parts of the file.

To counter this, we should take the same actions when dealing with Garbage Collection, as they work together. Power the system off with a hard shut-down or pull the plug (again, we need to remember volatile evidence, which we’ll cover later!).
### Wear Levelling

Wear leveling is a technique that some SSDs utilize to increase the lifetime of the memory using a very simple approach: evenly distribute writing on all blocks of an SSD so they wear evenly. Using this method, all physical cells in the SSD receive the same number of writes, to avoid writing too often on the same blocks, causing damage over time.

Wear leveling is performed by the micro-controller or the firmware of the SSD device. The process of wear leveling is conducted by algorithms, of which there are two basic varieties.

- **Dynamic wear leveling** – When dynamic wear leveling is used blocks that undergo rewriting are repositioned to new blocks. The algorithm selects an empty block on which to write the data. The number of writes to each block is kept track of by the controller. A downside to dynamic leveling is that data blocks that are not frequently updated are not moved which can lead to uneven block wear.
- **Static wear leveling** – The same techniques are employed by static wear-leveling with one important difference. Blocks of static data are moved when their block erase count falls below a certain threshold. This leads to more effective leveling which results in slightly slower write performance countered with enhanced longevity of the device.

---
# File Systems

It is a means of classifying and organizing files and storing data, helping to efficiently manage the space available in a device for storing data, so that the required information can be received whenever necessary.

A filesystem is a set of data types that is employed for:

- **Data storage**
- **Hierarchical categorization**
- **Data management**
- **File navigation**
- **Accessing the data**
- **Recovery of data**

A file system is used to control how data is stored and retrieved on a storage medium, such as a hard-disk drive. There are many different kinds of file systems, and each one has a different structure and logic, speed, flexibility, security, size, and more.

Most popuar file systems:

- **FAT16**
- **FAT32**
- **NTFS**
- **EXT3 / EXT4**
### Identifying File Systems

In DF3) Digital Evidence Collection we cover how to use FTK Imager for taking forensically-sound disk images during an investigation, but here we’re going to quickly cover how you can identify the file system from an existing disk image, which you’ll be doing in the file systems activity.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/37fc4ff322750d22235723a70d136d56004d2312d508038fe7d4701ed71a2a61451809fbd2a4b951ce464da39f7e.png)

We need to click on File > Add Evidence Item.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/660182a64b079aea0067a917f884834a5fb8ff243b46309f657456bce1b42dd3398dccec3fd94879ca496530f8dd.png)

When asked for the source evidence type, we want to select Image File.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/83acc1400a758dd36406ae7a41307de353292091530851593e822f6e134ab08c81b890c5effbada2db3c1ac947e5.png)

We’re going to open the file disk2.img, then click Finish.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c06fce847ed133ec18339669f5588f469331231c829a8023658f93e171981e2d8f42090ec820eef014efd31d6584.png)

The below GIF shows how you can identify the file system using FTK Imager. The system this image file was taken from is using NTFS.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9a37608cc6df9c5c5a2bcae4b6d40d9eb0a635ab175f3872f981f14e49aa6b7c25a2cdb11c680e603875f21e3ca6.gif)

----
# Digital Evidence and Handling

**Digital evidence** or electronic evidence is any probative information stored or transmitted in digital form.
### Digital Evidence Forms

There are a wide range of forms that digital evidence can take. Below we’ve compiled a short list of some common evidence forms, which can apply to both law enforcement investigations, and security teams conducting DFIR activities.

- **E-mails -** These can contain written communication between two or more individuals, and may also contain files as attachments.
- **Digital Photographs -** The photos themselves can be evidence, additionally extra information may be present as photo metadata, which can include the location and device used to take the photograph.
- **Logs -** System logs can contain a wide range of information, depending on the device that has created the log, and the level of logging enabled. Examples can include Windows Event logs that can show login times to show when a user account was accessed.
- **Files -** User files such as notes, code, images, installed software, and more can all provide context about the activity of a user.
- **Messages -** Similar to emails, messages (text, iMessage, Facebook Messenger, WhatsApp, etc) can provide information about a conversation between two or more individuals.
- **Browser History -** This can help us to understand what websites and resources have been accessed from a device, and at what time.
- **Backups -** If files have been deleted, they may be present in backups, allowing us to investigate them even if they have been overwritten on the original storage medium.
- **Video/audio files -** These files, similarly to digital photographs, could be evidence themselves, but could also have metadata to help provide additional information.
### Evidence Handling

Proper handling and securing of evidence are critical. Mistakes in how evidence is acquired can lead to that evidence being tainted and, subsequently, not forensically sound. In addition, if an incident involves potential legal issues, critical evidence can be excluded from being admitted in a criminal or civil proceeding. There are several key tenets for evidence handling that need to be followed, as listed here:

– **Altering the original evidence**: Actions taken by digital forensics examiners should not alter the original evidence. For example, forensic analysts should not access a running system if they do not have to. It should be noted that some of the tasks that will be explored have the potential to alter some of the evidence. By incorporating proper documentation and having a justifiable reason, digital forensics examiners can reduce the chance that evidence will be deemed tainted.

– **Using write-blockers**: Although most forensic software tools have built-in software write blockers, you also need an assortment of physical write blockers to cover as many situations or devices as possible. A write blocker is used to keep an operating system from making any changes to the original or suspect media to keep from erasing or damaging potential evidence. Software write blockers work at the operating system level and are specific to the operating system. In other words, a software write blocker works on only the operating system in which it is installed. A physical write blocker works at the hardware level and can work with any operating system because, at the physical level, the write blocker is intercepting (or, in many cases, blocking) electrical signals to the storage device and has no concern about which operating system is in place.

– **Document:**  One central theme you will often hear in law enforcement is the phrase: “If you didn’t write it down, it didn’t happen.” This is especially true when discussing digital forensics. Every action that is taken should be documented in one way or another. This includes detailed notes and diagrams. Another way to document is through photographs. Proper documentation allows examiners to reconstruct the chain of events if ever the integrity of evidence is called into question.

---
# Order of Volatility

When examining digital evidence, it is important to understand the volatile nature of some of the evidence an examiner will want to look at. Volatile evidence is evidence that **can be lost when a system is powered down**.
#### Order of Volatility

**Registers & Cache**

The contents of the CPU cache and registers are extremely volatile since they are constantly changing. An investigator needs to retrieve data from the cache and register immediately before that evidence is lost.

**Memory**

The information located on random access memory (RAM) can be lost if there is a power spike or if the system is disconnected from power. This is a fast, temporary, type of memory in which programs, applications and data are stored. This can include very useful data about running processes, network connections, and much more.

**Disk (HDD and SSD)**

As we covered in the hard disk drive (HDD) and solid-state disk drive (SSD) basics lessons, we know that once data has been overwritten, it is impossible to recover it, and SSDs have the additional risk of Garbage Collection or TRIM deleting files that could be used as evidence. If the system is offline then the disk space can’t be overwritten and the disk is no longer considered volatile.

**Remote Logging and Monitoring Data**

The potential for remote logging and monitoring data to change is much higher than data on a hard drive, but the information is not as vital. So, even though the volatility of the data is higher here, we still want that hard drive data first.

**Physical Configuration, Network Topology, Archival Media**

Here we have items that are either not that vital in terms of the data or are not at all volatile. The physical configuration and network topology is information that could help an investigation but is likely not going to have a tremendous impact. Finally, archived data is usually going to be located on a separate physical device, such as a USB drive or external hard drive.

---
# Metadata and File Carving

**File carving** is a process of searching for files in a data stream and is used to carve deleted files from disk images, so we can investigate files that have been deleted by a user, provided they haven’t been overwritten with new data.

**Metadata** is “data about data”, which sounds confusing, but is relatively straightforward. If you have a Microsoft Word document that contains text, that text is data. Metadata is information that describes the data and can include details such as the author of the document, and in photos, it can contain the camera settings, GPS location, resolution, and much more.
### Metadata

Let’s take a look at some metadata by viewing file properties inside the Windows OS. By right-clicking on a Microsoft Word file and clicking on the ‘Details’ tab we can see some useful information including the author when the file was created, last saved, and the word count.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/22d66c7bcbd9ee24b81fb00d759f8abdf7f22202c7329be98f7697b8bd503c587577952f13c02cfb43035e8134b5.png)

We can also retrieve metadata in a Linux system by using the same method as above, right-clicking on a file and viewing the properties, or using two commands, `ls -lisap <file>` and `stat <file>`, as shown below. In this case, we’re provided with information such as the read/write permissions we have, the file name and size, and the times for when the file was last accessed and modified.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/18afa56cff08754db5d5638f63eaab7495bc75de5a2a5db953bf3d24cb462b0bd4bb9369a63f99538257e23ba652.png)

A great command-line tool we can use in Kali Linux is `exiftool`, which works to retrieve metadata from files. Type “exiftool” to see if you have it installed, and if not, use `sudo apt-get install exiftool` to download and install the tool.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ca11ff8b518b761c308d2555507136a7ac2470b9d79e32ae6018ac6cf08920315d7a5fd28082d4b9a77b73b34573.png)

The tool is straightforward to use, just type `exiftool <filename>` and we can retrieve a ton of useful information, as shown in the GIF demonstration below.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/79ab7a938d106d52b2508d6bae5b1198cc50020e9cead577667fdd581bbb08db615e58f9e4d10d2014a400896c6a.gif)

### File Carving

We’re going to show you how to retrieve deleted files using the Linux command-line tool `scalpel`. If you haven’t used this tool before, use the command `man scalpel` to see what it can do! When attempting to use scalpel on a disk image file (.img) the tool will communicate with it’s configuration file, which is located at `/etc/scalpel/scalpel.conf` by default. This configuration file allows us to define what file types we’re trying to search for. Let’s walk through an example where we believe a suspect has deleted a .jpg image file containing sensitive information, and we need to retrieve it as digital evidence. The hard drive appeared empty when collected from the crime scene, but a bit-by-bit disk image was taken, so we can identify any deleted files.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/98774d86159df9bc11640810fd62ad4789ca3bdb464b99f93271b05907b1d534ec7181bf2283c1c41b242be27085.png)

First things first, we need to edit the `scalpel.conf` file to tell scalpel that we want to identify and extract Microsoft Office Word files. You can use command-line text editors such as `nano` or `vim`, but it’s easier to use the file system GUI and navigate to the file yourself. The file path is **/etc/scalpel/scalpel.conf.**

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/59ae71984b1dc29d9bbd3f8587054196840b9393eb524614819ccb67d7e2aa53b482ba501e612f8d5440ac204780.gif)

Once you’ve found and opened the config file in your choice of text editor, you’ll be presented with a file that looks like the below screenshot, where we’re looking at the section for Microsoft Office document profiles. The “#” at the start of each line means they are commented out and are not read by the program when the .config file is called.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/47728710362744042aa31c780732593571eea6889f8c81b7b7c05cf13b70c7f4cabefb61155207c65dfc69e93912.png)

As we’re looking for .jpg image files, we need to locate the section of the .conf file that references jpg files. In the below screenshot you can see how we’re able to remove the hashtags to enable detection for this file type (the line will turn white to show it is no longer commented).
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9adf750e9e60f0dd6b83d25d51b8dd108d0686d27e82f92132c2c4f75a63d0763601031b288082c79d75d7f9f264.gif)

Now that we’ve configured scalpel to understand what files we’re looking for, we can summon the tool using the following command: `scalpel -o <output> <disk image file>`

- **scalpel** calls the tool we want to use
- `-o <name>` provides a directory for recovered files to be stored. This MUST be an empty directory, or the name of a non-existent directory, as scalpel will create one 
- `<disk image file>` tells scalpel the file we want to search for files inside

Example command: `scalpel -o /root/Desktop/ScalpelOutput DiskImage1.img`

Let’s run the command and watch scalpel recover any JPG image files for us!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/539b3b142f29ddc5a4878be5fd18b0c81708adf6cd55644824f0d968f273eff3b1806ba11fc69ddcf61cf3e0d128.png)

In the above screenshot we can see that scalpel identified and retrieved one JPG file, based on the message at the bottom of the terminal “Scalpel is done, files carved = 1, elapsed = 0 seconds”! Let’s go see what Scalpel found in the output directory we listed. In the below screenshots we can see that Scalpel created a file audit.txt which contains information about the activity the tool has completed, and the jpg directory includes the deleted photo we have retrieved.  

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/67bcff35e4bc327f7bd2da9ce715baaa9558689b1cbb3d9ff1336102d85b83e8dac8e67e5ee8a7ae0e1df07ae3f1.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/22c5d96620e0aa7833e7e0b93580b555c19535cb02a2e4a18b55004374d5c97eb99b1f20cec7972a117b0b030add.png)

It’s worth mentioning that profiles in the scalpel.conf file can be created by a user if you need to search for specific or custom files by altering the file extension, file header, and file footer values. The top of the .conf file has detailed information about writing custom detection profiles for file carving, so give it a read!
### Chown Command 

**Modifying User Files with Chown**

We covered a lot when it comes to interacting with User Files in Linux, but we have yet to cover the Linux command **chown**—short for 'change owner.' This crucial tool is used for managing file ownership and permission on Unix-like operating systems such as Linux. This command is pivotal in scenarios where digital forensic analysts need to grant or revoke access to specific resources.

We are going to be looking at the three types of file permission utilized in the chown command: User, Group, and Other. Let's take a look at the syntax below and break down Chown's components:

`chown [options] new_owner[:new_group] file(s)`

_(Disclaimer: You can also run the command_ `_man chown_` _within your CLI for a sufficient breakdown)._  
Here’s a breakdown of the components:

- `chown`: The base command.
- `options`: Optional flags that modify the behavior of the `chown` command.
- `new_owner[:new_group]`: The new owner and optionally the new group. If `new_group` is omitted, only the owner is changed.
- `file(s)`: The file or files for which ownership is to be changed.

Let's try to do a mock example below:

Let's say we have a file titled **q3.conf** and our current user is **ubuntu**. We would like to edit this configuration file, but we lack file ownership. How would we go about this?  
Remember the syntax from above, this time, I will provide a cleaner version since we will not be utilizing any options, group owners, or multiple files: 

`chown new_owner file`   
  
I will place the following in my CLI:

`chown ubuntu q3.conf`

In this instance, the command has designated the user **ubuntu** as the new owner of the file `q3.conf`. Also, let us double-check our work with this command below:

`ls -l q3.conf`

---
# Memory, Pagefile, and Hibernation File

This lesson is going to cover four important topics;

- Memory (Windows and Linux)
- Pagefile (Windows)
- Swapfile (Linux)
- Hibernation File (Windows)
## Memory

#### What is Memory?

In computing, memory refers to a device that is used to store information for immediate use in a computer or related computer hardware device. Computer memory operates at a high speed, for example, random-access memory (RAM), as a distinction from storage that provides slow-to-access information but offers higher capacities.
#### What is Memory Analysis?

Memory forensics (sometimes referred to as memory analysis) refers to the analysis of volatile data in a computer’s memory dump. Information security professionals conduct memory forensics to investigate and identify attacks or malicious behaviors that do not leave easily detectable tracks on hard drive data.
#### What is in a Memory Dump?

A memory dump (also known as a core dump or system dump) is a snapshot capture of computer memory data from a specific instant. A memory dump can contain valuable forensics data about the state of the system before an incident such as a crash or security compromise, such as running processes, network connections, and malware that doesn’t take the form of files, but instead resides purely in memory.
#### Why is Memory Forensics Important?

Memory forensics can provide unique insights into runtime system activity, including open network connections and recently executed commands or processes. In many cases, critical data pertaining to attacks or threats will exist solely in system memory – examples include network connections, account credentials, chat messages, encryption keys, running processes, injected code fragments, and internet history which is non-cacheable. Any program – malicious or otherwise – must be loaded in memory in order to execute, making memory forensics critical for identifying otherwise obfuscated attacks.

As attack methods become increasingly sophisticated, memory forensics tools and skills are in high demand for security professionals today. Security solutions such as antivirus programs and endpoint detection and response (EDR) agents may be unable to detect malware written directly into a computer’s physical memory or RAM. Security teams should look to memory forensics tools and specialists to protect invaluable business intelligence and data from stealthy attacks such as fileless, in-memory malware or RAM scrapers.
## Pagefile

#### What is Pagefile.sys?

The Pagefile.sys is used within Windows operating systems to store data from the RAM when it becomes full. The Pagefile.sys is a contiguous file, so it can be read more quickly, that is located on the root of the hard drive and, normally, the more infrequently used memory pages are stored to it. Whilst RAM is used by the system to store active data as, due to the speed of its operation of it, the system functions more quickly than if that data were stored and read from the hard drive. However, through normal use, RAM is filled by the system and then Windows is able to identify which data to move from it to the Pagefile.sys where it can remain until required again.

It can also be used as a backup of data in the event of a system crash. By default, the Windows operating system configures the size of the Pagefile.sys, however, it can also be altered by the user. Normally the Pagefile.sys can be a significant proportion of data present on the hard drive, however, removing it can greatly reduce the operating speed of the computer.
#### Deleting Pagefile.sys

The Pagefile.sys is hidden from the normal Windows user by default as, like many other files on the hard drive, it is a system file that Windows identifies as important in the normal operation of the system. If the file is deleted fully then the system will not function correctly and is likely to become unstable, however, the system can be configured to store the pagefile.sys onto another secondary hard drive.
## Swapfile

#### The Swap file in Linux

Similar to Windows, Linux uses swap space to store RAM when it is full or when the data is not in current use. Within Linux however, traditionally it is a swap partition rather than a swap file and is therefore separate from the other files as it is contained on its own partition. However, it is possible to create a swap file within Linux and to manage the size of that file if required, whereas it is not as easy and sometimes impossible to adjust the size of a swap partition. This can be done via the command `sudo fallocate -l [file size] /swapfile` once the swap file has been temporarily disabled.
#### Swap space Related Commands in Linux

In order to check the amount of swap space available to the system, the `free -h` command can be used which will provide the breakdown of total, used and free swap space on the system. The `swapon –show` command can then be used to identify whether the swap space is a file or a partition. It is also possible to adjust how often the swap space is used within Linux, the default being 60, however, it can be increased from between 0 (for servers) to 100 (for desktop) which makes the system use the swap space more frequently.
## Hibernation File

#### What is a Hibernation File?

Starting with Windows 2000, Microsoft introduced the hibernation feature that allows the operating system to store the current state of operation when you turn off the computer, or the system goes into sleep mode. During hibernation everything from memory is copied to the disk in a file called hiberfil.sys, when the computer is restored, the system moves to the saved state. Hibernation files are a good source of information for digital forensic practitioners, as they store data in RAM file without having to run special tools.

---
# Hashing and Integrity

Creating hashes is an important part of digital forensics, as it allows any tampering or modification of evidence to be immediately visible.
## What are Hashes?

Hash values, which come in the form of text strings, are the unique fingerprint of a file or string. If I had a text file with the letter “ABC” in it, I could generate a hash value. Now if I went back into that file and added the letter “D” to it, and retrieved the file’s hash value, it will be different than the initial one. We have modified the contents, so now the fingerprint is different.

The most common hash to work with is Message Digest 5, commonly referred to as MD5. Two other common hashes include SHA1, and SHA256. Due to collisions, an event where two different data values can have the same hash value, MD5 is no longer used as a secure standard, and SHA256 is taking over as the most common algorithm to use. We have already covered how to generate MD5, SHA1, and SHA256 hashes in the Phishing Analysis domain, but we’ll provide a quick overview here.
## Gathering Hashes in Windows

`get-filehash <file>` 

will generate a SHA256 hash. 
If we want to retrieve the MD5 or SHA1 values, we need:

`get-filehash -algorithm md5 <file>` 
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/e5bb0f5944a529b146ca6ec917fb862dbddbb2b1cecc6b3745716fb3214099fa0288a0495b76fb34d4a15f8be872.png)
## Gathering Hashes in Linux

On a Linux system generating hashes is a lot quicker. We can use the following three commands to generate SHA256, MD5, and SHA1 hashes respectively:

- `sha256sum <file>`
- `md5sum <file>`
- `sha1sum <file>`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/873e84b4be5d17a186ad9aeb2c550227aa9db4ef467e83ce088dc1eb54d3ae2608bbdf231fb58ab7d2590c922b3c.png)

We can also retrieve the hash values of text strings using the command `echo -n <text> | string`, as demonstrated below.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5e3278ebf934725bdf1d276f30df506ca3414c600b7259f1373faf5610b663213417d603aa660396476634e55caa.gif)
## Evidence Integrity

Now that you understand how hashes work, and how they’re generated, you should be able to see how this applies to digital forensics, and ensuring the integrity of files or evidence. In most investigations involving a hard drive, a hash will be generated from the hard drive, and then a complete copy of the storage media will be taken at a bit-by-bit level, meaning that **everything** possible from the disk is copied to a fresh hard drive. 
This new hard drive then has its hash generated, to ensure that this is the exact same value as the original, proving that an exact copy was successfully generated. This allows forensic analysts or investigators to work on a copy of the evidence, instead of analyzing the actual disk which could result in loss of evidence if anything went wrong, or the court could argue that the evidence may have been tampered with, and is therefore not viable for use in court during legal proceedings.