# IDOR Lab Report — Insecure Direct Object References

> **Category:** Web Security / Access Control  
> **Platform:** PortSwigger Web Security Academy  
> **Lab:** Insecure direct object references  
> **Status:** Solved  
> **Environment:** Authorized lab only

---

## 1. Summary

This lab demonstrates an **Insecure Direct Object Reference (IDOR)** vulnerability.

The application stores user chat transcripts on the server and retrieves them using static file paths. By changing the transcript file name in the request, it was possible to access another user's chat transcript and extract sensitive information.

---

## 2. Vulnerability

**Insecure Direct Object Reference (IDOR)** occurs when an application exposes a direct reference to an internal object, such as a file, user ID, invoice ID, or transcript name, without checking whether the current user is authorized to access it.

In this lab, the vulnerable object was a chat transcript file.

Example pattern:

```http
GET /download-transcript/2.txt HTTP/1.1
Host: LAB-HOST
```

Changing the file number allowed access to another transcript:

```http
GET /download-transcript/1.txt HTTP/1.1
Host: LAB-HOST
```

---

## 3. Steps to Reproduce

1. Opened the lab in **Burp Browser**.
2. Navigated to the **Live chat** feature.
3. Sent a test message in the chat.
4. Downloaded or viewed the chat transcript.
5. Captured the request in:

```text
Proxy → HTTP history
```

6. Found a request similar to:

```http
GET /download-transcript/2.txt HTTP/1.1
```

7. Sent the request to **Repeater**.
8. Modified the transcript file number:

```http
GET /download-transcript/1.txt HTTP/1.1
```

9. Sent the modified request.
10. The server returned another user's transcript.
11. The transcript contained the password for the user `carlos`.
12. Logged in as `carlos` using the discovered password.
13. The lab was solved.

---

## 4. Root Cause

The application allowed access to transcript files based only on the file name in the URL.

The server did not verify whether the authenticated user was allowed to access the requested transcript.

---

## 5. Impact

An attacker could use this vulnerability to:

- Access other users' private chat transcripts.
- Extract sensitive data such as passwords or personal information.
- Enumerate transcript files by changing numbers in the URL.
- Compromise user accounts if credentials are exposed.

---

## 6. Recommended Fix

The server should enforce authorization checks before returning any transcript file.

Good fixes include:

- Verify that the requested transcript belongs to the authenticated user.
- Store transcript ownership in the database.
- Avoid exposing predictable file names.
- Do not rely on hidden links or UI restrictions.
- Prevent sensitive information, such as passwords, from being stored in chat logs.
- Return `403 Forbidden` or `404 Not Found` for unauthorized transcript access.

Example secure logic:

```pseudo
current_user = session.user

transcript = database.find_transcript(
    id = requested_transcript_id,
    owner = current_user.id
)

if transcript does not exist:
    return 404

return transcript
```

---

## 7. Key Lesson

The main issue in IDOR is not the ID itself.  
The real issue is trusting user-controlled input without checking authorization on the server side.

Every request that accesses an object must answer this question:

> Is this user allowed to access this exact object?

If the answer is not checked by the server, the application may be vulnerable.

---

## 8. Tools Used

- Burp Suite Community Edition
- Burp Browser
- Proxy HTTP history
- Repeater
- PortSwigger Web Security Academy lab environment

---

## 9. Notes

- This test was performed only in an authorized training lab.
- Real websites must not be tested without permission.
- IDOR vulnerabilities are part of the broader **Broken Access Control** category.
- Always document IDOR findings with: request, modified request, response, impact, and recommended fix.

---
