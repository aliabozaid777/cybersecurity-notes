# Day 6 - Directory Listing & Web Enumeration

## 🎯 Goal
Understand how exposed directories and files can leak sensitive information during web reconnaissance.

---

## 🧰 Commands Table

| Task | Command | Purpose |
| --- | --- | --- |
| Start a simple web server | python3 -m http.server 8000 | Hosts current folder on port 8000 for testing. |
| Check target in browser | http://TARGET_IP:8000/ | View available files/directories from the browser. |
| Download visible file | wget http://TARGET_IP:8000/file.txt | Downloads a file from the server. |
| Download with curl | curl -O http://TARGET_IP:8000/file.txt | Downloads and saves the remote file using its original name. |
| Check headers | curl -I http://TARGET_IP:8000/ | Shows HTTP response headers only. |
| Recursive listing test | wget -r http://TARGET_IP:8000/ | Recursively mirrors accessible files for lab practice only. |

---

## 🧠 Key Concepts

| Concept | Meaning |
| --- | --- |
| Directory Listing | A web server feature/misconfiguration that shows files inside a folder. |
| Index Page | The default page served by a web server, commonly index.html. |
| Information Disclosure | Leaking files, names, paths, backups, or configs that should not be public. |
| Reconnaissance | The first phase where you gather visible information about a target. |

---

## 🧪 Practice Workflow

1. Open the target in the browser and observe whether files are listed.
2. Use curl or wget to request files directly.
3. Look for backup files, notes, config names, or exposed folders.
4. Document the finding clearly without modifying the target.

---

## ✅ Checklist

- [ ] Can identify a directory listing page.
- [ ] Can download a file using wget and curl.
- [ ] Can explain why exposed folders are risky.
- [ ] Can write a short note describing the evidence found.

---

## ⚠️ Notes

> Only test systems you own or have permission to test.
> Directory listing is not always a vulnerability by itself, but it becomes risky when sensitive files are exposed.

---

## 📝 Mini Report Template

```md
# Finding Title
Day 6 - Directory Listing & Web Enumeration

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
