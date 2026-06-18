# Day 2 – Linux & Networking Basics  

---

## Linux Commands

| أمر | وظيفة سريعة |
|-----|-------------|
| `whoami` | طباعة اسم المستخدم الحالي |
| `sudo` | تنفيذ أوامر بصلاحيات الجذر |
| `ps aux` | عرض جميع العمليات الجارية |
| `top` | شاشة حيّة لاستهلاك المعالج/الذاكرة |
| `kill <PID>` | إيقاف عملية |
| `ip a` | عرض عناوين الشبكة |
| `ss -tulnp` | إظهار المنافذ المفتوحة |
| `wget` | تنزيل ملف عبر HTTP/HTTPS |
| `zip` / `unzip` | ضغط الملفات وفكها |

```bash
# أمثلة سريعة
whoami
sudo apt update
ps aux | grep nmap
kill 1234
