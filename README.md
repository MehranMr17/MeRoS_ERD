<div align="center">

<img src="https://img.shields.io/badge/MeRoS-ERD%20Editor-185FA5?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAzMiAzMiI+PHJlY3Qgd2lkdGg9IjMyIiBoZWlnaHQ9IjMyIiByeD0iNyIgZmlsbD0iIzE4NUZBNSIvPjxyZWN0IHg9IjYiIHk9IjYiIHdpZHRoPSI4IiBoZWlnaHQ9IjIwIiByeD0iMiIgZmlsbD0id2hpdGUiIG9wYWNpdHk9Ii45Ii8+PHJlY3QgeD0iMTgiIHk9IjE0IiB3aWR0aD0iOCIgaGVpZ2h0PSIxMiIgcng9IjIiIGZpbGw9IndoaXRlIi8+PGNpcmNsZSBjeD0iMTAiIGN5PSIxMCIgcj0iMiIgZmlsbD0iIzRkOGVmMCIvPjxjaXJjbGUgY3g9IjIyIiBjeT0iMTgiIHI9IjIiIGZpbGw9IiMzZWNmNzQiLz48L3N2Zz4=" alt="MeRoS ERD Editor">

# MeRoS ERD Editor

**ابزار طراحی بصری دیاگرام رابطه-موجودیت (ERD) — کاملاً آفلاین، بدون نیاز به سرور**

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live%20Demo-4d8ef0?style=flat-square&logo=github)](https://mehranmr17.github.io/MeRoS_ERD/)
[![License](https://img.shields.io/badge/License-MIT-3ecf74?style=flat-square)](LICENSE)
[![Version](https://img.shields.io/badge/Version-2.0-f0a040?style=flat-square)](CHANGELOG.md)
[![Single File](https://img.shields.io/badge/Single%20File-HTML-a070f0?style=flat-square)](meros_erd_editor.html)

</div>

---

## ✨ ویژگی‌ها

| قابلیت | توضیح |
|--------|-------|
| 📁 **مدیریت چندین پروژه** | هر پروژه یک دیتابیس مستقل با جداول و روابط مجزا |
| 🗄️ **نام‌گذاری دیتابیس** | هر پروژه نام دیتابیس خاص خودش را دارد که در خروجی SQL منعکس می‌شود |
| 📥 **ورودی SQL** | پارس خودکار `CREATE TABLE` — پیست مستقیم یا آپلود فایل `.sql` |
| 📥 **ورودی JSON** | وارد کردن schema از JSON — پیست مستقیم یا آپلود فایل `.json` |
| 📤 **خروجی SQL** | تولید SQL کامل با `CREATE DATABASE`، `CREATE TABLE` و `FOREIGN KEY` |
| 📤 **خروجی JSON** | صدور schema برای انتقال بین پروژه‌ها یا ذخیره |
| 🎨 **طراحی بصری** | کانواس تعاملی با Drag & Drop، زوم و Pan |
| 🔗 **روابط بصری** | خطوط Bezier با برچسب نوع رابطه (1:N، 1:1، N:N) |
| 🗺️ **Minimap** | نمای کوچک کل دیاگرام در گوشه صفحه |
| 💾 **ذخیره خودکار** | تمام تغییرات در `localStorage` مرورگر ذخیره می‌شود |
| 🌙 **Dark Mode** | رابط تاریک حرفه‌ای، کاملاً سازگار با کار شبانه |
| ⌨️ **کلیدهای میانبر** | بهره‌وری بالا با shortcuts کیبورد |

---

## 📖 راهنمای استفاده

### مدیریت پروژه‌ها

```
نوار بالای صفحه → "مدیریت پروژه‌ها"
```

- **ایجاد پروژه جدید:** نام و نام دیتابیس را وارد کنید
- **تغییر پروژه:** از dropdown انتخاب کنید
- **حذف پروژه:** در پنل مدیریت، دکمه 🗑 را بزنید
- هر پروژه جداول، روابط و `nextId` مستقل خودش را دارد

### ورودی SQL

```sql
-- مثال: این SQL را پیست کنید یا به‌عنوان فایل آپلود کنید
CREATE TABLE users (
    id         INTEGER PRIMARY KEY,
    username   VARCHAR(255) NOT NULL UNIQUE,
    email      VARCHAR(255) NOT NULL,
    created_at TIMESTAMP NOT NULL
);

CREATE TABLE posts (
    id         INTEGER PRIMARY KEY,
    user_id    INTEGER NOT NULL REFERENCES users(id),
    title      TEXT NOT NULL,
    body       TEXT,
    created_at TIMESTAMP NOT NULL
);
```

> **نکته:** Parser از `CREATE TABLE` و `CREATE TABLE IF NOT EXISTS` پشتیبانی می‌کند و انواع داده‌ای رایج (INTEGER, TEXT, VARCHAR, TIMESTAMP, ...) را تشخیص می‌دهد.

### خروجی SQL

خروجی شامل موارد زیر است:
```sql
CREATE DATABASE IF NOT EXISTS `my_database`;
USE `my_database`;
PRAGMA foreign_keys = ON;

CREATE TABLE IF NOT EXISTS `users` (
    `id`         INTEGER PRIMARY KEY,
    `username`   VARCHAR(255) NOT NULL UNIQUE,
    FOREIGN KEY (`user_id`) REFERENCES `users`(`id`) ON DELETE CASCADE
);
```

### کلیدهای میانبر

| کلید | عملکرد |
|------|---------|
| `+` / `-` | زوم |
| `F` | Fit View (تنظیم نمایش) |
| `Del` / `Backspace` | حذف جدول یا رابطه انتخابی |
| `Esc` | بستن پنجره |
| چرخ ماوس | زوم |
| Drag روی فضای خالی | Pan (جابجایی دید) |
| Drag روی هدر جدول | جابجایی جدول |
| دابل‌کلیک روی نام جدول | باز کردن ویرایشگر |
| راست‌کلیک روی جدول | منوی سریع |

---

## 🏗️ ساختار فنی

```
meros_erd_editor.html  ← تمام اپلیکیشن در یک فایل
│
├── CSS (Dark theme, RTL-ready)
├── HTML (ساختار UI)
└── JavaScript
    ├── Projects System     ← مدیریت چندپروژه‌ای
    ├── Canvas Engine       ← رندر و تعامل
    ├── SQL Parser          ← پارس CREATE TABLE
    ├── SQL Generator       ← تولید CREATE DATABASE + TABLE + FK
    ├── JSON Import/Export  ← صدور و وارد کردن schema
    └── LocalStorage        ← ذخیره خودکار
```

**ذخیره‌سازی:** تمام داده‌ها در `localStorage` با کلید `meros_erd_projects_v2` ذخیره می‌شوند.

---

## 📸 اسکرین‌شات

> *برای افزودن اسکرین‌شات، یک تصویر از ابزار بگیرید و در پوشه `docs/` قرار دهید.*

---

## 🛠️ توسعه و مشارکت

این پروژه یک فایل HTML تک‌فایل است:

```bash
# برای ویرایش
code meros_erd_editor.html   # VS Code
# یا
vim meros_erd_editor.html
```

Pull Request پذیرفته می‌شود! لطفاً:
1. ریپو را Fork کنید
2. یک branch جدید بسازید: `git checkout -b feature/my-feature`
3. تغییرات را commit کنید
4. PR ارسال کنید

---

## 📝 تاریخچه تغییرات

### v2.0 (2026)
- ✅ سیستم مدیریت چندین پروژه (هر پروژه = یک دیتابیس)
- ✅ ورودی SQL با پارسر (پیست مستقیم + آپلود فایل)
- ✅ ورودی JSON (پیست مستقیم + آپلود فایل با Drag & Drop)
- ✅ خروجی SQL شامل `CREATE DATABASE` و `FOREIGN KEY` کامل
- ✅ آیکون تب مرورگر (favicon)
- ✅ نمایش نام دیتابیس فعال در نوار بالا
- ✅ دیتابیس نمونه ساده‌تر (سیستم لاگین)

### v1.0
- ✅ طراحی بصری ERD
- ✅ خروجی SQL و JSON
- ✅ ذخیره خودکار
- ✅ Minimap
- ✅ روابط بصری

---

## 📄 لایسنس

MIT License — آزاد برای استفاده شخصی و تجاری.

---

<div align="center">
  ساخته‌شده توسط تیم MeRoS
</div>
