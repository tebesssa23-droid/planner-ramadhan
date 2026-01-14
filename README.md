# Ramadan Planner (Book Web App)

Web App (Next.js) على شكل "كراس" (Page Flip) + مواعيد الصلاة حسب GPS + تسجيل دخول بـ Magic Link (Firebase) + Invitation-only مع Demo Mode.

## 1) الأدوات اللي تحتاجهم
- Node.js (LTS) + npm
- VS Code
- Git (اختياري)
- حساب Firebase + حساب Vercel

## 2) تشغيل محلي (Local)
1) فكّ الضغط وافتح الفولدر في VS Code
2) انسخ `.env.example` لملف `.env.local`
3) عمّر متغيرات Firebase (من Firebase Console ➜ Project settings ➜ Web app)
4) ثبّت الحزم:
```bash
npm install
```
5) شغّل:
```bash
npm run dev
```
ثم افتح: http://localhost:3000

## 3) إعداد Firebase (مهم)
### Auth (Magic Link)
- Firebase Console ➜ Authentication ➜ Sign-in method
- فعّل `Email/Password` ثم فعّل خيار **Email link (passwordless sign-in)**

### Authorized domains
- Authentication ➜ Settings ➜ Authorized domains
- زِد:
  - `localhost`
  - دومين Vercel تاعك بعد ما تنشر (مثال: your-app.vercel.app)

### Firestore
- Firebase Console ➜ Firestore Database ➜ Create database
- خدم Collection:
  - `invites` (document id = email lowercased)
  - `users/{uid}/entries/{YYYY-MM-DD}`

### Firestore Rules
- استعمل الملف `firestore.rules` (عدّل admin email إذا تحب)

## 4) Deploy على Vercel
1) Push المشروع لـ GitHub أو استعمل Import من Vercel
2) Vercel ➜ Project ➜ Settings ➜ Environment Variables
   - زِد كامل `NEXT_PUBLIC_FIREBASE_*`
   - زِد `NEXT_PUBLIC_APP_URL` = رابط Vercel النهائي (مهم لـ Magic Link)
3) اعمل Deploy

## 5) الاستعمال
- `/` تسجيل دخول (Invite-only)
- `/demo` وضع Demo (يتحفظ محلياً)
- `/admin` (للـ admin فقط) باش يزيد Invites

> إذا بانلك `auth/invalid-api-key`: راجع `NEXT_PUBLIC_FIREBASE_API_KEY` و تأكد ماكانش فراغات/قوسين، وراه من نفس Firebase Web App.

