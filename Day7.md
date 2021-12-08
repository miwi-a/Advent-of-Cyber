Interact with the MongoDB server to find the flag. What is the flag?

![image](https://user-images.githubusercontent.com/95479102/145145768-132c125f-c23c-48d4-a86b-4be94df3e335.png)

We discussed how to bypass login pages as an admin. Can you log into the application that Grinch Enterprise controls as admin and retrieve the flag?

Use the knowledge given in AoC3 day 4 to setup and run Burp Suite proxy to intercept the HTTP request for the login page. Then modify the POST parameter.

![image](https://user-images.githubusercontent.com/95479102/145220286-5e6e7df4-e3ee-42c7-9018-5ce1317a6d41.png)

![image](https://user-images.githubusercontent.com/95479102/145219467-99274a65-af95-41c2-ba75-2e632644588a.png)

Once you are logged in, use the gift search page to list all usernames that have guest roles. What is the flag?

![image](https://user-images.githubusercontent.com/95479102/145219892-acb9e3b2-0142-402b-8bbd-ab68e01134e2.png)

![image](https://user-images.githubusercontent.com/95479102/145219932-d4dac2e8-25fa-47eb-9038-8e881230c8d3.png)


Use the gift search page to perform NoSQL injection and retrieve the mcskidy record. What is the details record?

![image](https://user-images.githubusercontent.com/95479102/145220100-1038a3b4-5037-41d6-b7b0-77f72d94f24a.png)
