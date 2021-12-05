<div class="card-body task-complete">
                            <div class="room-task-desc">
            <div class="room-task-desc-data"><div class="btn-group mb-3 ml-3 float-right">
</div> <p style="text-align:center"><i>Grinch Enterprises have also tried to block communication between anyone at the company. They've locked everyone out of their email systems and McSysAdmin has also lost access to their admin panel. Can you find the admin panel and help restore communication for the Best Festival Company.</i></p><hr><h2><br></h2><h2>Learning Objectives</h2><p>
</p><p>In today's task, we're going to be using our investigatory skills and techniques to discover un-listed content, and attempt some common authentication using the clues around us.</p><p><br></p><h2>What is Content Discovery &amp; Why is it Useful?</h2><p>Before we begin looking for content, let's define what "content" actually is. Content is the assets and inner workings of the application that we are testing. Contents can be files, folders, or pathways that weren't necessarily intended to be accessed by the general public.</p><p>For example, you may have a blog, where you post about your tasty treats! You want everyone to view all of your delicious snacks, but you don't want everyone to be able to manage what delicious snacks are up for review - You may hide the administrator panel away from the public!</p><p>

 ![image](https://user-images.githubusercontent.com/95479102/144710456-30efadd3-f8cd-456b-86d3-848c5e508ac8.png)
              
<br>Let's expand on this. Web servers, unless configured otherwise, are designed to serve these files and folders, as long as you know the names.</p><p>

![image](https://user-images.githubusercontent.com/95479102/144710498-d1c1905e-fb48-46c1-9c49-fd1239733ba1.png)
             
              
<br></p><p><span style="font-size:1rem">Content discovery is a useful technique to have in our arsenal because it allows us to find things that we aren't supposed to see. For example, we may be able to find:</span><br></p><ul>
<li>Configuration files</li>
<li>Passwords and secrets</li>
<li>Backups</li>
<li>Content management systems</li>
<li>Administrator dashboards or portals</li>
</ul><p>
</p><p>These are just some examples of the types of information that we may be able to uncover by discovering content. We can find these pieces of information because they are stored in either a folder (which will have a name) or a file (which will have both a name and extension). This means that we can search for files by their extension, for example, discovering text files with the extension of <code>.txt</code>.</p><p><span style="font-size:1rem">You can do this manually by thinking of some names such as "<i>admin</i>" or "<i>passwords.txt</i>" and navigating to it in your browser. However, we can use tools to do this process for us at a considerably faster rate. Enter Dirbuster. Dirbuster is a tool that we can use to automate this process for us. The tool works by accepting a wordlist which is a file containing everything that we want to search for, and then a few other arguments. Let's demonstrate this into the snippets below:</span><br></p>
<div class="terminal-container">
    <div class="terminal-content">
        <div class="terminal-top">
            My Wordlist
        </div>
        <pre class="terminal-code language-shell-session" tabindex="0">           <code class=" language-shell-session"><span class="token command"><span class="token info punctuation"><span class="token user">cmnatic@thm</span></span><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> wordlist.txt</span></span>

<span class="token output">admin/
docs/
config/
install/
install-en/
</span></code>
        </pre></div></div><p>Dirbuster will scan the website "santascookies.thm" for the folders listed within this wordlist. To use Dirbuster to discover content on this site, we would use the command <code>dirb</code> and provide some information such as the URL of the website and the location of the word list. Our final command would look like something similar to the snippet below::</p><p><br></p><div class="terminal-container">
    <div class="terminal-content">
        <div class="terminal-top">
            An example Dirbuster command
        </div>
        <pre class="terminal-code language-shell-session" tabindex="0">           <code class=" language-shell-session"><span class="token command"><span class="token info punctuation"><span class="token user">cmnatic@thm</span></span><span class="token shell-symbol important">$</span> <span class="token bash language-bash">dirb http://santascookies.thm/ /usr/share/wordlists/mywordlist.txt</span></span>
</code>
        </pre>
    </div>
</div>
<p>In the above, we have provided Dirbuster the following commands:</p><ol>
<li>The URL of the website</li>
<li>The location (full path) on our attacking machine of our wordlist. If you are unfamiliar with this, check out <a href="https://tryhackme.com/module/linux-fundamentals" target="_blank">Linux Fundamentals</a>.</li>
</ol><p>

</p><p>Now, once we execute this command, Dirbuster will search for the existence of a directory on the website using every value in the wordlist that we have created.&nbsp;</p>

<div class="terminal-container">
    <div class="terminal-content">
        <div class="terminal-top">
            Listing example wordlists to use with Dirbuster
        </div>
        <pre class="terminal-code language-shell-session" tabindex="0">           <code class=" language-shell-session"><span class="token command"><span class="token info punctuation"><span class="token user">cmnatic@thm</span><span class="token punctuation">:</span><span class="token path">/usr/share/wordlists/dirb</span></span><span class="token shell-symbol important">#</span> <span class="token bash language-bash"><span class="token function">ls</span> </span></span>

<span class="token output">big.txt     euskera.txt            mutations_common.txt  spanish.txt
catala.txt  extensions_common.txt  others                stress
common.txt  indexes.txt            small.txt             vulns</span></code>
        </pre>
    </div>
</div>

<p><br></p><p>Your ability to discover content is only as good as your wordlist. You will find another collection of open-source wordlist such as <a href="https://github.com/danielmiessler/SecLists" target="_blank">SecLists</a>, where you may be able to use a combination of context and wordlist to discover content.</p><p><br></p><h2>Default Credentials</h2><p>Web applications and services often come with a default pair of credentials. Developers leave these credentials in place so that you can quickly get started with the platform (with the hopes that you will change them). However, as you'll come to discover, not everyone does, or in fact, applications often include other accounts that are not well documented. SecLists also provide a wordlist for default credentials, which you can find <a href="https://github.com/danielmiessler/SecLists/tree/master/Passwords/Default-Credentials" target="_blank">here</a>.</p><p>For example, take a guess at using some common usernames and password combinations for privileged users. This could include:</p><table class="table table-bordered"><tbody><tr><td style="background:#efefef"><b>Count</b></td><td style="background:#efefef"><b>Username</b></td><td style="background:#efefef"><b>Password</b></td></tr><tr><td>#1</td><td>administrator</td><td>administrator</td></tr><tr><td>#2<br></td><td>administrator</td><td>password123</td></tr><tr><td>#3<br></td><td>administrator</td><td>letmein</td></tr></tbody></table><p>Sometimes, these credentials are stored in the web applications configuration files or public documentation. For example, this application, "BikeIT", is an open-source application for registering your Bicycle to a community page. The administrator is enabled by default, with credentials provided in both the documentation and source code.</p><p style="text-align:center">

![image](https://user-images.githubusercontent.com/95479102/144710844-f663f23e-4026-40d9-a24d-b343c0f4ac30.png)
            
</p><p style="text-align:center">The photo above shows the "Read Me" documentation (or instructions) for the web application.</p><p style="text-align:center"><code>$username="Administrator";</code></p><p style="text-align:center"><code>$password="letmein123"; //change this</code></p><p style="text-align:center">The source code contains these default credentials too.</p><hr><p style="text-align:center"></p><p style="text-align:center">Unless the administrator installing this application changes the credentials, anyone will be able to log in using them if they know to look for these details being published (such as they usually are with open-source projects), or are capable of guessing them.</p><p><br></p><p style="text-align:center">For today's task, you will need to deploy the <b>vulnerable machine attached to this task</b> by pressing the green "Start Machine" button at the <b>top right of this task</b> <b>and</b> the<b> TryHackMe AttackBox</b><span style="font-size:1rem">, which can be deployed by pressing the "Start AttackBox" button located at the<b> top-right of the room</b>.</span></p><p style="text-align:center"><br></p><hr><h2><br></h2><h2>Additional Resources</h2><p>If you are interested in learning more&nbsp; (or wish to apply your knowledge) about content discovery and authentication bypass, check out the following rooms on TryHackMe:</p><ul><li><a href="https://tryhackme.com/jr/contentdiscovery" target="_blank">Content Discovery</a></li><li><a href="https://tryhackme.com/jr/authenticationbypass" target="_blank">Authentication Bypass&nbsp;&nbsp;</a></li></ul><p></p></div>
        </div>
        
 <div class="room-questions-split vertical-align-custom hacker-green">
            <div>Answer the questions below</div>
        </div>
        

  
1.) Using a common wordlist for discovering content, enumerate http://MACHINE_IP to find the location of the administrator dashboard. What is the name of the folder?

![image](https://user-images.githubusercontent.com/95479102/144711361-5d0e157c-8533-429e-bb53-c6aa636e5a3b.png)
This is how the site's homepage look like.

I just used some wordlists containing common words which I found in my machine. There are actually multiple ways to enumerate, in my case I used gobuster.
  
![image](https://user-images.githubusercontent.com/95479102/144711528-e4bd3450-3a6c-452f-9826-402ebd90e9d7.png)

With that, I was able to locate /**admin**/

![image](https://user-images.githubusercontent.com/95479102/144711557-dbd780b0-dc07-4423-a413-fa211dc01031.png)

  
2.) In your web browser, try some default credentials on the newly discovered login form for the "administrator" user. What is the password?

![image](https://user-images.githubusercontent.com/95479102/144711583-24328463-5014-4c74-8ada-f9bb59bde0e1.png)
 
 Given the table above, which consists of commonly used default credentials. I was able to login using u**sername: administrator and password: administrator**

3.) Access the admin panel. What is the value of the flag?

 After successfull login, a flag will be shown on the redirected page.
  ![image](https://user-images.githubusercontent.com/95479102/144711668-417ab2cb-14ea-4eaa-947b-a2b63735d02e.png)

That concludes Day 3 of Advent of Cyber 2021. 
  
  
