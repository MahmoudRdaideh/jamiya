# 🏛️ نظام إدارة الجمعية — جمعتنا

<div align="center">

![Version](https://img.shields.io/badge/version-1.0.0-blue?style=flat-square)
![Firebase](https://img.shields.io/badge/Firebase-Firestore-orange?style=flat-square&logo=firebase)
![Status](https://img.shields.io/badge/status-production-green?style=flat-square)
![License](https://img.shields.io/badge/license-Private-red?style=flat-square)

**نظام متكامل لإدارة الأقساط والمعاملات المالية للجمعيات والمؤسسات الصغيرة**

[🌐 الرابط المباشر](https://mahmoudrdaideh.github.io/jamiya/) • [📋 دليل الاستخدام](#-دليل-الاستخدام) • [🔧 الإعداد](#-الإعداد)

</div>

---

## 📸 لقطات الشاشة

| لوحة التحكم | المعاملات | تفاصيل الأسهم |
|:-----------:|:---------:|:-------------:|
| إحصائيات شاملة | كشف حساب تفصيلي | توزيع الأرباح السنوي |

---

## ✨ المميزات الرئيسية

### 💼 إدارة المعاملات
- ✅ إضافة وتعديل وحذف المعاملات المالية
- ✅ كشف حساب تفصيلي لكل عميل مع جدول الأقساط
- ✅ تتبع المدفوعات والمتبقي بشكل آني
- ✅ تصدير التقارير بصيغة Excel

### 👥 إدارة المساهمين
- ✅ تفاصيل أسهم كل مساهم عبر السنوات
- ✅ حساب الأرباح والتوزيعات السنوية
- ✅ رسوم بيانية تفاعلية للأداء المالي

### 🔐 نظام الصلاحيات
- ✅ تسجيل دخول آمن عبر Firebase Authentication
- ✅ ثلاثة مستويات صلاحيات: أدمن / محرر / مشاهد
- ✅ سجل أحداث كامل لجميع العمليات

### 🧾 سندات الدفع
- ✅ توليد سند دفع احترافي عند كل عملية
- ✅ ترقيم تلقائي متسلسل لسندات القبض
- ✅ حفظ السندات في قاعدة البيانات

### 📁 وثائق العملاء
- ✅ رفع صور الهوية والعقود والإيصالات
- ✅ تخزين آمن على Cloudinary
- ✅ عرض الوثائق داخل التطبيق

### ⚙️ إعدادات النظام
- ✅ تخصيص هوية النظام (الاسم والشعار)
- ✅ وضع الصيانة
- ✅ الإعدادات الإقليمية (عربي/إنجليزي)
- ✅ دعم Offline (يعمل بدون إنترنت مؤقتاً)

---

## 🛠️ التقنيات المستخدمة

| التقنية | الاستخدام |
|---------|-----------|
| **Firebase Firestore** | قاعدة البيانات السحابية |
| **Firebase Authentication** | نظام تسجيل الدخول |
| **Cloudinary** | تخزين الصور والوثائق |
| **GitHub Pages** | استضافة التطبيق |
| **Vanilla JS** | منطق التطبيق |
| **Chart.js** | الرسوم البيانية |
| **SheetJS (XLSX)** | تصدير Excel |

---

## 🚀 الإعداد

### المتطلبات
- حساب Firebase (مجاني)
- حساب Cloudinary (مجاني)
- حساب GitHub

### خطوات الإعداد

**١. إعداد Firebase**
```bash
# أنشئ مشروعاً جديداً على
https://console.firebase.google.com

# فعّل الخدمات التالية:
- Firestore Database
- Authentication (Email/Password)
```

**٢. إعداد Firestore Rules**
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
    match /{document=**} {
      allow read, write: if request.auth != null;
    }
  }
}
```

**٣. إنشاء أول مستخدم أدمن**
```
Authentication → Add user → أدخل البريد وكلمة المرور
Firestore → users → Add document:
  Document ID: [UID من Authentication]
  email: "your@email.com"
  role: "admin"
```

**٤. تعطيل App Check**
```
Firebase Console → App Check → Cloud Firestore → Unenforce
```

---

## 📖 دليل الاستخدام

### لوحة التحكم
تعرض إحصائيات شاملة: إجمالي المعاملات، المدفوع، المتبقي، نسبة الإنجاز، ورسوم بيانية للأداء المالي.

### إدارة المعاملات
- **إضافة معاملة**: اضغط "معاملة جديدة" وأدخل بيانات العميل والأقساط
- **تسجيل دفعة**: افتح المعاملة واضغط "تسجيل دفعة" — يُولَّد سند الدفع تلقائياً
- **كشف الحساب**: يظهر جدول الأقساط كاملاً داخل تفاصيل المعاملة

### تقرير المدفوعات
فلترة متقدمة بالتاريخ والحالة واسم المشتري مع إمكانية التصدير لـ Excel.

---

## 🔒 الأمان

- جميع البيانات محمية بـ Firestore Security Rules
- تسجيل دخول إلزامي للوصول لأي بيانات
- سجل أحداث لا يمكن تعديله أو حذفه
- سندات القبض محمية من التعديل

---

## 📊 هيكل قاعدة البيانات

```
Firestore/
├── transactions/     ← المعاملات والأقساط
├── yearly/           ← البيانات السنوية
├── sh_details/       ← تفاصيل الأسهم
├── users/            ← المستخدمون والصلاحيات
├── event_logs/       ← سجل الأحداث
├── receipts/         ← سندات القبض
└── app_settings/     ← إعدادات النظام
```

---

## 📞 الدعم الفني

للتواصل بخصوص الدعم الفني أو الاستفسارات:

- **البريد الإلكتروني**: mahmod_rd@yahoo.com
- **GitHub**: [@MahmoudRdaideh](https://github.com/MahmoudRdaideh)

---

## 📄 الترخيص

هذا النظام مرخص للاستخدام الخاص. جميع الحقوق محفوظة © 2026 محمود الردايدة.

---

<div align="center">
صُنع بـ ❤️ لإدارة الجمعيات والمؤسسات المالية الصغيرة
</div>
