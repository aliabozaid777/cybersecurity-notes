# Day 12 – Network Discovery Basics  

---

## 1. اكتشاف الأجهزة (Ping Sweep)

```bash
nmap -sn 10.0.0.0/24
```

---

## 2. فحص المنافذ الافتراضية

```bash
nmap -sS 10.0.0.5
```

---

## 3. استخراج أسماء المضيفين

```bash
nmap -sL 10.0.0.0/24 | grep '('
```

---

## 4. توليد خريطة شبكة

```bash
nmap -sn -oX net.xml 10.0.0.0/24
xsltproc net.xml -o netmap.html
```

> افتح **netmap.html** في المتصفح لرؤية الخريطة.
