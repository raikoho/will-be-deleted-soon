We'll start by opening the VolatilityWorkbench folder on the Desktop and double-clicking the VolatilityWorkbench application. 

When we click the Browse Image button at the top to import our memorydump, we'll navigate to Desktop > Malware3, but for the image to show up, we need to change the file types in the bottom right to “Any File”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/8feba1e4d81da8587edf8e8cc1afca41efd8b86b3215af389b22df4dd9818db9c7adcd89bbfde53e1466c1dc1623.png)

Click on malware3.elf, then click Open in the bottom right.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/efe36745257910326794bd87f7ceb60b685243e1327ef20265b3c8f13f69aaf5b89f688bf13d6489b104d5522f64.png)

Before we can start, we need to click the “Refresh Process List” button in Workbench.

**Question 1) When refreshing the process list - what plugin is volatility actually using? (Format: Command.command)**

In the main window of Workbench we can see that after clicking the Refresh Process List button, Workbench is just running the windows.pslist command:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/2448bb384aaa533963c59608781dbb00b3919a1c6a199851389be1c11f72c75eccc637eb11bf8c7193dd11cee65f.png)

**Question 2) Select the windows.info.info plugin from the drop down list. What version of the Windows Operating system is being used on the system the memorydump is taken from? (Format: Windows Version)**

 Selecting the command provided in the question within the output we can see the following lines of interest:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/9cea979f55b974eb4b4688941e48b882b38dc6f0fa967494af926de3f7cd03869e0405750103bd0a5424222368e1.png)

Combining the SystemRoot and MajorOperatingSystemVersion, we can identify that the machine the memory image was taken from is running Windows 10.

**Question 3) Run the windows.pstree.PsTree command and use the process ID drop down menu to help filter out the noise. What is the parent process of Powershell.exe? (Format: PID, ProcessName)**

We'll select the windows.pstree command and click the Process ID checkbox which gives us a dropdown to select the process we want to focus on. Based on the question, we'll find and click on PowerShell.exe that has a PID of 4708. Now we can run the command.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/c264779edeeb60a31154f54dc6774e0ba12ed28602af2fa943117c19031dd5ef60c605a16b76afa918dfa9e9d9d9.png)

In the above output we can see that the parent process of PowerShell.exe is CompatTelRunne which has a process ID of 5264.

**Question 4) Use the windows.privileges command. The process 2416 has the ability to 'Add Workstations to the Domain. What is the attribute associated with this privilege? (Format: AttributeName)**

The question specifically mentions process 2416, so we'll click the Process ID checkbox and select this process from the dropdown menu, which is listed as HxTsr.exe (2416).

Looking through the output we can find a reference to “Add workstations to the domain” which has a Privilege Attribute value of “SeMachineAccountPrivilege”.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/fa16aafc13b6dd69a402fabacb77156c9d417be9756b56c9972cd2f3c77ac37cc8b98e03f00a4023389ddc49b7c0.png)

**Question 5) Pick a plugin to analyse the command-line arguments executed by process 2416. What is the server name the executable is parsing in its command? (Format: ServerName)**

Looking through the command dropdown menu for a relevant plugin, we find windows.cmdline.CmdLine, which seems like it'll do what we need. We'll click the Process ID checkbox and select HxTsr.exe (2416) and run it.

In the output we can see the ServerName value is HX.IPC.Server:

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/3dc04604640d8331dfadfd1b0ced1fa25e5780990753f16452e2061920c56e9ffd326092767b1adf5c9238f7337d.png)