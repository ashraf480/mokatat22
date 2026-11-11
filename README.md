# المخطط – تطبيق أندرويد

الصفحة موجودة في `www/index.html` ويتم تحويلها لتطبيق APK موقّع عن طريق GitHub Actions (Capacitor).

## الإعداد (مرة واحدة)

1. ارفع محتوى هذا المجلد كله على مستودع GitHub (الفرع `main`). الخطوة الأولى هتفشل لأن مفتاح التوقيع لسه مش موجود – ده طبيعي.
2. من تبويب **Actions** شغّل workflow اسمه **Generate keystore (run once)** (Run workflow).
3. افتح التشغيل الناجح، ونزّل الـ Artifact اسمه `keystore-secrets-DELETE-AFTER-USE`، وفك الضغط.
4. من **Settings → Secrets and variables → Actions → New repository secret** أضف 4 secrets:
   - `KEYSTORE_BASE64` = كل محتوى ملف `keystore.b64`
   - `KEYSTORE_PASSWORD` = القيمة من `secrets.txt`
   - `KEY_PASSWORD` = القيمة من `secrets.txt`
   - `KEY_ALIAS` = `mukhatat`
5. احفظ ملف `release.keystore` في مكان آمن (نسخة احتياطية) ثم احذف الـ Artifact من GitHub.
   **لو ضاع المفتاح مش هتقدر تحدّث التطبيق على نفس التثبيت.**

## البناء

- أي push على `main` أو تشغيل يدوي لـ **Build signed release APK** يبني APK موقّع ويظهر في **Releases**.
- رقم النسخة بيزيد تلقائيًا: `versionName = 1.0.<رقم التشغيل>` و `versionCode = <رقم التشغيل>`، فالنسخة الأحدث تتثبت فوق القديمة.
