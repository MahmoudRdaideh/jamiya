# 🏛️ نظام إدارة الجمعية — جمعتنا

<div align="center">

![Version](https://img.shields.io/badge/version-2.0.0-blue?style=flat-square)
![Firebase](https://img.shields.io/badge/Firebase-Firestore-orange?style=flat-square&logo=firebase)
![Status](https://img.shields.io/badge/status-production-green?style=flat-square)
![License](https://img.shields.io/badge/license-Private-red?style=flat-square)

**نظام متكامل لإدارة الأقساط والمعاملات المالية للجمعيات والمؤسسات الصغيرة**

[🌐 الرابط المباشر](https://mahmoudrdaideh.github.io/jamiya/) • [📋 دليل الاستخدام](#-دليل-الاستخدام) • [🔧 الإعداد](#-الإعداد)

</div>

---

## ✨ المميزات الرئيسية

### 💼 إدارة المعاملات
- ✅ إضافة وتعديل المعاملات مع رفع الوثائق أثناء الإنشاء
- ✅ كشف حساب تفصيلي بجدول الأقساط مع تاريخ الدفع الفعلي لكل قسط
- ✅ تتبع المدفوعات والمتبقي بشكل آني
- ✅ منع تسجيل دفعة على معاملة مكتملة السداد
- ✅ حالة العميل: 🔒 مغلق / 🔓 نشط / 🔴 دين معدوم
- ✅ تصدير التقارير بصيغة Excel

### 👥 إدارة العملاء
- ✅ صفحة مستقلة لقائمة العملاء مع بحث وفلترة
- ✅ تقرير تفصيلي لكل عميل يعرض جميع معاملاته
- ✅ تعديل اسم العميل مع دمج تلقائي للمعاملات عند التطابق
- ✅ شريط تقدم السداد الكلي لكل عميل

### 🧾 سند القبض
- ✅ توليد سند قبض احترافي عند كل دفعة
- ✅ رقم تسلسلي فريد `RCP-YYYY-XXXXXX`
- ✅ حفظ تاريخ الدفعة الفعلي بدل تاريخ الاستحقاق
- ✅ اسم المسؤول بدل الإيميل في السند
- ✅ زر 🧾 سند الدفع في كل معاملة ولوحة التحكم

### 📊 لوحة التحكم
- ✅ بطاقات إحصائية شاملة تتحدث آنياً
- ✅ بطاقة **موجود الصندوق** مع تفصيل لكل سنة عند الضغط
- ✅ قسم "💳 آخر الدفعات" — آخر 5 دفعات مع زر السند
- ✅ أحدث التقارير السنوية

### 📈 الإدارة السنوية
- ✅ بطاقة لكل سنة مالية مع جميع المؤشرات
- ✅ إغلاق السنة المالية رسمياً مع توزيع الأرباح التلقائي
- ✅ الأرباح الموزعة تظهر فقط بعد الإغلاق الرسمي
- ✅ حساب موجود الصندوق = رأس المال + الأرباح - إجمالي المتبقي
- ✅ مؤشر ⓘ يعرض تفصيل المتبقي لكل سنة

### 🔴 الديون المعدومة (Direct Write-off Method)
- ✅ شطب الديون المعدومة مع قيد محاسبي كامل
- ✅ خصم تلقائي من أرباح السنة الحالية
- ✅ حفظ في `bad_debt_entries` لا يُحذف
- ✅ فلتر "🔴 ديون معدومة" في جدول المعاملات
- ✅ بطاقة إجمالي الديون المعدومة في لوحة التحكم

### 📁 وثائق العملاء
- ✅ رفع صور الهوية والعقود والإيصالات عبر Cloudinary
- ✅ رفع الوثائق أثناء إنشاء معاملة جديدة
- ✅ عرض الوثائق في lightbox داخل الصفحة

### 📋 التقارير
- ✅ تقرير المعاملات مع تاريخ آخر دفعة
- ✅ سجل الدفعات المنفصل مع جميع التفاصيل
- ✅ تصدير Excel لكلا التقريرين

### 🔐 نظام الصلاحيات والأمان
- ✅ تسجيل دخول آمن عبر Firebase Authentication
- ✅ ثلاثة مستويات: أدمن / محرر / مشاهد
- ✅ سجل أحداث كامل لا يُحذف ولا يُعدَّل
- ✅ وضع الصيانة يمنع المستخدمين العاديين
- ✅ اسم المستخدم الكامل بدل الإيميل

### ⚙️ إعدادات النظام
- ✅ تخصيص هوية النظام (الاسم والشعار)
- ✅ الإعدادات الإقليمية (عربي/إنجليزي RTL/LTR)
- ✅ سجل الأحداث ضمن قائمة الإعدادات المنسدلة
- ✅ إدارة المستخدمين ضمن نفس القائمة

---

## 🛠️ التقنيات المستخدمة

| التقنية | الاستخدام |
|---------|-----------|
| **Firebase Firestore** | قاعدة البيانات السحابية |
| **Firebase Authentication** | نظام تسجيل الدخول |
| **Cloudinary** | تخزين الصور والوثائق |
| **GitHub Pages** | استضافة التطبيق |
| **Vanilla JS** | منطق التطبيق (بدون frameworks) |
| **SheetJS (XLSX)** | تصدير Excel |

---

## 📊 هيكل قاعدة البيانات

```
Firestore/
├── transactions/       ← المعاملات + payment_dates + last_payment_date
├── yearly/             ← البيانات السنوية + closed + members + fund_balance
├── sh_details/         ← تفاصيل الأسهم
├── users/              ← المستخدمون + displayName + role
├── event_logs/         ← سجل الأحداث (لا يُحذف)
├── receipts/           ← سندات القبض RCP-YYYY-XXXXXX
├── bad_debt_entries/   ← قيود الديون المعدومة (لا تُحذف)
├── year_close_entries/ ← قيود إغلاق السنوات (لا تُحذف)
└── app_settings/       ← branding + maintenance + receipt_counter
```

---

## 🚀 الإعداد

**١. أنشئ مشروع Firebase جديداً**
- فعّل Firestore Database
- فعّل Authentication (Email/Password)
- عطّل App Check أو أضف دومين GitHub

**٢. أنشئ أول مستخدم أدمن**
```
Authentication → Add user
Firestore → users → Document ID: [UID]
  email: "your@email.com"
  role:  "admin"
  displayName: "اسمك الكامل"
```

**٣. Firestore Rules**
```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read: if request.auth != null && request.auth.uid == userId;
      allow write: if request.auth != null;
    }
    match /event_logs/{logId} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update, delete: if false;
    }
    match /receipts/{id} {
      allow read: if request.auth != null;
      allow create: if request.auth != null;
      allow update, delete: if false;
    }
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

---

## 🔗 الروابط

- **النظام المباشر:** https://mahmoudrdaideh.github.io/jamiya/
- **GitHub:** https://github.com/MahmoudRdaideh/jamiya
- **Firebase Console:** https://console.firebase.google.com

---

## 📞 الدعم الفني

- **البريد:** mahmod_rd@yahoo.com
- **GitHub:** [@MahmoudRdaideh](https://github.com/MahmoudRdaideh)

---

<div align="center">
صُنع بـ ❤️ لإدارة الجمعيات والمؤسسات المالية الصغيرة | v2.0.0 — أبريل 2026
</div>
