Answer the questions below

Help McSkidy and run nmap -sT 10.10.241.116. How many ports are open between 1 and 100?

![image](https://user-images.githubusercontent.com/95479102/145607478-2a0be3f0-5f22-4b68-be5a-56a00a3591e0.png)

What is the smallest port number that is open?

22

What is the service related to the highest port number you found in the first question?

http

Now run nmap -sS 10.10.241.116. Did you get the same results? (Y/N)

![image](https://user-images.githubusercontent.com/95479102/145608144-bcfc30f4-c3c7-40c6-8bd6-c62450318e1e.png)

If you want Nmap to detect the version info of the services installed, you can use nmap -sV 10.10.241.116. What is the version number of the web server?

![image](https://user-images.githubusercontent.com/95479102/145608762-642a2a33-1e71-4174-8f4f-8ec6f9559cff.png)

By checking the vulnerabilities related to the installed web server, you learn that there is a critical vulnerability that allows path traversal and remote code execution. Now you can tell McSkidy that Grinch Enterprises used this vulnerability. What is the CVE number of the vulnerability that was solved in version 2.4.51?

![image](https://user-images.githubusercontent.com/95479102/145609342-d11707aa-0bb2-47b3-82d5-4492f26c77fd.png)

You are putting the pieces together and have a good idea of how your web server was exploited. McSkidy is suspicious that the attacker might have installed a backdoor. She asks you to check if there is some service listening on an uncommon port, i.e. outside the 1000 common ports that Nmap scans by default. She explains that adding -p1-65535 or -p- will scan all 65,535 TCP ports instead of only scanning the 1000 most common ports. What is the port number that appeared in the results now?

![image](https://user-images.githubusercontent.com/95479102/145614046-ee812369-9d02-4b7a-b435-5f99440fb479.png)

What is the name of the program listening on the newly discovered port?

telnetd

If you would like to learn more about the topics covered in today’s tasks, we recommend checking out the Network Security module.
