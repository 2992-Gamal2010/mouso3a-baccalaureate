موسوعة البكالوريا التفاعلية — Online V2

هذه النسخة تستخدم Vite + Supabase Auth + PostgreSQL.

تشغيل محلي:
1) npm install
2) أنشئ .env.local من .env.example
3) npm run dev

Vercel:
- VITE_SUPABASE_URL
- VITE_SUPABASE_ANON_KEY

مهم: لا تضع service_role أو أي secret key في الواجهة.

بعد إنشاء الجداول الأساسية، شغّل supabase/profile.sql ثم أنشئ أول مستخدم من Supabase Auth وأضف له صفًا في profiles بدوره admin.
