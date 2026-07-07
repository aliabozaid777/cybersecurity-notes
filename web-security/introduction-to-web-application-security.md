# Day 8 – Introduction to Web Application Security

> **Course:** Web Application Security Course (Arabic)  
> **Lesson:** 1 – Introduction  
> **Instructor:** Mohamed Sayed – محمد سيد  
> **Repository folder:** `web-security/`  
> **Recommended file path:** `web-security/introduction-to-web-application-security.md`  
> **Status:** Study notes – beginner friendly  

---

## 🎯 Goal

The goal of this lesson is to understand how web applications work before learning how to test them for security issues.

Before studying vulnerabilities like IDOR, Broken Authentication, CSRF, XSS, or SQL Injection, you need to understand the normal flow of a web application:

1. The browser sends a request.
2. The server receives and processes the request.
3. The server may communicate with a database.
4. The server sends a response.
5. The browser renders the result for the user.

---

## 🧠 Big Idea

Web application security is not only about tools.  
It is mainly about understanding how data moves between:

- User
- Browser
- Server
- Database
- APIs

If you understand the normal behavior, you can later recognize abnormal or insecure behavior.

---

# Step-by-Step Explanation

## Step 1 – What is a Web Application?

A **web application** is a program that runs through a browser and communicates with a server over HTTP or HTTPS.

Examples:

- Gmail
- Facebook
- GitHub
- Online stores
- Banking dashboards
- Admin panels

A normal website may only display content, but a web application usually lets the user interact with data, such as logging in, uploading files, buying products, or changing account settings.

---

## Step 2 – Understand the Client

The **Client** is usually the user’s browser.

The client is responsible for showing the page to the user using:

| Technology | Purpose |
|---|---|
| HTML | Page structure |
| CSS | Page design and colors |
| JavaScript | Dynamic behavior and interaction |

Important note:

> Anything that runs on the client side can usually be seen or modified by the user.  
> لذلك لا تعتمد على المتصفح فقط في حماية الصلاحيات أو البيانات الحساسة.

---

## Step 3 – Understand the Server

The **Server** receives requests from the client and decides what response should be returned.

The server may handle:

- Login
- User permissions
- Business logic
- Database queries
- File uploads
- API responses

Common backend technologies:

- PHP
- Python
- Node.js
- Java
- C# / ASP.NET
- Ruby
- Go

Security rule:

> Important security checks must happen on the server side, not only on the client side.

---

## Step 4 – Understand the Database

The **Database** stores application data.

Examples of stored data:

- User accounts
- Password hashes
- Emails
- Orders
- Messages
- Permissions
- Products

Common databases:

- MySQL
- PostgreSQL
- SQLite
- MongoDB
- Microsoft SQL Server

Security risk:

If user input is sent to the database without proper validation or safe queries, vulnerabilities such as SQL Injection may appear.

---

## Step 5 – Understand HTTP Request and Response

When you open a page, the browser sends an **HTTP Request** to the server.

Example request:

```http
GET /login HTTP/1.1
Host: example.com
User-Agent: Mozilla/5.0
Cookie: session=abc123
```

The server replies with an **HTTP Response**.

Example response:

```http
HTTP/1.1 200 OK
Content-Type: text/html
Set-Cookie: session=xyz789; HttpOnly; Secure

<html>Login Page</html>
```

As a security learner, you should learn to read both the request and the response.

---

## Step 6 – Understand Common HTTP Methods

| Method | Meaning | Example Use |
|---|---|---|
| GET | Request data | Open a page or view a product |
| POST | Send data | Login form or create account |
| PUT | Update data | Update profile through an API |
| PATCH | Partial update | Change one field only |
| DELETE | Delete data | Delete a post or item |

Important note:

> The HTTP method alone does not make an action secure.  
> The server must still verify authentication, authorization, and input validation.

---

## Step 7 – Understand Status Codes

| Code | Meaning | Security Note |
|---|---|---|
| 200 | OK | Request succeeded |
| 301 / 302 | Redirect | Often used after login/logout |
| 400 | Bad Request | Request format is invalid |
| 401 | Unauthorized | Login is required or failed |
| 403 | Forbidden | User is known but not allowed |
| 404 | Not Found | Resource does not exist or is hidden |
| 500 | Server Error | May reveal backend issues if verbose |

---

## Step 8 – Understand Cookies and Sessions

HTTP is stateless, which means each request is independent by default.

To remember users after login, applications often use:

- Cookies
- Sessions
- Tokens

Example:

```http
Cookie: sessionid=8f7a9c1d
```

The session tells the server which user is sending the request.

Security risks related to sessions:

- Weak session IDs
- Session fixation
- Missing `HttpOnly`
- Missing `Secure`
- Missing `SameSite`
- Session not expiring after logout

