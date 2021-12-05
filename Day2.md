<div class="room-task-desc-data"><span style="font-size:24px"><br></span></p><p><span style="font-size:24px">Story</span></p><p>McSkidy needs to check if any other employee elves have left/been affected by Grinch Industries attack, but the systems that hold the employee information have been hacked. Can you hack them back to determine if the other teams in the Best Festival Company have been affected?</p>

<div>
<p><span style="font-size:24px">Learning Objectives</span></p>

<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/51333ad8cdaade3fcd23986dbd235b5c.png" style="float:right;width:141.24px;height:141.24px" class="note-float-right">
<ul><li>Understanding the underlying technology of web servers and how the web communicates.</li><li>Understand what cookies are and their purpose.</li>
<li>Learn how to manipulate and manage cookies for malicious use.</li></ul>
</div>

<p><span style="font-size:24px">HTTP(S)</span></p><p><span>For your computer and a webserver to communicate with each other, an intermediary protocol is required. This is where the <a class="OdbOR50Y glossary-term" onclick="initPopOver('HTTP', 'OdbOR50Y')">HTTP</a> (Hypertext Transfer Protocol) is introduced! The HTTP protocol is a client-server protocol to provide communication between a client and a webserver. HTTP requests are similar to a standard TCP network request; however, HTTP adds specific headers to the request to identify the protocol and other information.</span><br></p><p style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt"><span style="background:transparent;margin-top:0pt;margin-bottom:0pt"><span>When an <a class="dKmP7Wog glossary-term" onclick="initPopOver('HTTP', 'dKmP7Wog')">HTTP</a> request is crafted, the&nbsp;</span></span><em>method</em><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">&nbsp;and&nbsp;</span><em>target</em><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">&nbsp;header will always be included. The target header will specify what to retrieve from the server, and the method header will specify how.</span></p><p style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt"><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">When retrieving information from a web server, it is common to use the&nbsp;</span><em>GET</em><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">&nbsp;method, such as loading a picture.</span></p><p style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt"><span style="background:transparent;margin-top:0pt;margin-bottom:0pt"><br></span></p><p><span style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt">When sending data to a web server, it is common to use the&nbsp;</span><em>POST</em><span style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt">&nbsp;method, such as sending login information.</span><br></p><p><span style="font-size:16px"><b>Example Request</b></span></p><pre class="  language-http" style="font-family:Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace;font-size:16px;margin-top:0.5em;margin-bottom:0.5em;color:black;background:rgb(245, 242, 240);word-break:normal;overflow-wrap:normal;line-height:1.5;tab-size:4;hyphens:none;padding:1em" tabindex="0"><code class="  language-http" style="font-family:Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace;font-size:1em;color:black;background:none;padding-top:6px;white-space:pre;word-spacing:normal;overflow-wrap:normal;line-height:1.5;tab-size:4;hyphens:none"><span class="token request-line"><span class="token method property">GET</span> <span class="token request-target url">/</span> <span class="token http-version property">HTTP/1.1</span></span>
<span class="token header-name keyword">Host:</span> tryhackme.com
<span class="token header-name keyword">User-Agent:</span> Mozilla/5.0 Firefox/87.0
<span class="token header-name keyword">Referer:</span> https://tryhackme.com/</code></pre><p>Once the server receives a request, it will send back a response, including any requested content if successful and a status code. The status code is used to tell the client browser how the webserver interpreted the request. The most common "successful" status code is <code><span><a class="3tOU4S7s glossary-term" onclick="initPopOver('HTTP', '3tOU4S7s')">HTTP</a> 200 OK</span></code>.<br></p><p><b>Example Response</b></p><pre class="  language-http" style="font-family:Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace;font-size:16px;margin-top:0.5em;margin-bottom:0.5em;background:rgb(245, 242, 240);word-break:normal;overflow-wrap:normal;line-height:1.5;tab-size:4;hyphens:none;padding:1em" tabindex="0"><code class="  language-http" style="font-family:Consolas, Monaco, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, monospace;font-size:1em;background:none;padding-top:6px;white-space:pre;word-spacing:normal;overflow-wrap:normal;line-height:1.5;tab-size:4;hyphens:none"><span class="token response-status"><span class="token http-version property">HTTP/1.1</span> <span class="token status-code number">200</span> <span class="token reason-phrase string">OK</span></span>
<span class="token header-name keyword">Server:</span> nginx/1.15.8
<span class="token header-name keyword">Date:</span> Wednesday, 24 Nov 2021 13:34:03 GMT
<span class="token header-name keyword">Content-Type:</span> text/html
<span class="token header-name keyword">Content-Length:</span> 98<span class="token text-html">

