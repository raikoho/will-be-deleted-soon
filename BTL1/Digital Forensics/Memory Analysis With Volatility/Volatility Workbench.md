**ONLY AVAILABLE IN WINDOWS!!**

Volatility Workbench is a standalone graphical user interface **(GUI) variant of Volatility 3**. Volatility Workbench is free, open source, and runs on Windows. It provides a number of advantages over the command-line version including:

- No need to install Python.
- No need to remember command line parameters.
- Storage of the platform and process list with the memory dump, in a .CFG file. When a memory image is re-loaded, this saves a lot of time and eliminates the need to get a process list each time.
- Simpler copy & paste.
- Simpler saving of the dumped information to a file on disk.
- A drop-down list of available commands and a short description of what the command does.
- Time stamping of the commands executed.
## Using Volatility Workbench

After launching **VolatilityWorkbench.exe**, we're presented with the simple GUI.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/63963102716a28e17e5995e349b6cfaba9c7741818e996bb345f902a14c22d02d03cefa44796bb7053f77cac64ee.png)

Now we need to add a memory dump. Click Browser Image in the top right and navigate to the file you want to import.

We can now select the Platform (OS) and the command we want to run from the two drop-down menus in top left.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/5335ec840f6656fd05df394cc3b4eb898ceea6d03fe9efe1d286baf2896c1ab0f7b8fe604ea7a7fe5fb1ce6b5d0d.png)

In the below screenshot we've run the **windows.pslist** plugin against our memory dump, and received our results almost instantly.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/a2874c46e489d0453ec93dae3d5baf5b68604b44aaf0d5637305abfcf26caba962369a4206665d41c4abdd97a63f.png)

In the bottom right corner we have the ability to copy the output to our clipboard so we can paste it somewhere, or we can click '**Save to file**' to export it.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3c515a03389251be15132d7c4b61ecee357b417aae97435ad398703fcfd866fd450328b25cffe5cd9d4d056f8fbb.png)

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/dc20e3f3e5f4adc157db6c588f9a8ef6be46a2d6ac56582dc572075eeb332c934c98159bda93859c3d8a0d9ce245.png)

And that's it! It's very simple to use, and means we don't need to remember plugin names. **But, this tool is only available on Windows**, so if you're conducting your memory forensics on a Linux-based system, you won't be able to use this natively!