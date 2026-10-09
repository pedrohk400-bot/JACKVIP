PED SAN — نسخة Firebase + GitHub Pages
=======================================

الملفات:
- index.html: صفحة عرض الدروس للزوار.
- admin.html: لوحة إدارة لإضافة/تعديل/حذف الدروس.
- firebase-config.js: ضع فيه إعدادات تطبيق Firebase Web.
- database.rules.json: قواعد Realtime Database. لا تنشرها قبل استبدال UID.
- README_AR.txt: خطوات الإعداد.

مهم جداً:
1) هذه نسخة موقع ثابتة تعمل على GitHub Pages، وتستخدم Firebase مباشرة من المتصفح.
2) لا تضع أي كلمة مرور أو service-account key أو مفتاح خاص في ملفات الموقع.
3) apiKey الموجود في firebase-config.js هو إعداد عميل وليس كلمة مرور؛ قواعد Firebase هي التي تحمي البيانات.
4) لا تستخدم قواعد مفتوحة للكتابة مثل .write: true.
5) لا تفعّل إنشاء حسابات عامة من صفحة الموقع؛ أنشئ حساب المشرف يدوياً من Firebase Console.

الإعداد من الموبايل:
A. إنشاء المشروع:
1. افتح https://console.firebase.google.com/
2. أنشئ مشروعاً جديداً باسم PED SAN.
3. من Project settings > General > Your apps، اضغط إضافة تطبيق Web (</>).
4. سجّل التطبيق، وانسخ قيم firebaseConfig إلى firebase-config.js.
   استبدل YOUR_PROJECT_ID وPASTE_API_KEY_HERE وPASTE_REALTIME_DATABASE_URL_HERE
   وPASTE_MESSAGING_SENDER_ID_HERE وPASTE_APP_ID_HERE بالقيم الحقيقية.
5. من Build > Realtime Database أنشئ قاعدة بيانات. اختر موقع قاعدة البيانات، ثم انسخ رابطها الكامل
   إلى databaseURL. لا تخمّن الرابط؛ انسخه من صفحة Realtime Database.

B. حساب المشرف:
1. من Build > Authentication > Get started.
2. من Sign-in method فعّل Email/Password.
3. من Users > Add user أنشئ بريد وكلمة مرور خاصة بالمشرف.
4. افتح المستخدم وانسخ UID الخاص به.

C. قواعد قاعدة البيانات:
1. افتح Realtime Database > Rules.
2. افتح database.rules.json واستبدل REPLACE_WITH_ADMIN_UID بقيمة UID الفعلية.
3. انسخ محتوى الملف بالكامل إلى Rules واضغط Publish.
4. تأكد أن قاعدة الدروس اسمها lessons. القراءة عامة للدروس فقط، والكتابة للمشرف الذي يطابق UID.
5. لا تترك نص REPLACE_WITH_ADMIN_UID كما هو، وإلا لن يتمكن المشرف من الحفظ.

D. رفع الموقع إلى GitHub من الهاتف:
1. أنشئ مستودعاً جديداً باسم ped-san، ويفضل أن يكون Public إذا تريد GitHub Pages مجاناً.
2. ارفع index.html وadmin.html وfirebase-config.js فقط إلى جذر المستودع.
   لا ترفع كلمات المرور أو ملفات مفاتيح خاصة. database.rules.json يمكن رفعه بعد استبدال UID، أو تكتفي بلصقه في Firebase Console.
3. من Settings > Pages اختر Deploy from a branch، ثم Branch: main وFolder: /(root)، واضغط Save.
4. انتظر نشر GitHub Pages وافتح الرابط الذي يظهر لك.
5. افتح /admin.html وسجّل الدخول بحساب المشرف.

اختبار:
- افتح الصفحة الرئيسية. إذا ظهرت رسالة تعذّر الاتصال، تحقق من firebase-config.js ورابط قاعدة البيانات وقواعد .read.
- إذا تسجيل الدخول نجح لكن الحفظ يعطي Permission denied، تأكد من UID في Rules وأنك نشرت القواعد.
- اختبر إضافة درس ثم افتح الموقع الرئيسي.
- إذا عدلت قواعد البيانات، اضغط Publish.

تنبيهات:
- من الأفضل عدم استخدام حساب المشرف نفسه في أجهزة عامة.
- فعّل مصادقة البريد وكلمة مرور قوية، واستخدم استرداد كلمة المرور من Firebase عند الحاجة.
- قواعد هذا المثال تمنع حقول الدروس غير المعروفة وتحدّ أطوال النصوص، لكنها ليست بديلاً عن مراجعة المحتوى.
- GitHub Pages لا يشغّل PHP؛ هذه النسخة HTML/JavaScript وتربط Firebase مباشرة.