<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>html</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>head</span><span class="token punctuation">&gt;</span></span>
    <span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>title</span><span class="token punctuation">&gt;</span></span>Advent of Cyber<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>title</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>head</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;</span>body</span><span class="token punctuation">&gt;</span></span>
    Welcome To Advent of Cyber!
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>body</span><span class="token punctuation">&gt;</span></span>
<span class="token tag"><span class="token tag"><span class="token punctuation">&lt;/</span>html</span><span class="token punctuation">&gt;</span></span></span></code></pre><p>The protocol itself is only one small piece of the puzzle; once content is retrieved from the web server, your browser needs a way to interpret and render the information sent. Web applications are commonly formatted in HTML (HyperText Markup Language), rendered, and styled in CSS (Cascading Style Sheets). JavaScript is also commonly used to provide additional functionality.<br></p><p>In today's web environment, the use of web frameworks has significantly increased in popularity. Most modern web applications use many web frameworks and other web solutions that an end-user does not see or interact with.<br></p><p>






</p><p>For more information about&nbsp;HTTP&nbsp;requests, methods, and headers, check out the&nbsp;<a href="https://tryhackme.com/room/webfundamentals">Web Fundamentals</a>&nbsp;room!</p><p><span style="font-size:24px">Cookies</span></p>
<div>
<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/44d05b3199fe4c73c810d0f06da27687.png" style="float:right;width:141.24px;height:141.24px" class="note-float-right">
<p><span><a class="L2YJEJEM glossary-term" onclick="initPopOver('HTTP', 'L2YJEJEM')">HTTP</a> is a stateless protocol. When you send requests to a web server, the server cannot distinguish your request from someone else's request.. To solve the stateless problem and identify different users and access levels, the webserver will assign cookies to create and manage a stateful session between client and server.</span></p>
<p>Cookies are tiny pieces of data (metadata)&nbsp;or information locally stored on your computer that are sent to the server when you make a request.</p>
<p>Cookies can be assigned any name and any value allowing the webserver to store any information it wants. Today we will be focusing on authentication cookies, also known as session cookies.&nbsp;Authentication or session cookies are used to identify you and what access level is attached to your session.</p>
</div>

<p>Below is a diagram describing assigning and using a cookie from the initial request to the session request.<br></p>
<p style="text-align:center"><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/64c8a1a54a0e08d9e89701307462f24b.png" style="width:586.328px;height:454.587px"><br></p>


<p>To begin the process, when you send a request such as a login request, your browser will send that information typically as a POST request to the webserver. The web server will verify that it received the data and set a unique cookie; as previously mentioned, cookies are arbitrary, and values are determined by best-practice or the web developer. Once the cookie is assigned, as long as the cookie stays locally stored in your browser, all future GET requests will be automatically sent with that cookie to identify you and your access level. Once the server receives your GET request and cookie, it will locate and de-serialize your session. Deserialization is the process of taking a data format such as JSON and rebuilding it as an object. If successful, the webserver will reply to your request with a 200 response.</p><p>Now that we understand what cookies are and how they are used, let us dive into their contents.<br></p><p>
</p>

<p><span style="font-size:24px">Cookie Components</span></p>

<p>Cookies are made up of 11 different components; you can find an explanation of each component in the table below.<br></p><table class="table table-bordered"><tbody>


