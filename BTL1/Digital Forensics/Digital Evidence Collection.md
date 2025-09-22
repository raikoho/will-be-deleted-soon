This section is dedicated to artifact collection, and how these should be properly retrieved during a forensic investigation.
# Equipment

### Forensic Laptop or Workstation

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c0053208651c9afb7a73776480381896a79e99a03cdef19c2af7619fbbc5936df7d8c536f0b74926c71fe4b1fa69.png)

Bringing a laptop specifically designated for digital evidence can be essential when gathering the evidence at the scene or capturing evidence that may be in memory.  Popular Linux distributions such as CAINE or DEFT can often be found on these laptops, as well as commercialized systems for law enforcement.
  
### Electro-Static Evidence Bags with Tamper-proof Stickers

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a4f44578dc5316508d7c12470e875925863d4c26da3a25f6a46e078c252d964c830effb9e923439a1b3b530dfcbf.jpg)

Electro-Static Evidence Bags will help protect any sensitive digital components from Electro-Static Discharge (ESD) during the transport of the evidence from its initial location, to a secure lab environment.  Labeling is often applied to these bags to let investigators know what is contained inside of them. Having bags or stickers that are sealed, and the seal must be physically broken to gain access to the evidence within is critical to ensure the chain of custody is maintained, and that evidence is not tampered with whilst in storage or transit.
### Labels

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/78e83bb7183d75806bad7762b2f968c9d5c69b12fdb79f94122a075e2ec3af8aeb7bf328f98215c9cb9c2ca57b4a.jpg)

Labeling is essential when conducting any kind of evidence collection.  Knowing what piece of hardware is, helps yourself and other people in the chain of custody determine what the evidence is, without having to go inside of it.
### Photographs

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9295cf761e481df32d3dfa80e7583d6f9aa172aff8d646ddea6d3046f6095ce1416f7e11e159c65b8094bb119ccf.jpg)

Digital cameras can be used to document how IT equipment was found to maintain the Chain of Custody. It can show what cables were plugged in to a server, what external hard drives were connected to a laptop, what was on the screen, and much more.
### Grounding Bracelets

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a6c0b8eab63dc1e876a533e7d5d27932c4816b7b467f27f59fd92a6962b2198c37aa00904d51697162ea3a1e71de.jpg)

Similar to Electro-Static Bags, grounding bracelets are important for investigators to use, to ensure that when handling evidence, they do not inadvertently compromise or damage the evidence.
### Hardware Write-Blockers

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/566f60699b00dcceaa4d490639bbe4e761aef604449af1557e95593b067848d19a0767a13c2437a2b1e69433bc40.png)

Hardware Write Blockers can be an essential piece of equipment that will ensure that your evidence has not been tampered with.  It can either be software on your forensic laptop, or a hardware device that permits read-only access to data storage devices without compromising the integrity of any data that may be contained on them.
### Blank Hard Drives

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/41a6d3171d408cb09b2abdd28bffc186b6095aa089c592ac6b34fae40797c9cf8492060bb0e54ec45f11ce048987.jpg)

In the event that you need to copy data on-site, having blank hard disks are an essential piece of hardware to have in your toolkit.  These can be used in conjunction with write-blockers to copy the disk to another one without making any writeable changes to the media. Drives used for forensic work need to be extremely high capacity, especially if bit-by-bit copies of suspect hard drives are being copied. The size of the receiving drive must always be higher than that of the original drive.
### Specialist Equipment

In some cases, specialized equipment/software is used on the scene to assess the digital evidence that was found. This can include:

- **Wireless Stronghold/Faraday Boxes –** to block any wireless signals from reaching the evidence, preventing remote access or wiping.
- **Specialized Write-Blockers –** write-blockers that could also be used on cell phones, GPS devices, IoT devices, and other non-standard hard drives.
- **Phone Jammers –** acting the same as a faraday box or wireless stronghold.
- **Dedicated Flash Drives –** containing tools like Encase, FTK, CSILinux, and MacQuisiton.

---
# ACPO

