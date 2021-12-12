
Scan the target server with the IP 10.10.226.20. Remember that MS Windows hosts block pings by default, so we need to add -Pn, for example, nmap -Pn 10.10.226.20 for the scan to work correctly. How many TCP ports are open?

![image](https://user-images.githubusercontent.com/95479102/145716672-0b00db03-1833-42b2-8dc0-4aa4e7edcfd2.png)

Network File System (NFS) is a protocol that allows the ability to transfer files between different computers and is available on many systems, including MS Windows and Linux. Consequently, NFS makes it easy to share files between various operating systems.


In the scan results you received earlier, you should be able to spot NFS or mountd, depending on whether you used the -sV option with Nmap or not. Which port is detected by Nmap as NFS or using the mountd service?

Now that we have discovered an NFS service is listening, let’s check what files are being shared. We can do this using the command showmount. In the terminal below, we run showmount -e 10.10.226.20. The -e or --exports show the NFS server’s export list.
Pentester Terminal

           
pentester@TryHackMe$ showmount -e 10.10.226.20 Export list for 10.10.226.20: /share (everyone) /my-notes (noone)

        

As we can see in the terminal output above, we have two shares, /share and /my-notes. After you have started the attached machine, use the AttackBox terminal to discover the shares on 10.10.226.20.

![image](https://user-images.githubusercontent.com/95479102/145716894-5496d261-8d0d-4322-87ef-4ed6559cad17.png)

How many shares did you find?

How many shares show “everyone”?

Let’s try to mount the shares we have discovered. We can create a directory on the AttackBox using mkdir tmp1, where tmp1 is the directory’s name. Then we can use this directory  we created to mount the public NFS share using: mount 10.10.226.20:/my-notes tmp1.
Pentester Terminal

           
pentester@TryHackMe$ mount 10.10.226.20:/my-notes tmp1 mount.nfs: access denied by server while mounting 10.10.226.20:/my-notes

        

We can see that the mounting has failed. my-notes is not public and requires specific authentication mechanisms that we don’t have access to. Let’s try again with the other folder, share.
Pentester Terminal

           
pentester@TryHackMe$ mount 10.10.226.20:/share tmp1

        

We didn’t get any error messages, so it was a success. Let’s go inside the share to see what’s inside it using cd tmp1, then ls.
Pentester Terminal

           
pentester@TryHackMe$ ls 132-0.txt 2680-0.txt

        

There are two text files. We can open the file using any text editor such as nano FILENAME or something quicker such as less FILENAME.

What is the title of file 2680-0.txt?

![image](https://user-images.githubusercontent.com/95479102/145717154-faaa8b81-dc14-4d1a-849a-936569675991.png)

It seems that Grinch Enterprises has forgotten their SSH keys on our system. One of the shares contains a private key used for SSH authentication (id_rsa). What is the name of the share?

Confidential

We can calculate the MD5 sum of a file using md5sum FILENAME. What is the MD5 sum of id_rsa?

![image](https://user-images.githubusercontent.com/95479102/145717284-15a83789-9d8d-4165-ba4a-4c9be4ee52ef.png)
