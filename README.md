# موسوعة البكالوريا التفاعلية — Online Deployment

## الاختيار التقني
- Frontend: HTML/CSS/JavaScript الحالي.
- Hosting: Vercel.
- Auth: Supabase Auth.
- Database: Supabase Postgres + RLS.
- Files: Supabase Storage.

Vercel يدعم الربط مع GitHub والنشر التلقائي عند كل push، كما يمكن النشر مباشرة عبر CLI. Supabase يوفر Auth وPostgres وStorage وRLS.

## 1) ارفع المشروع إلى GitHub
أنشئ repository جديد، ثم ارفع محتويات هذا المجلد إلى `main`.

## 2) اربطه بـ Vercel
- افتح Vercel.
- New Project.
- اختر repository.
- Framework: Other / Static.
- Build Command: اتركه فارغًا.
- Output Directory: `.`
- Deploy.

## 3) أنشئ مشروع Supabase
أنشئ Project جديدًا، ثم افتح SQL Editor وشغّل:
`supabase/schema.sql`

## 4) Auth
فعّل Email/Password في Authentication > Sign In / Providers.
لا تعرض كلمات المرور في الواجهة ولا تضع service_role key داخل ملفات المتصفح.

## 5) Storage
أنشئ Bucket باسم `lesson-files` للـPDF والصور والملفات التعليمية، ثم ضع Policies تسمح للطلاب بالقراءة وللإدارة بالرفع/التعديل. لا تضع ملفات حساسة في bucket عام.

## 6) المتغيرات
أنشئ متغيرات Vercel حسب الحاجة:
- `SUPABASE_URL`
- `SUPABASE_PUBLISHABLE_KEY`

المفتاح publishable يمكن استخدامه من الواجهة مع RLS صحيحة. لا تستخدم service role في المتصفح.

## 7) إنشاء الطلاب من الإدارة
ملف `supabase/functions/create-student/index.ts` هو الهيكل الآمن لإنشاء حساب طالب من الإدارة. يتم استخدام service role داخل Edge Function فقط، وليس داخل JavaScript الخاص بالمتصفح.

## 8) الدومين
بعد تشغيل الموقع يمكن إضافة دومين مخصص من Vercel. Vercel يوضح إعداد DNS وSSL من لوحة المشروع.

## ملاحظة مهمة
النسخة المرفقة هي حزمة نشر وتجهيز Online مبنية على الواجهة الحالية. تسجيل الدخول الحالي داخل `script.js` ما زال Local-first؛ قبل فتح التسجيل العام يجب استبداله بـSupabase Auth وربط الصفحات والجداول بالـdatabase. لا تستخدم كلمات المرور الموجودة في النسخة المحلية في موقع حقيقي.