Computer-based electronic evidence is held to the same rules and expectations that apply to all other evidence types when presented before a court.
**The main principles of the ACPO Good Practice Guide for Computer-Based Electronic Evidence are:**
### ACPO Principle 1

That no action is taken that should change data held on a digital device including a computer or mobile phone that may subsequently be relied upon as evidence in court.
### ACPO Principle 2

Where a person finds it necessary to access original data held on a digital device, that the person must be competent to do so, and able to explain their actions and the implications of those actions on the digital evidence to a Court.
### ACPO Principle 3

That a trail or record of all actions taken that have been applied to the digital evidence should be created and preserved. An independent third-party forensic expert should be able to examine those processes and reach the same conclusion.
### ACPO Principle 4

That the individual that is leading the investigation has the overall responsibility to ensure that the ACPO principles are followed throughout the investigation.

---
# Chain of Custody

The Chain of Custody is a crucial process within computer forensics, and its primary purpose is to ensure that all of the evidence collected in a case has not been tampered with by an unauthorized individual and the original evidence remains unchanged. 
This involves documenting various information regarding the evidence, such as who, when, and how the evidence was copied or transferred to another person.
### Why is it Important?

The Chain of Custody is extremely important when performing digital forensics for a court case. The court is able to dismiss the evidence if a clear Chain of Custody cannot be presented, as the lack of a Chain of Custody documentation could suggest that there may have been an unauthorized alteration to the evidence.
### Following the Chain of Custody

There are two components to following the Chain of Custody. The first involves ensuring the integrity of the original evidence is maintained. The second involves documenting and recording all of the events that happen to the evidence.
#### Evidence Integrity Hashing

Before you even think about starting to perform analysis on digital evidence or making a forensic copy of it, or even opening the evidence on your workstation, you should always calculate its hash first. Since hashes are small strings that are unique (with the exception of hash collisions) to the input, they are a quick and easy way to ensure evidence integrity. The hash is calculated before and after handling and compared to confirm that no alterations have been made. 
The hash does not necessarily have to be cryptographically secure, since it is only used to verify the integrity of the evidence. You should always hash the evidence using at least two methods – the most popular ones being MD5 and SHA1. This is in part due to the possibility (albeit a very low one) of a hash collision attack, where two distinctly different inputs have the same hash value, allowing attackers to modify the evidence without the hash being changed. Alternatively, SHA256 can be used to generate hashes, as they have not caused collisions before.

If the evidence is physical, such as an external hard drive, you should use a hardware write blocker when you connect your workstation to the device. Write blockers only allow the workstation to have read access on the device and blocks any attempts to write to it. Although software options are available, hardware write blockers are the most effective.
#### Taking a Forensic Copy

Once the hash of the evidence has been recorded, it is best to make a forensic copy of the original evidence if possible and perform analysis on the copy, as this will allow the original evidence to remain untouched. Many tools are available for this process, from simpler bit-by-bit cloning using the `dd` command in Linux to forensic image generators that automatically add metadata and Chain of Custody information, such as the Forensic Toolkit (FTK) and EnCase.
#### Storing Digital Evidence

Physical evidence should be stored in antistatic bags which prevent damage through electric discharge to the data it holds. Taking a step further, Faraday cages may be used, which prevents wireless communication and cellular signal exchange of the device within it. In any case, the evidence should be kept within a locked container, which only the authorized examiners have access to, and kept within an authorized personnel’s watch during transportation.
#### Chain of Custody Form

Every forensic examiner who works with the evidence should fill out a Chain of Custody form. The form should include the description of the evidence when/where it has been acquired or transferred, and by whom, the contacts of the examiners, how the evidence has been accessed, collected or stored and other details regarding the evidence. 
This ensures that there is no broken link within the evidence handling process where the location of the evidence is questioned, as well as having the ability to go back and contact previous examiners.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4a8b75311d24b9abb5bd2c8e59de7dc92cad3463ffb3941f98d6aba0a7e209a1742067ebc36573b4358243d78bda.jpg)


