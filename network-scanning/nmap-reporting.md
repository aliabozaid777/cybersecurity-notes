# Day 10 – Nmap Reporting & Scan Summary  

---

## 1. أمر الفحص الرئيس

```bash
nmap -p- -A -O -vv 192.168.100.8
```

| خيار | ماذا يفعل؟ |
|------|------------|
| `-p-` | يفحص جميع المنافذ (1‑65535) |
| `-A`  | فحص هجومي يشمل NSE scripts |
| `-O`  | تحديد نظام التشغيل |
| `-vv` | إخراج تفصيلي جدًّا |

---

## 2. تفسير النتائج

| حقل في الـOutput | معنى سريع |
|------------------|-----------|
| **PORT** | المنفذ + البروتوكول |
| **STATE** | open / closed / filtered |
| **SERVICE** | اسم الخدمة (http, ssh…) |
| **VERSION** | رقم إصدار الخدمة |

---

## 3. قوالب تقرير سريعة

| قسم | مثال محتوى |
|-----|------------|
| **Scope** | 192.168.100.8/32 – منظور داخلي |
| **Methodology** | Nmap ‎`-p- -A -O` |
| **Findings** | منفذ 22 مفتوح – SSH 7.6p1 (weak ciphers) |
| **Recommendations** | حدّث SSH أو فعّل Key‑based auth |

---

## 4. تحويل XML إلى HTML

```bash
# حفظ ناتج XML
nmap -p- -A -O -oX scan.xml 192.168.100.8

# تحويل إلى HTML بتقرير جميل
xsltproc scan.xml -o report.html
```

> يمكنك رفع **report.html** إلى مجلّد `reports/` لعرضه في GitHub Pages.
