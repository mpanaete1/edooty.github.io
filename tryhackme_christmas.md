<h1>TryHackMe Christams</h1>	

[toc]

#### Day 1

##### Insecure Direct Object Reference (IDOR) Vulnerability

TryHackMe IDOR room [here](https://tryhackme.com/room/idor)

A type of access control vulnerability, when an attacker can gain access to information or actions not indented for them. 

Occurs when a web server receives user supplied input to retrieve objects (file,data,documents). The web application does not validate whether user should have access to the requested object

##### Real World IDOR/Finding IDOR Vulnerabilities

Seeing a product, user, or service identifier in the URL is a must to test. 

**Find IDOR Vulnerabilities**

Changing user-supplied data

​	**Query Component** - data passed in the url when making a request to a website

```
https://website.com/profile?id=23
```

​    ^Protocol     ^Domain      ^Page      ^Query component

by changing the query component can we see other users data using a different ID ?

​	**Post Variables** - examining the contents of forms on a website can reveal fields that could be vulnerable to IDOR exploitation.

```
<form method="POST" action="/update-password">
    <input type="hidden" name"user_id" value="123">
    <div>New Password:</div>
    <div><input type="password" name="new_password"></div>
    <div><input type="submit" value="Change Password">
</form>
```

You can see from the input type line above that the users id is being passed to the webserver in a POST request. Can we change this to change a users password?

​	**Cookies** - Used to remember your session when connected to a website. webservers securely use these to retrieve user information.

sometimes these may store user information in the cookie itself such as user's ID. Changing the value of the cookie could display user information.

```
GET /user-information HTTP/1.1
Host: website.thm
Cookie: user_id=9
User-Agent: Mozilla/5.0 (Ubuntu;Linux) Firefox/94.0
```

---



#### Day 2

[Top](tryhackme_christmas.html)

##### Web Servers

TryHackMe Web Fundamentals [here](https://tryhackme.com/room/webfundamentals)

​	**HTTPS**

client-server protocol to provide communication between a client and a webserver

HTTP adds specific headers to the request to identify the protocol and other information.

- ​	Method and target header will always be included
  - ​    Target header will specify what to receive from the server
  - ​    Method header will specify how
    - ​    When retrieving information from a webserver you commonly use the Get method
    - ​    When sending information to a webserver you commonly use the Post method
- ​    Status codes tell the client browser how the webserver interpreted the request `HTTP 200 OK`

##### Cookies

used to distinguish your request from someone else's. Identifies different users and access levels. 

a tiny piece of meta data containing several types of data determined by the webserver developers

​	**Authentication/session cookies**

​	used to identify you and what access level is attached to your session on the webserver

 1. send a login request to a server

 2. webserver verifies that it received the data and sets/assigns a unique cookie

    all future requests will be automatically set with that cookie to identify you and your access level

3. Once webserver receives future get requests and cookies it will de-seralize your session

   Deserialization if the process of taking a data format such as JSON and rebuilding it as an object

There are several components that make up a cookie but we are only worried about the `name` and `value` since the others are handled by the webserver

Cookies are always prepared in pairs. `name-value` and `attribute-value`

Set-Cookie : `Set-Cookie: <cookie-name>=<cookie-value>; Domain=<domain-value>; Secure; HttpOnly`

​	**Cookie Manipulation**

​	taking a cookie an modifying it to obtain unintended behavior. They are stored locally on your host system, meaning you have complete control.

​	Open developer tools in your browser to find your cookies Application tab (Chrome) , Storage tab (Firefox)

1. Obtain a cookie value from registering or signing up for an account.
2. Decode the cookie value. [CyberChef](https://0x1.gitlab.io/code/CyberChef/)
3. Identify the object notation or structure of the cookie.
4. Change the parameters inside the object to a different parameter with a higher privilege level, such as admin or administrator.
5. Re-encode the cookie and insert the cookie into the value space; this can be done by double-clicking the value box.
6. Action the cookie; this can be done by refreshing the page or logging in.

  More on authentication bypass [here](https://tryhackme.com/jr/authenticationbypass)

---



#### Day 3

[Top](tryhackme_christmas.html)

##### Content Discovery

TryHackMe [Content Discovery](https://tryhackme.com/room/contentdiscovery)

the assets and inner workings of the application that we are testing such as files, folders, or pathways.

A useful technique allowing us to find things that were not suppose to see.

- Config files
- Passwords and secrets
- Backups
- Content management systems
- Administrator dashboards or portals

You can manually search for things like `admin` or `passwords.txt` or use `dirbuster` to automatically do this process

a wordlist will contain several common directory/files names to search for on a website, [SecLists](https://github.com/danielmiessler/SecLists) has a great collection.

Kali default = `/usr/share/wordlists`

`dirb <URL> <wordlist>`

##### Default Credentials

TryHackMe [Authentication Bypass](https://tryhackme.com/jr/authenticationbypass)

Sometimes devs leave default passwords on portals, its always a good idea to try common username/password combinations.

