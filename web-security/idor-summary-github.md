# IDOR — Insecure Direct Object Reference

> **Status:** Web Security / Access Control  
> **Environment:** Authorized labs only  
> **Goal:** Understand how IDOR happens, how to test it safely, and how to prevent it.

---

## Summary

**IDOR** is a type of **Broken Access Control** vulnerability.  
It happens when an application uses a user-controlled value, such as `id`, `userId`, file name, or object ID, to access data directly without checking whether the current user is allowed to access that object.

Example idea:

```http
GET /my-account?id=1001
```

If changing the value to another user’s ID returns their private data:

```http
GET /my-account?id=1002
```

then the application may be vulnerable to **IDOR**.

---

## Why IDOR Happens

The problem is not the presence of an ID in the request.  
The real problem is that the server trusts the ID from the client without proper authorization checks.

Common vulnerable places:

- Query parameters: `?id=123`
- URL paths: `/users/123`
- JSON body values: `"userId": 123`
- File names: `/files/12345.txt`
- UUIDs or GUIDs exposed in another place

---

## Horizontal vs Vertical Access Control

| Type | Meaning | Example |
|---|---|---|
| Horizontal IDOR | A normal user accesses another normal user’s data | User A reads User B’s invoice |
| Vertical IDOR | A low-privilege user accesses higher-privilege data or functions | Normal user accesses admin resource |

---

## Simple Testing Flow

1. Log in to an authorized lab environment.
2. Use the application normally and capture requests with **Burp Suite**.
3. Look for object references such as `id`, `userId`, `file`, `invoice`, or `account`.
4. Send the request to **Repeater**.
5. Change the object reference to another valid value.
6. Compare the response.
7. If unauthorized data appears, document the issue clearly.

---

## Example HTTP Request

Original request:

```http
GET /my-account?id=wiener HTTP/1.1
Host: lab.example.com
Cookie: session=YOUR_SESSION_COOKIE
```

Modified request:

```http
GET /my-account?id=carlos HTTP/1.1
Host: lab.example.com
Cookie: session=YOUR_SESSION_COOKIE
```

If the second request returns data for `carlos`, this indicates an access control issue.

---

## Example curl Commands

```bash
# Request your own account page
curl -i -b "session=YOUR_SESSION_COOKIE" \
  "https://LAB_HOST/my-account?id=wiener"

# Test access to another user object
curl -i -b "session=YOUR_SESSION_COOKIE" \
  "https://LAB_HOST/my-account?id=carlos"
```

> Replace `LAB_HOST`, `YOUR_SESSION_COOKIE`, and usernames/IDs with values from your own authorized lab.

---

## Detection Checklist

- [ ] Is there a user-controlled object reference?
- [ ] Can the ID, username, filename, or UUID be modified?
- [ ] Does the server return another user’s data?
- [ ] Does the response status stay `200 OK` after changing the object?
- [ ] Is sensitive data leaked in the response body?
- [ ] Is access denied only in the UI but not on the server?
- [ ] Are identifiers predictable, such as `1`, `2`, `3`?

---

## Impact

A successful IDOR vulnerability may allow an attacker to:

- Read private user data
- Download files belonging to other users
- Access invoices, tickets, or messages
- Modify or delete another user’s resources
- Escalate privileges in some cases

---

## Recommended Fix

The server must verify authorization for every object access.

Good practices:

- Enforce **server-side authorization checks**.
- Check whether the current user owns the requested object.
- Do not rely on hiding buttons or links in the UI.
- Do not trust `userId` or `id` values sent by the client.
- Use unpredictable IDs only as defense-in-depth, not as the main protection.
- Apply authorization checks in the data access layer when possible.
- Log suspicious enumeration attempts.

Example secure logic:

```pseudo
current_user = session.user

invoice = database.find_invoice(
    id = requested_invoice_id,
    owner = current_user.id
)

if invoice does not exist:
    return 404 or 403
```

---

## Lab Report Template

```md
# IDOR Lab Report

## Vulnerability
Insecure Direct Object Reference (IDOR)

## Target
Authorized lab environment only.

## Summary
The application allowed access to another user's object by changing an object reference in the request.

## Steps to Reproduce
1. Logged in as a normal user.
2. Captured the target request using Burp Suite.
3. Found a user-controlled object reference.
4. Modified the object reference to another valid value.
5. The server returned unauthorized data.

## Impact
A normal user may access data belonging to another user.

## Recommended Fix
The server should verify that the authenticated user is authorized to access the requested object before returning it.
```

---

## Notes

- Always test only in legal and authorized environments.
- Do not test real websites without permission.
- Document every lab with: **summary + steps + impact + fix**.
- Keep screenshots or Burp requests as evidence when writing reports.

---

## References

- PortSwigger Web Security Academy — IDOR  
  https://portswigger.net/web-security/access-control/idor

- PortSwigger Lab — Insecure Direct Object References  
  https://portswigger.net/web-security/access-control/lab-insecure-direct-object-references

- OWASP IDOR Prevention Cheat Sheet  
  https://cheatsheetseries.owasp.org/cheatsheets/Insecure_Direct_Object_Reference_Prevention_Cheat_Sheet.html

- OWASP Broken Access Control  
  https://owasp.org/www-community/Broken_Access_Control

---