<tr><td><b>Component</b></td><td><b>Purpose</b></td><td><b>Example</b></td></tr><tr><td>Name</td><td>Unique cookie identifier (arbitrarily set by web-server). Always paired with the value component.</td><td>SessionID</td></tr><tr><td>Value</td><td>Unique cookie value (arbitrarily set by web-server). Always paired with the name component<br></td><td>sty1z3kz11mpqxjv648mqwlx4ginpt6c<br></td></tr><tr><td>Domain</td><td>Originating domain of the cookie. Sets the scope of the cookie.<br></td><td>.tryhackme.com<br></td></tr><tr><td>Path</td><td>Local path to cookie. Sets the scope of the cookie.<br></td><td>/<br></td></tr><tr><td>Expires/Max-age</td><td>Date/time at which cookies expires<br></td><td>2022-11-11T15:39:04.166Z<br></td></tr><tr><td>Size</td><td>Disk size of the cookie in bytes. This is typically {Name+Value}<br></td><td>91<br></td></tr><tr><td>HttpOnly</td><td>Cookie cannot be accessed through client-side scripts<br></td><td>(indicated by a checkmark)<br></td></tr><tr><td>Secure</td><td>Cookie is only sent over HTTPS<br></td><td>(indicated by a checkmark)<br></td></tr><tr><td>SameSite</td><td>Specifies when a cookie is sent through cross-site requests<br></td><td>none<br></td></tr><tr><td>SameParty</td><td>Extends functionality of <i>SameSite</i> attribute to First-Party sets.&nbsp;<br></td><td>(indicated by a checkmark)<br></td></tr><tr><td>Priority</td><td>Defines the importance of a cookie. Determines whether it should be removed or held on to<br></td><td>High<br></td></tr>
</tbody></table>

<p>Looking at all the components of a cookie may seem intimidating. There is no need to worry as attackers; we only need to concern ourselves with two components: <code>Name</code> and <code>Value</code>; the rest of the components are handled by the webserver.<br></p><p>Cookie components are always prepared in pairs. The main pair is <code>name-value</code>; this will define the name of the cookie and the value of the name. The second pair is the <code>attribute-value</code> pair; this will define an attribute of the cookie and the value of the attribute. Below is an example of what <code>Set-Cookie</code> syntax looks like.<br></p><p style="text-align:center"><code>Set-Cookie: &lt;cookie-name&gt;=&lt;cookie-value&gt;; Domain=&lt;domain-value&gt;; Secure; HttpOnly</code><br></p><p><span style="font-size:24px">Cookie Manipulation</span></p>


<div>
<img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/898063d13e178ef01f6442c84270e40e.png" style="float:left;width:141.24px;height:141.24px" class="note-float-left">
<p>Cookie manipulation is taking a cookie and modifying it to obtain unintended behavior determined by the web developer. Cookie manipulation is possible because cookies are stored locally on your host system, meaning you have complete control over them and modify them as you please.<br></p><p><span style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt">To begin modifying and manipulating cookies, we need to open our developer tools. In Google Chrome, developer tools are known as the&nbsp;</span><em>"Chrome Developer Tools,"</em><span style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt">&nbsp;and in Mozilla Firefox, they are known as the&nbsp;</span><em>"Firefox Developer Tools."</em></p><p>Developer tools can be accessed by pressing <code>F12</code> or <code>Ctrl+Shift+I</code>. Once developer tools are open, to access your cookies, navigate to the <code>Storage</code> tab in Firefox or <code>Application</code> tab in Chrome/Edge; select the <code>Cookies</code> dropdown on the left-hand side of the console.<br></p><p style="text-align:center"><img src="https://tryhackme-images.s3.amazonaws.com/user-uploads/5e73cca6ec4fcf1309f2df86/room-content/fe6e979cce8c9e8396ce40c24a2140b9.png" style="width:954px"><br></p>
</div>

