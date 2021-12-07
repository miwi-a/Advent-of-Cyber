
Deploy the attached VM and look around. What is the entry point for our web application?

![image](https://user-images.githubusercontent.com/95479102/144979517-4ac81e0a-140b-443a-9c90-cc9c662ecc8b.png)

Use the entry point to perform LFI to read the /etc/flag file. What is the flag?

![image](https://user-images.githubusercontent.com/95479102/144982751-1301b09a-3d2f-4bde-a6dd-c73e1b0dd308.png)

Use the PHP filter technique to read the source code of the index.php. What is the $flag variable's value?

![image](https://user-images.githubusercontent.com/95479102/144983373-83b186df-9c5c-4293-b5cd-dd1e258a42fc.png)

![image](https://user-images.githubusercontent.com/95479102/144983410-0a25488e-5ce3-40f6-ba5b-84a1123231e2.png)


McSkidy forgot his login credential. Can you help him to login in order to recover one of the server's passwords?

![image](https://user-images.githubusercontent.com/95479102/144983510-451558d9-be4b-4bee-8ef8-5713e9e5aa75.png)

![image](https://user-images.githubusercontent.com/95479102/144986892-81a65e2f-8249-4f44-ae13-1e82739dec15.png)

![image](https://user-images.githubusercontent.com/95479102/144986928-86203b45-3880-4881-bf6f-8a4b5079431e.png)


Now that you read the index.php, there is a login credential PHP file's path. Use the PHP filter technique to read its content. What are the username and password?



Use the credentials to login into the web application. Help McSkidy to recover the server's password. What is the password of the flag.thm.aoc server? 

![image](https://user-images.githubusercontent.com/95479102/144987166-7de21bc7-355c-42e8-8de7-9aa258ce6031.png)

![image](https://user-images.githubusercontent.com/95479102/144987222-8dc7eb1d-be6f-4e7b-bdfd-a7d46c17503a.png)

![image](https://user-images.githubusercontent.com/95479102/144987271-6d695946-8360-4ed4-b178-c1a491774030.png)


The web application logs all users' requests, and only authorized users can read the log file. Use the LFI to gain RCE via the log file page. What is the hostname of the webserver? The log file location is at ./includes/logs/app_access.log.

![image](https://user-images.githubusercontent.com/95479102/144991425-1ba32e8b-02a4-479d-96a4-17b52bc782d0.png)

![image](https://user-images.githubusercontent.com/95479102/144991497-605db585-1007-417f-a703-3735087bdb57.png)

![image](https://user-images.githubusercontent.com/95479102/144996524-76309951-5115-4ff7-9c8f-9c4a684c1fdb.png)

![image](https://user-images.githubusercontent.com/95479102/145002297-783aeb58-772e-4b3e-95be-761ce3c026d7.png)

![image](https://user-images.githubusercontent.com/95479102/145002100-2d3e0099-2b08-4ea0-87d2-cca9ac80d802.png)

Bonus: The current PHP configuration stores the PHP session files in /tmp. Use the LFI to call the PHP session file to get your PHP code executed. 
