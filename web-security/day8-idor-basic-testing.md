# Day 8 - IDOR & Broken Access Control Basics

## 🎯 Goal
Understand how insecure object references can expose another user’s data in a controlled lab.

---

## 🧰 Commands Table

| Task | Command | Purpose |
| --- | --- | --- |
| Request user object | curl http://TARGET_IP/user?id=1 | Requests object/user number 1 in a lab app. |
| Change object ID | curl http://TARGET_IP/user?id=2 | Tests whether another object is exposed. |
| Show full response | curl -i http://TARGET_IP/user?id=2 | Shows headers, status code, and body. |
| Use saved cookie | curl -b cookies.txt http://TARGET_IP/user?id=2 | Sends a saved session cookie in a lab. |
| Save cookies | curl -c cookies.txt http://TARGET_IP/login | Stores cookies from a lab login flow. |

---

## 🧠 Key Concepts

| Concept | Meaning |
| --- | --- |
| IDOR | Insecure Direct Object Reference: accessing objects by changing IDs without proper authorization checks. |
| Object Reference | A value like id=5, file=report.pdf, or account=1002 that points to a resource. |
| Broken Access Control | A broad category where users can access actions or data they should not access. |
| Horizontal Access | Accessing another user’s data at the same privilege level. |
| Vertical Access | Accessing admin or higher-privilege functionality as a normal user. |

---

## 🧪 Practice Workflow

1. Log in as a normal test user in a lab.
2. Find an object ID in the URL or request.
3. Change the ID and observe whether the application blocks access.
4. Write down the exact request and the unexpected data exposure.

---

## ✅ Checklist

- [ ] Can explain IDOR in simple words.
- [ ] Can identify object references in URLs or requests.
- [ ] Can distinguish horizontal and vertical access issues.
- [ ] Can write safe evidence without sharing sensitive data.

---

## ⚠️ Notes

> Never test IDOR on real accounts or real users without authorization.
> In reports, avoid exposing personal data. Mask or summarize sensitive fields.

---

## 📝 Mini Report Template

```md
# Finding Title
Day 8 - IDOR & Broken Access Control Basics

## Target
TARGET_IP / URL

## What I Tested
Describe what you checked.

## Evidence
Add command output, screenshot reference, or response details.

## Impact
Explain the risk in simple words.

## Recommended Fix
Explain how to reduce or fix the issue.
```
