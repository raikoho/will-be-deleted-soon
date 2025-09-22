
FTK Imager is an extremely powerful tool, and is used in real-world investigations by investigators and security teams. Let’s cover some of the features quickly:

- **Dumping RAM** and storing it in a `.mem` file, so we can output it to other tools such as Volatility for analysis purposes.
- **Taking forensically-sound disk images** that can be analyzed in tools such as Autopsy.
- **Export files** directly from disk images.
- **Generate MD5 and SHA1 hashes** for evidence files.
- **Provide a read-only view** of the contents of a disk image, exactly how the user would have seen it.
- **And lots more!**
## Dumping Memory

Once we’ve installed FTK Imager and loaded it up, we’re presented with this display:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/ba9219ef95d2f4558f265739e660ea05bffef5c5684b88bd82f5cbaf8b1be70b41567e3aa695dbbf2964e3dd7e50.png)

The first thing we want to show you how to do is take a snapshot of RAM from the system we’re running FTK Imager on. To do this, we go to **File > Capture Memory**.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8d7d686cd8b967effdca6b989bc75a029820918c2a0846a3ac2777bdd3332ccd26443e3cab36c3ddf77cb7ec3c06.png)

We are then prompted to enter a location for the file to be saved to, so we’ve created a new directory on our Desktop named “Memory Dump”. We can change the filename if we want, but in this example, we’ll leave it as “memdump.mem”. 
As covered earlier in this domain, pagefile may contain additional evidence, but we will not include it in this walkthrough. And at the bottom, we have the option to create an AD1 file – the signature filetype for The Forensic Toolkit (TFK), another tool developed by AccessData. We will leave both of those options unchecked, and click “Capture Memory”. 
FTK Imager will now get to work dumping everything from the RAM, and storing it in a .mem file.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4f6d3ad23b7fb17ba2a9024f5b0d4a57ecc3b27a1e69ca48710a182ff07be2b34d2657c7d9943f8aa2a159c6475f.png)

Once it’s completed, we’ll now have a memory file in our designated destination. We can use tools such as Volatility to analyze this dump, but we’ll cover that in a future lesson.
## Hard Drive Imaging
  
In the real world, a hard drive gathered from a crime scene will be connected to a forensic workstation (a PC with high-end hardware to allow for faster analysis and data transfer) with a clean hard drive attached. A write-blocker will be used between the workstation and the suspect hard drive, preventing the workstation from accidentally changing anything on the hard drive, which could lead to evidence being dismissed for tampering. 
The forensic analyst will then start a bit-by-bit copy of the suspect’s hard drive to the blank one. This can take an extremely long amount of time, as it is an exact copy of every piece of data so that nothing is missed.

We can create a system image file (`.img`) using FTK Imager, which we can then analyze to search for digital evidence. For this example, we’re going to be taking a disk image of a 15 GB USB drive we have. For demonstration purposes, we’ve put some random files on the USB.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c92d5a33b41fda82f289c708b25bd3ff1b03b2a6b52eaea552f27252db646971f0933d57da6d5126fa27948d4822.png)

Within FTK Imager, we want to click on **File**, then go to **Create Disk Image**.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/47c9705eeca789fd2b6c268703bb95e7e43745f7a93d27eb4278c1a4a2aa7e37e3ae2eef9226605d1544a77d02b3.png)

Next FTK Imager will ask us what the source of the evidence will be. As we are taking a copy of the data from a USB drive, we need to select **Physical Drive**.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/572a30babec765d460b7dd138e95b72901f8bda320e0de5dc212f6559b9388a03de83b67232948b05cb19ab6f4c3.png)

As we have selected Physical Drive, FTK Imager will now ask us to select which of the drives are currently attached to the system running the tool. In the drop-down, you can see the 500GB SSD, and the 15GB USB. We need to select the USB drive.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/96c5e38e23f3b15a261583cfc57f4492919b4dd30f36ae29dc1c8da46c77e90d7d204d55527c79f05e1e5924d13b.png)
Next, we will be prompted for Evidence Item Information. This is great to follow the Chain of Custody and ACPO Principles, however, as we are doing this as an example and not a law enforcement or incident response investigation, we can leave this information blank, and click **Next**
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/246e744f8978aec3599633e0902d2d1c894dd41664bf28802a81831c99c61433fe887e9234a74eb98c2acc1075ed.png)

Now we have to assign an output destination, and the file name we want our disk image to have when exported from FTK Imager. We want the `.img` file to be named USBImage.img, and be placed on our Desktop. We also want to set the Image Fragment Size to 0MB – this means that the disk image won’t be split into smaller segments, as we want it all in one file.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b1e40b19556f4892ed6177a89edd9d34dde2208d588d62332ed08ad737bbf188ead04d9bd264517ff841ff73a2c6.png)
After we click Finish FTK Imager will get to work, copying over every single bit of data from the USB to our hard drive.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/189cdd1fc9c18df3dff82c4aad9b17b12ff733996c62fbfbe90f1b6a43be3cf58b4d41e813b86225fc6d11e69563.png)

For this example, it is completed quickly, as the total space of the USB is 15GB. It is also a brand new USB, meaning that there aren’t existing data on it that has been deleted but hasn’t yet been overwritten (remember our Hard Drive Basics lesson, where we mentioned that deleted data is still on the disk!). If you were taking a copy of a 1TB hard drive that has been used for a year, it’s going to take a very long time. Once FTK Imager has finished taking the copy, the below window will popup, comparing file hashes to ensure that the copy is forensically sound.
  
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3d46610b89ec6c16c7f4b7ae6113b564078b953c9057c00a9524d69ddcf4d59522c71c9e0400981372ee906878b8.png)

So how does this work in the real world? The below diagrams demonstrate how a forensic analyst or law enforcement officer would take a forensic copy of a hard drive that is under investigation. The first diagram shows how a hard drive is copied to make a .img file that remains on the forensic workstation.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/480069c446c6a61534ab695e7fb30fbeace2ff37f1302f2941fb17e61064e68c90100644b60b10bb9921dcd10a9a.png)

The second diagram below shows how FTK imager can be used to write the contents of the hard drive under investigation to a blank hard drive.
![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fd0d1284bdb6975c94fbd676b13602ae0b8f5d7c32190e9da9d8cc7b2770b7ce898c7ac45af0149bc26c71e430a7.png)

Want to practice with FTK Imager? You can try imaging an old USB drive, or when selecting the Source Evidence Type you can make copies of folders using the “Contents of a Folder” option.

---

