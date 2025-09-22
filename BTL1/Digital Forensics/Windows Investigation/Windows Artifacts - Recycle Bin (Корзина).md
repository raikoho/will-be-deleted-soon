## Artifact Description

The Windows Recycle Bin is a system folder designed to temporarily store deleted files and folders before they are permanently removed from the computer's hard drive or storage device. When a user deletes a file or folder in the Windows operating system, it is typically moved to the Recycle Bin, allowing the user to restore the item if it was deleted accidentally. However, once the Recycle Bin is emptied, the items within it are considered permanently deleted.

In the context of digital forensics, the Windows Recycle Bin is important for several reasons:

- **Recovery of deleted files:** Files that have been recently deleted and are still present in the Recycle Bin can be easily restored by forensic examiners. This can provide valuable evidence or information related to a case, as it may contain relevant documents, images, or other data that were intentionally or unintentionally deleted.
- **Tracing user activity:** The presence of specific files in the Recycle Bin can indicate a user's attempt to delete evidence or conceal their activities. Forensic experts can analyze the metadata of the deleted files, such as timestamps and file paths, to establish a timeline of events and identify potential motives or patterns of behavior.
- **File remnants and data carving:** Even after the Recycle Bin has been emptied, the underlying data of the deleted files may still be present on the storage device. When a file is deleted, the operating system typically marks the occupied space as free, but the actual data remains until it is overwritten by new data. Forensic examiners can use specialized tools and techniques, such as data carving, to recover these remnants and reconstruct the deleted files, providing additional evidence for an investigation.
- **Analysis of Recycle Bin artifacts:** The Recycle Bin maintains several system files that store information about the deleted items, such as their original file paths, deletion timestamps, and other metadata. These artifacts can be valuable for forensic investigations, as they can help investigators understand the user's actions and intentions, as well as provide context for other digital evidence.

## Artifact Location

On Windows 10, we can find the Recycle Bin directory for all users located at `C:\$Recycle.Bin`

If the user has emptied the Recycle Bin, we lose this artifact and cannot analyze it.

## Artifact Analysis, Overview

To collect and triage Recycle Bin artifacts, we're going to use the following tools:

- Command Prompt (CMD)
- RBCmd - [GitHub - EricZimmerman/RBCmd: Recycle bin artifact parser](https://github.com/EricZimmerman/RBCmd)
- CSVQuickViewer

## Technical Analysis

So, we know the directory for the Reycle Bin is (by default) `C:\$Recycle.Bin`. We need to use `dir /a` as the folders are hidden by default, and the /a flag will show these.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/7a554358a996bd1286d7c51e61e3480cfe76075a00f7b662e6eb0ea0b46bf93f175fc27e6f6580ca63fe93d16c5e.png)

We can see that there are sub-folders using account security identifiers as the name (SIDs). It's easy to find out what username the SID relates to  using Windows Management Instrumentation Command (WMIC): `wmic useraccount get name,SID`

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2298a091420a14de5f0cb60c5f4bf066c10f4dad59a76caa54ce921e85bbf48c463eb034b6b5d0942c7e21faf6f0.png)

Imagine we're investigating the account Simon.Leeves to verify claims he has intentionally deleted critical company files. We know his SID ends in "1010". We'll move into the folder associated with his account's SID (we can use the [Tab] key to auto-fill and go through the directories for us, so we don't need to type it out!). Using `dir /a` again, we can list all of the hidden contents.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/777d9cde5616e584159d9a5a1ac94b7a33f343a447953a6990d0a5ba36e79667f19912102e81604145da38d589e3.png)

The filenames might seem quite confusing, but since Windows Vista, two files are generated whenever a file is deleted by a user.

Files that begin with “**$R**” followed by a random string contain the true file contents of the recycled file.

Files that begin with `$I` and end in the same string as the **“$R”** file counterpart contain the metadata for that specific file, such as the original filename, path, size, and timestamp of when the file was deleted.

So, now that we have access to $R and $I files related to the user account Simon.Leeves, let's analyze them to see what files we can find! First we'll use RBCmd. To simplify things, we will use our current Command Prompt session in the Recycle Bin sub-folder for the SID of the Simon.Leeves user account, and execute RBCmd from here, using the command: `C:\Users\BTLOTest\Desktop\Recycle-Bin-Analysis\Tools\RBCmd.exe -f $I1UOZ51.xlsx`. This command tells the RBCmd executable to analyze the specific file provided, which is the first $I file in this folder.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b3728488e215a3de5de0a4d4bfe139f520ce8dd1e83aaaf88c7604d93c44e436b20e7478a46dd0314bca222bb8f0.png)

From the output above, we can see that the file was originally 1.8MB in size, was located in the /Downloads/ folder, was named “DU Financials 2022.xlsx”, and was deleted on 2023-04-12 at 13:18.

Great, we know everything is working as expected. Now we can provide the entire folder to RBCmd to analyse using the -d flag (directory) instead of the -f flag (file). We'll also output everything to a CSV file so we don't have to scroll in the terminal.

`C:\Users\BTLOTest\Desktop\Recycle-Bin-Analysis\Tools\RBCmd.exe -d . --csv "C:\Users\BTLOTest\Desktop\RBCmdOutput"`

This command is running the RBCmd executable, telling it to input the current directory (-d . ) and export a CSV to a folder on the Desktop of our user.

Using CSVQuickViewer from the Desktop we can open the generated CSV file and investigate the contents. Using this file format, we can easily see what files were deleted by the user and when!

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2417026fd9e1d500b2ea072c3850c2e8bbe11b49ca81ce2cb57b0f6a2acc55979aa143384fa9486f66f686464ad6.png)

If, for some reason, we wanted to analyze the Recycle Bin for all local accounts on a system, we could run RBCmd from the C:$Recycle.Bin directory, and the use (-d . ) argument to point the tool at this directory. It will then recursively go through each of the SID sub-folders looking for $I files to analyze.