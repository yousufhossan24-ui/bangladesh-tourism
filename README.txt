বাংলাদেশ ট্যুরিজম: উন্নত অ্যাডমিন প্যানেল স্টার্টার
==================================================

ফাইলসমূহ
- index.html: জনসাধারণের ওয়েবসাইট
- admin.html: ইমেইল/পাসওয়ার্ড লগইনসহ অ্যাডমিন প্যানেল
- config.js: Supabase URL ও anon key বসানোর জায়গা
- supabase-schema.sql: ডেটাবেস টেবিল ও Row Level Security নীতিমালা

গুরুত্বপূর্ণ
এটি একটি starter package, এখনো লাইভ ওয়েবসাইট নয়। Supabase project তৈরি, কনফিগার, প্রথম অ্যাডমিন user তৈরি, admin_users-এ user UUID যোগ এবং hosting প্রকাশ করা বাকি। কোনো password বা service_role key এই ফাইলে লিখবেন না। config.js-এ শুধু Project URL ও anon/public key বসাবেন।

সেটআপ ধাপ
1. Supabase-এ একটি project তৈরি করুন।
2. Project Settings > API থেকে Project URL এবং anon/public key কপি করুন।
3. config.js-এ placeholder দুটি বদলে ওই URL ও anon key বসান।
4. Supabase Dashboard > SQL Editor খুলে supabase-schema.sql-এর সম্পূর্ণ SQL রান করুন।
5. Authentication > Users-এ প্রথম অ্যাডমিনের ইমেইল দিয়ে user তৈরি করুন। পাসওয়ার্ডটি নিরাপদ রাখুন।
6. Auth Users তালিকা থেকে সেই user-এর UUID কপি করুন।
7. SQL Editor-এ নিচের query চালান, UUID বসিয়ে:
   insert into public.admin_users (user_id) values ('YOUR-ADMIN-USER-UUID');
8. index.html, admin.html ও config.js একসঙ্গে GitHub-এর public repository-তে upload করুন।
9. Settings > Pages > Deploy from a branch > main > /(root) নির্বাচন করে Save দিন।
10. প্রকাশিত ওয়েবসাইটে /admin.html যোগ করে অ্যাডমিন লগইন খুলুন।

নিরাপত্তা নোট
- service_role key কখনো ব্রাউজার/HTML/JavaScript-এ রাখবেন না।
- anon key ক্লায়েন্টে থাকা স্বাভাবিক, তবে ডেটা সুরক্ষার জন্য SQL-এ থাকা RLS নীতিমালা অবশ্যই প্রয়োগ করুন।
- অ্যাডমিন account-এর শক্তিশালী, আলাদা পাসওয়ার্ড ব্যবহার করুন এবং অন্য কাউকে দেবেন না।
- production-এ যাওয়ার আগে Supabase Auth email confirmation, rate limits, backup ও abuse protection সেটিংস যাচাই করুন।
- ব্যবহারকারীর জমা তথ্য প্রথমে pending থাকবে; অ্যাডমিন অনুমোদন করলে tourism_places-এ প্রকাশ হবে।
- বর্তমান সংস্করণে ছবি URL হিসেবে যোগ করা যায়; ফাইল আপলোড করতে চাইলে Supabase Storage bucket ও আলাদা policies লাগবে।
