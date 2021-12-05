**Link to room:
https://tryhackme.com/room/adventofcyber3 **

Without further ado, lets go and start with Day 1.

**Story**

The inventory management systems used to create the gifts have been tampered with to frustrate the elves. It's a night shift, and McStocker comes to McSkidy panicking about the gifts all being built wrong. With no managers around to fix the issue, McSkidy needs to somehow get access and fix the system and keep everything on track to be ready for Christmas!

**Learning Objectives**

What is an IDOR vulnerability?
How do I find and exploit IDOR vulnerabilities?

**Challenge Walkthrough.**
**What is an IDOR vulnerability?**

IDOR stands for Insecure Direct Object Reference and is a type of access control vulnerability. An access control vulnerability is when an attacker can gain access to information or actions not intended for them. An IDOR vulnerability can occur when a web server receives user-supplied input to retrieve objects (files, data, documents), and too much trust has been placed on that input data, and the web application does not validate whether the user should, in fact, have access to the requested object.

How do I find and exploit IDOR vulnerabilities?

As previously mentioned, an IDOR vulnerability relies on changing user-supplied data. This user-supplied data can mainly be found in the following three places:

**Query Component:**

Query component data is passed in the URL when making a request to a website. Take, for instance, the following screenshot of a URL.

![image](https://user-images.githubusercontent.com/95479102/144602615-a6625cab-351c-40a9-91e4-58d430d0d6d0.png)

We can breakdown this URL into the following:

**Protocol:** https://

**Domain:** website.thm

**Page:** /profile

**Query Component:** id=23

Here we can see the /profile page is being requested, and the parameter id with the value of 23 is being passed in the query component. This page could potentially be showing us personal user information, and by changing the id parameter to another value, we could view other users data.

**Post Variables:**

Examining the contents of forms on a website can sometimes reveal fields that could be vulnerable to IDOR exploitation. Take, for example, the following HTML code for a form that updates a user's password.
```
<form method="POST" action="/update-password">
    <input type="hidden" name"user_id" value="123">
    <div>New Password:</div>
    <div><input type="password" name="new_password"></div>
    <div><input type="submit" value="Change Password">
</form>
```
You can see from the highlighted line that the user's id is being passed to the webserver in a hidden field. Changing the value of this field from 123 to another user_id may result in changing the password for another user's account.

**Cookies:**

To stay logged into a website such as this one, cookies are used to remember your session. Usually, this will involve sending a session id which is a long string of random hard to guess text such as **5db28452c4161cf88c6f33e57b62a357**, which the webserver securely uses to retrieve your user information and validate your session. Sometimes though, less experienced developers may store user information in the cookie its self, such as the user's ID. Changing the value of this cookie could result in displaying another user's information. See below for an example of how this might look.
```
GET /user-information HTTP/1.1
Host: website.thm
Cookie: user_id=9
User-Agent: Mozilla/5.0 (Ubuntu;Linux) Firefox/94.0
```
Hello Jon!

```
GET /user-information HTTP/1.1
Host: website.thm
Cookie: user_id=5
User-Agent: Mozilla/5.0 (Ubuntu;Linux) Firefox/94.0
```
Hello Martin!


**IDOR in the wild**
Seeing a product, user, or service identifier in the URL or otherwise is a must to test. IDOR vulnerabilities can reveal sensitive information, as well as potentially giving you access to usually restricted site functionality. For security researchers, IDOR vulnerabilities can be impactful, and reporting them can yield a good bug bounty; see this article, where an IDOR vulnerability report to PayPal had a $10,500 payout.



**Challenge Walkthrough**

Click the green "View Site" button at the top right of this task to open up the inventory management system.

Here you'll find a mock browser on the completed orders page showing images of the toys which have been made incorrectly due to the Grinch's tampering!

![image](https://user-images.githubusercontent.com/95479102/144603293-daba99fe-c1d6-4a40-8bac-a08ef3b5b1ca.png)


There are also three other pages on the navigation panel; Builds, Inventory and Your Activity.

The **builds** page shows different toys and the parts they are made up of (as you can see, due to tampering, these are all incorrect)
The **Inventory** page lists the individual items with their corresponding SKU codes.
The Your **Activity** page displays McSkidy's user information, photo and their recent actions on the system.
As we learnt above, an IDOR vulnerability requires changing some kind of user input. Out of all the pages we can navigate to, the only page that has input that can be altered is on the Your Activity page. You'll see in the URL a query component parameter named user_id, which is set to the value of 11 (McSkidy's User Id).



Try changing the **user_id** value in the address bar, and you'll see that the web application tries to load another user's information. Try different numbers between the values 1 - 20 until you find a user who could have been responsible for the tampering on the system.



Clicking on the **Revert** button on the user's actions will roll back the changes and allow the toy-making machine to make properly built toys again. Once all the changes have been reverted, you'll be rewarded with a flag which can be entered below.
    
    
    
**Answer the questions below**

After launching the site, you'll be able to see **Builds**, **Inventory** and **Activity** Page on the uppermost part.
![image](https://user-images.githubusercontent.com/95479102/144601793-e830bebf-3664-4029-9c46-816f9378f4e6.png)

-
![image](https://user-images.githubusercontent.com/95479102/144602152-b81da314-b758-4fd1-a9aa-4c99c20aa944.png)
    
The builds page shows different toys and the parts they are made up of (as you can see, due to tampering, these are all incorrect)

![image](https://user-images.githubusercontent.com/95479102/144602214-a82c5af6-e58d-4ec4-a09a-b6f51d2c633b.png)

The Inventory page lists the individual items with their corresponding SKU codes.

![image](https://user-images.githubusercontent.com/95479102/144603575-f4bbd21d-5bfd-4285-85b1-616a807b9945.png)

The Your Activity page displays McSkidy's user information, photo and their recent actions on the system.

From here, you'll see that the link contains **?user_id=11** which we can manipulate to whatever we want.

##1.) After finding Santa's account, what is their position in the company?

**Assuming Santa would be the user_id=1, I still did a run through from 0 to 23**

![image](https://user-images.githubusercontent.com/95479102/144604141-4ee28569-bb68-4905-b32d-6de9631135c9.png)

**Apparently, he was sitting on user_id = 1. We can see from the screenshot above that his position is **[The Boss!]****

PS: Include the (!) as it is needed on the field.

##2.) After finding McStocker's account, what is their position in the company?

**I was able to locate McStocker on user_id = 3**

![image](https://user-images.githubusercontent.com/95479102/144604675-ba40cad5-8ef6-4346-9767-fea03aeb64c4.png)

We can see from the screenshot above that his position is **[Build Manager]**

##3.) After finding the account responsible for tampering, what is their position in the company?

**As expected, it was the Grinch causing the trouble again, found him on user_id = 9**

![image](https://user-images.githubusercontent.com/95479102/144605157-5604596d-1d28-49cf-9fc4-e017116dc976.png)

We can see from the screenshot above that his position is **[Mischief Manager]**

##4.) What is the received flag when McSkidy fixes the Inventory Management System?

**Given the steps made previously, we were able to locate the one who maliciously tampered the data causing trouble on the workshop. And by clicking the [Revert] Button we were able to roll back all the changes made by the Grinch and fix the issue with the Builds.**

![image](https://user-images.githubusercontent.com/95479102/144605674-7beb2754-2dec-4582-ba43-60a6d67cdbdf.png)

**After reverting all the changes, a flag will be revealed**

![image](https://user-images.githubusercontent.com/95479102/144605958-43338eab-a031-4080-a83b-8be7aacecdbb.png)

##5.) If you want to learn more about IDOR vulnerabilities, we suggest trying out this room https://tryhackme.com/room/idor

That sums up the Day 1 for Advent of Cyber 2021. It was actually pretty easy that beginners will be able to follow through the steps.

See you on to the next tasks.

![image](https://user-images.githubusercontent.com/95479102/144605090-cf1b89b2-daba-4b62-acc5-22281c541ce0.png)
