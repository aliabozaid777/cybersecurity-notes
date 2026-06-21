# Day 7 - Access Control Basics

## 🎯 Goal
Learn how applications decide who can access pages, files, and actions.

---

## 🧰 Commands Table

| Task | Command | Purpose |
| --- | --- | --- |
| Check normal access | curl http://TARGET_IP/private/ | Tests whether a protected path is accessible. |
| Show response code | curl -i http://TARGET_IP/private/ | Displays status code and headers. |
| Try known paths | curl http://TARGET_IP/admin/ | Checks whether an admin path is exposed. |
| Save response | curl -o response.html http://TARGET_IP/admin/ | Saves the response for later review. |
| Basic auth format | curl -u user:pass http://TARGET_IP/protected/ | Tests HTTP Basic Authentication in a lab. |

---

## 🧠 Key Concepts

| Concept | Meaning |
| --- | --- |
| Authentication | Verifies who the user is, usually with login credentials. |
| Authorization | Decides what the authenticated user is allowed to access. |
| Access Control | Rules that restrict users from pages, files, or actions. |
| 403 Forbidden | The server understood the request but refuses access. |
| 401 Unauthorized | Authentication is required or failed. |

---

## 🧪 Practice Workflow

1. Identify public, user-only, and admin-only areas.
2. Check HTTP status codes for protected paths.
3. Compare what is accessible before and after login in a lab environment.
4. Record evidence: URL, status code, and expected vs actual behavior.

---

## ✅ Checklist

- [ ] Can explain authentication vs authorization.
- [ ] Can recognize 401 and 403 responses.
- [ ] Can test access to a protected route safely.
- [ ] Can describe an access control issue without exploiting real systems.

---

## ⚠️ Notes

> Do not bypass authentication on real websites.
> Testing access control must be limited to legal labs, CTFs, or systems where you have permission.

---

## 📝 Mini Report Template

```md
# Finding Title
Day 7 - Access Control Basics

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