<p>Cookie values may seem random at first; however, they often have an encoded value or meaning behind them that can be decoded to a non-arbitrary value such as a Javascript object.</p><p>From an attacker's perspective, you can decode the cookie value to identify the underlying objects. Once you have identified the underlying objects, you can modify them to what you want. To use the cookie, you will need to encode it back to the original encoding and replace the cookie value. Below is an example of a decoded cookie value.</p><p style="text-align:center"><code>{firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"</code></p><p>






</p><p>Now that we have all of the pieces of cookies and how to manipulate them, we can put them all together to gain unintended access.</p><p>Below is a summary of how cookie values could be manipulated.</p><ol><li>Obtain a cookie value from registering or signing up for an account.</li><li>Decode the cookie value.</li><li>Identify the object notation or structure of the cookie.</li><li>Change the parameters inside the object to a different parameter with a higher privilege level, such as admin or administrator.</li><li style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt;list-style-type:decimal"><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">Re-encode the cookie and insert the cookie into the value space; this can be done by double-clicking the value box.</span></li><li style="color:rgb(14, 16, 26);background:transparent;margin-top:0pt;margin-bottom:0pt;list-style-type:decimal"><span style="background:transparent;margin-top:0pt;margin-bottom:0pt">Action the cookie; this can be done by refreshing the page or logging in.</span></li></ol><p><span style="font-size:24px">Additional Resources</span></p><p><span style="font-size:16px">﻿</span><span style="background-color:transparent;color:rgb(14, 16, 26);font-size:1rem">For more information about HTTP(s) and cookies, check out these other TryHackMe rooms.</span></p><ul>
<li><span><a class="WY9ycMRU glossary-term" onclick="initPopOver('HTTP', 'WY9ycMRU')">HTTP</a>: </span><a href="https://tryhackme.com/jr/httpindetail"></a><a href="https://tryhackme.com/jr/httpindetail">https://tryhackme.com/jr/httpindetail</a></li>
<li>Authentication: <a href="https://tryhackme.com/jr/authenticationbypass" target="_blank">https://tryhackme.com/jr/authenticationbypass</a><a href="https://tryhackme.com/jr/authenticationbypass"></a></li></ul><p style="text-align:center"><span style="font-size:24px">If you're stuck solving the challenge, check out the walkthrough video </span><a href="https://www.youtube.com/watch?v=bovOGgp_TbE&amp;t" target="_blank"><span style="font-size:24px">here</span></a></p></div>

**
Answer the questions below.**


Open the static site in a new tab, here.

![image](https://user-images.githubusercontent.com/95479102/144715569-244ed862-f726-4589-aea7-6df7c0a7f997.png)

Register an account, and verify the cookies using the Developer Tools in your browser.

![image](https://user-images.githubusercontent.com/95479102/144715800-8d908530-8efe-4356-9b66-145a207298de.png)


What is the name of the new cookie that was created for your account?

![image](https://user-images.githubusercontent.com/95479102/144715965-788bd911-5109-40c8-9d09-fa1d9882be7b.png)


What encoding type was used for the cookie value?

What object format is the data of the cookie stored in?

![image](https://user-images.githubusercontent.com/95479102/144715990-217cb6bc-3770-40a1-afc8-a1e7c07c291b.png)


Manipulate the cookie and bypass the login portal.

What is the value of the administrator cookie? (username = admin)

![image](https://user-images.githubusercontent.com/95479102/144716022-0fe34ef7-d5ae-4a54-86b5-41e50da91995.png)

![image](https://user-images.githubusercontent.com/95479102/144716042-84832a35-4b66-4314-be7c-9f64f30f9abb.png)


What team environment is not responding?

What team environment has a network warning?

If you want to learn more about Authentication bypasses, we suggest trying out this room https://tryhackme.com/jr/authenticationbypass  

Tasks released each day get progressively harder (but are still guided with walkthrough videos). Come back tomorrow for Day 3's task, where InsiderPHD will be recording a video walkthrough!

**wip**


7b636f6d70616e793a2022546865204265737420466573746976616c20436f6d70616e79222c206973726567697374657265643a2254727565222c20757365726e616d653a2261646d696e227d
