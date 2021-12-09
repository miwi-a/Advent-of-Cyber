
Answer the questions below

Read the premise above, start the attached Windows analysis machine and find the transcription logs in the SantasLaptopLogs folder on the Desktop.

If you want to RDP into the machine, start the AttackBox and enter the following into a terminal: xfreerdp /u:Administrator /p:grinch123! /v:10.10.104.176 - The credentials for the machine are Administrator as the username, and grinch123! as the password.

Each transcription log is a simple plain text file that you can open in any editor of your choice. While the filenames are random, you can get an idea as to which log "comes first" by looking at the Date Modified or Date Created attributes, or the timestamps just before the file extension!

Open the first transcription log. You can see the commands and output for everything that ran within PowerShell, like whoami and systeminfo!

What operating system is Santa's laptop running ("OS Name")?

![image](https://user-images.githubusercontent.com/95479102/145354459-7ccd5a4c-77fe-411b-be0c-6a9b5c4153f5.png)

![image](https://user-images.githubusercontent.com/95479102/145354696-e694e9f3-50a1-4dee-96d6-d7abff7168bb.png)

Review each transcription log to get an idea for what activity was performed on the laptop just after it went missing. In the "second" transcription log, it seems as if the perpetrator created a backdoor user account!

What was the password set for the new "backdoor" account?

![image](https://user-images.githubusercontent.com/95479102/145354929-be3814da-39b9-4da6-b96e-93394007f52e.png)

In one of the transcription logs,  the bad actor interacts with the target under the new backdoor user account, and copies a unique file to the Desktop. Before it is copied to the Desktop, what is the full path of the original file? 

![image](https://user-images.githubusercontent.com/95479102/145355080-d9d6faf6-85cb-4840-abf7-28353ae2aac4.png)

The actor uses a Living Off The Land binary (LOLbin) to encode this file, and then verifies it succeeded by viewing the output file. What is the name of this LOLbin?

![image](https://user-images.githubusercontent.com/95479102/145355259-d30b289b-6919-4fd8-a0d7-dd1690bcea41.png)

The UsrClass.dat file was encoded with Base64, which thankfully, you can decode and recover the original UsrClass.dat file!  Base64 decode the contents between the -----BEGIN CERTIFICATE----- and -----END CERTIFICATE----- markers within the transcription log with CyberChef, which you have a local copy of on the Desktop of your analysis machine. 

This file can be used to aid in our investigation. The UsrClass.dat file contains "Shellbags," or artifacts contained within the Windows registry that store user preferences while viewing folders within the Windows Explorer GUI. If you could carve out this information, you could get an idea as to what user activity was performed on the laptop before it was stolen or compromised! For more details and information on Shellbags, you are strongly encouraged to do some extra reading or research. :)

To extract the Shellbags information within this UsrClass.dat file, we will use the "Shellbags Explorer" graphical utility put together by Eric Zimmerman. This utility is found readily available inside the ShellBagsExplorer folder on the Desktop of your Windows machine, with the application name ShellBagsExplorer.exe .

![image](https://user-images.githubusercontent.com/95479102/145355526-22e43e20-1954-4c9b-932c-c8616680f927.png)

![image](https://user-images.githubusercontent.com/95479102/145361800-410f6479-c71c-44a5-acf5-0482f0dc0c04.png)


Read the above and open the ShellBagsExplorer.exe application found in the folder on your Desktop.

With ShellBagsExplorer.exe  open, use the top-bar menu to select File  -> Load offline hive and navigate to the location of where you saved the decoded UsrClass.dat . Load in the UsrClass.dat file and begin to explore the Shellbags discovered!

![image](https://user-images.githubusercontent.com/95479102/145356389-76a11938-93ed-4d66-b4f2-acc57e139410.png)

![image](https://user-images.githubusercontent.com/95479102/145362289-28634548-d19e-49fe-a799-87ebcab4fc1a.png)

Under the Desktop folder, there seems to be a suspicious folder named "SantaRat". Could this be a remote access trojan, that was used for further nefarious activity on Santa's laptop? Unfortunately, from just Shellbags alone, we only have insight into folder names (sometimes files, if we are lucky) and column data within Windows Explorer, but not files... how could we uncover more details?

Drill down into the folders and see if you can find anything that might indicate how we could better track down what this SantaRat really is. What specific folder name clues us in that this might be publicly accessible software hosted on a code-sharing platform?

Additionally, there is a unique folder named "Bag of Toys" on the Desktop! This must be where Santa prepares his collection of toys, and this is certainly sensitive data that the actor could have compromised. What is the name of the file found in this folder? 

![image](https://user-images.githubusercontent.com/95479102/145366621-62054dbd-4316-40e1-a64d-f35461801f05.png)

![image](https://user-images.githubusercontent.com/95479102/145362577-6c8e6561-0a21-4653-a751-66091e7f5e97.png)

Track down this SantaRat software online. It may be just as simple as searching for the name of the software on the suggested website (Github).

Note that the TryHackMe Windows analysis machine does not have Internet access, so you will need to explore in your own web browser.

What is the name of the user that owns the SantaRat repository?

![image](https://user-images.githubusercontent.com/95479102/145363643-6efc2786-f10d-40ab-b115-cfe65a69ffec.png)

Explore the other repositories that this user owns. What is the name of the repository that seems especially pertinent to our investigation?

![image](https://user-images.githubusercontent.com/95479102/145363771-303e06c1-3216-4195-b4ba-69e3055dc35e.png)

Read the information presented in this repository. It seems as if the actor has, in fact, compromised and tampered with Santa's bag of toys! You can review the activity in the transcription logs. It looks as if the actor installed a special utility to collect and eventually exfiltrate the bag of toys. What is the name of the executable that installed a unique utility the actor used to collect the bag of toys?

![image](https://user-images.githubusercontent.com/95479102/145364895-61e02adb-a599-4be0-bc0d-143ea1a95126.png)

In the last transcription log, you can see the activity that this actor used to tamper with Santa's bag of toys! It looks as if they collected the original contents with a UHA archive. A UHA archive is similar to a ZIP or RAR archive, but faster and with better compression rates. It is very rare to see, but it looks the Grinch Enterprises are pulling out all the tricks!

You can see the actor compressed the original contents of the bag of toys with a password. Unfortunately, we are unable to see what the specific password was in these transcription logs! Perhaps we could find it elsewhere...

Following this, the actor looks to have removed everything from the bag of toys, and added in new things like coal, mold, worms, and more!  What are the contents of these "malicious" files (coal, mold, and all the others)?

![image](https://user-images.githubusercontent.com/95479102/145365021-aafb3328-cf94-4b13-90b2-66fc5156a4b4.png)

We know that the actor seemingly collected the original bag of toys. Maybe there was a slight OPSEC mistake, and we might be able to recover Santa's Bag of Toys! Review the actor's repository for its planned operations... maybe in the commit messages, we could find the original archive and the password!

What is the password to the original bag_of_toys.uha archive? (You do not need to perform any password-cracking or bruteforce attempts)

![image](https://user-images.githubusercontent.com/95479102/145363967-54293621-4875-439c-bec2-3d023285cd51.png)

![image](https://user-images.githubusercontent.com/95479102/145363999-61ac4dd6-94df-4fd0-ac7b-2d44a420ebbf.png)

![image](https://user-images.githubusercontent.com/95479102/145364079-95a7ca4c-4fe0-41df-9434-4dc380a5f68c.png)

McSkidy was able to download and save a copy of the bag_of_toys.uha archive, and you have it accessible on the Desktop of the Windows analysis machine. After uncovering the password from the actor's GitHub repository, you have everything you need to restore Santa's original bag of toys!! 

Double-click on the archive on the desktop to open a graphical UHARC extraction utility that has been prepared for you. Using the password you uncovered, extract the contents into a location of your choosing (you might make a "Bag of Toys" directory on the Desktop to save all the files into).

With that, you have successfully recovered the original contents of Santa's Bag of Toys! You can view these in the Windows Explorer file browser to see how many were present.

How many original files were present in Santa's Bag of Toys?

![image](https://user-images.githubusercontent.com/95479102/145364238-352bbdea-18c2-45ed-8af6-b9bb4e8a4e34.png)
