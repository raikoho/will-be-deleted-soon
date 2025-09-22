**Question 1 - Processes) To export a list of running processes from a Command Prompt into a text file, open a cmd session on the Desktop (or move into the desktop using "cd Desktop") and run "tasklist > tasklist.txt". Open this in Sublime Text and use the Find feature on the top menu to look for instances of cmd.exe. How many are there in total?**

After moving the CMD session to our Desktop (cd Desktop) and running the stated command (tasklist > tasklist.txt) we will right-click the created text file, Open With, and select Sublime Text.

Using CTRL+F and searching for “cmd.exe” shows 4 results (technically one of these is ours, which we used to get a list of running processes, so either 3 or 4 is a correct answer).

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/6ac46a64bd96972f91c4f3d9d69939f53e7ba6eac095bf1b81a106820feb6895ef1f57f0774fc8f453625513c44f.PNG)

**Question 2 - Users) How many accounts in total are present on the system?**

Using the command `net users` we can get a list of all local users on the system.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/aedf6563509ea465aeaca00b32d501b6954eac2424325cab2ab5ec51d0b5479760d313a3b356267a8d37c5027fd5.PNG)

**Question 3 - Users) How many of these accounts are in the administrators localgroup?**

Using the `net localgroup administrators` command we can list all local accounts that have administrative privileges.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/0a3d8ac3a769926a8717f06e179aa1efc2bc09ea5500b82854ee92e935333f56b945c9f492777cf110c1755faf93.PNG)

**Question 4 - Users) What is the name of the suspicious administrator account?**

Looking at the above screenshot, we can see there is an account with the name ‘ServiceeAccount’, which appears to be trying to imitate an account that could exist on the system for legitimate purposes.

**Question 5 - Users) What are the names of the local accounts that are able to connect to the system using RDP? (List them in alphabetical order)**

Using the net localgroup “Remote Desktop Users” command we can see that only one account is able to RDP, the suspicious account from the previous question.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/161c5b92c2a84c60b6dc16cfc8f65f670509bd0011a82ca72b564f5bb34dc8569d30965e2459db484f697d495a84.PNG)

**Question 6 - PowerShell Users) Run the command to get detailed information about the suspicious account identified earlier. When was it last logged in?** 

Using the command `Get-LocalUser -Name ServiceeAccount | Select *` we can retrieve all properties relating to this local account. Highlighted we can see the last login timestamp.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/86257b82d51145b40ef82499a6ffc6b88665dc3bcb6e832dda6dd2966d557c2b2f2373952e85664329dc570d0240.PNG)

**Question 7 - PowerShell Services) Run the command to list services on the system. What is the display name of the service starting with "Amazon"?**

Running the command Get-Service | Where Status -eq "Running" | Out-GridView will open a new window. From here, we can see that the service we've been asked to find is at the top of the alphabetical list.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/b03b663971c5dbc2eb64f3f4ada3302dd0c88260e679cc14c0d50280ff59849a0c096c6a0cf91bd9d55d4047f2be.PNG)

**Question 8 - PowerShell Scheduled Tasks) Get a list of all Scheduled Tasks. What is the TaskName of the entry beginning with 'P' that is in a Ready state?**

Using the command `Get-ScheduledTask | Where State -eq "Ready"` we can see only Scheduled Tasks that are in the state we're looking for. The first item shown is the task we're looking for.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/39ea31b38b6bdfd59caf37dad59cd8b0f1f660433f8a0f781d71075a2cfaf1572abb5d7266ababc1a9d22fe51bd4.PNG)

**Question 9 - PowerShell Scheduled Tasks)  Run the command "Get-ScheduledTask -TaskName 'TaskNameFromLastQuestionHere' | Select *". Look at the Triggers property, what is it?**

Running the provided command we can see that the Trigger property is set to when a user logs into the system.

![](https://d2y9h8w1ydnujs.cloudfront.net/uploads/content/images/4a9bb802f2b078938f66b54e0d4d8166970812008769d69c15f3a1fc73c943bb55df959259d2ea8d1e30be12dddf.PNG)