---

## Step 9 – Authentication vs Authorization

| Concept | Meaning | Example |
|---|---|---|
| Authentication | Verifies who you are | Login with email and password |
| Authorization | Verifies what you can access | Normal user cannot open admin panel |

Simple explanation:

- **Authentication:** Are you really Ali?
- **Authorization:** Is Ali allowed to access this page or action?

Many web vulnerabilities happen because authorization is missing or weak.

---

## Step 10 – Where Do Web Vulnerabilities Come From?

Most web vulnerabilities come from mistakes such as:

- Trusting user input
- Weak access control
- Bad session management
- Poor input validation
- Exposing sensitive information
- Misconfigured servers
- Unsafe file uploads
- Missing security headers
- Broken business logic

Examples of vulnerabilities you will study later:

- Broken Authentication
- Broken Access Control
- IDOR
- CSRF
- XSS
- SQL Injection
- File Upload Vulnerabilities
- Directory Listing

---

## Step 11 – Tools Used in Web Security Learning

| Tool | Purpose |
|---|---|
| Browser Developer Tools | Inspect requests, responses, HTML, JS, cookies |
| Burp Suite | Intercept and analyze HTTP traffic |
| curl | Send HTTP requests from terminal |
| Postman | Test APIs |
| OWASP Juice Shop | Legal vulnerable web app for practice |
| DVWA | Legal vulnerable web app for practice |
| PortSwigger Academy | Web security labs |
| TryHackMe | Guided cybersecurity labs |

---

# Safe Practice Lab

> Only practice on legal targets such as your own lab, TryHackMe, PortSwigger Academy, DVWA, or OWASP Juice Shop.

## Lab 1 – View HTTP Headers

```bash
curl -I https://example.com
```

What to observe:

- Status code
- Server headers
- Content-Type
- Cache headers

---

## Lab 2 – View Full Response

```bash
curl -i https://example.com
```

What to observe:

- Response headers
- Response body
- Status code

---

## Lab 3 – Use Browser Developer Tools

1. Open the browser.
2. Press `F12` or open Developer Tools.
3. Go to the **Network** tab.
4. Visit a website you are allowed to browse.
5. Click on any request.
6. Review:
   - Request URL
   - Method
   - Status code
   - Request headers
   - Response headers

---

# Mini Checklist

- [ ] I can explain what a web application is.
- [ ] I can explain the difference between client and server.
- [ ] I understand the role of the database.
- [ ] I can identify HTTP request and response.
- [ ] I know the difference between GET and POST.
- [ ] I know what 200, 401, 403, 404, and 500 mean.
- [ ] I understand the basic idea of cookies and sessions.
- [ ] I can explain authentication vs authorization.
- [ ] I understand why testing must be done only in legal labs.

---

# Common Beginner Mistakes

## Mistake 1 – Starting with tools before understanding HTTP

Tools are useful, but they are not enough.  
You must understand what the tool is showing you.

## Mistake 2 – Thinking client-side protection is enough

JavaScript checks can be bypassed by modifying requests.  
Important checks must be done on the server.

## Mistake 3 – Testing real websites without permission

This is illegal and dangerous.  
Always practice inside legal labs or systems where you have clear permission.

## Mistake 4 – Memorizing vulnerabilities without understanding the normal flow

You need to understand normal behavior first.  
Then you can recognize insecure behavior.

---

# Quick Review Questions

## 1. What is the difference between a website and a web application?

A website may only display content, while a web application allows interaction with data and actions such as login, upload, purchase, or account management.

## 2. What is the client?

The client is usually the browser that sends requests and displays responses.

## 3. What is the server?

The server receives requests, processes logic, communicates with the database, and sends responses.

## 4. Why is HTTP important in web security?

Because most web attacks involve manipulating requests, responses, parameters, cookies, headers, or sessions.

## 5. What is the difference between authentication and authorization?

Authentication verifies identity.  
Authorization verifies permissions.

---

# Personal Notes

Write your own notes here after watching the lesson:

```text
- New thing I learned:
- Thing I did not understand:
- Tool I want to practice:
- Question for review:
```

---

# Summary

This lesson introduces the foundation of web application security.  
The most important point is that web security starts with understanding how web applications normally work.

You should now understand:

- Client
- Server
- Database
- HTTP request/response
- Methods
- Status codes
- Cookies and sessions
- Authentication and authorization
- Safe legal practice environments

Next recommended lesson:

> Broken Authentication & Access Control

---

# References

- OWASP Web Security Testing Guide
- OWASP Top 10
- PortSwigger Web Security Academy
- TryHackMe
- Course: Web Application Security Course (Arabic) – Mohamed Sayed
