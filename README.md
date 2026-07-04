# Telegram Two Daily Posts Bot

هذا المشروع يعتمد على ملف واحد فقط:

```text
data/posts.txt
```

ويرسل منه منشورين منفصلين يوميًا إلى قناة Telegram الساعة 08:00 صباحًا تقريبًا بتوقيت تركيا/السعودية.

## الملفات المطلوبة

```text
send_post.py
state.json
data/posts.txt
.github/workflows/send_daily.yml
COPY_THIS_TO_GITHUB_ACTIONS.yml
```

## طريقة العمل

- `data/posts.txt` يحتوي على منشوراتك.
- كل منشور مفصول بسطر يحتوي على:
```text
---
```
- كل يوم يرسل السكربت منشورين.
- بعد الإرسال، يتم تحديث `state.json` تلقائيًا حتى لا يبدأ من نفس المنشورات في اليوم التالي.

## إنشاء بوت Telegram

1. افتح Telegram.
2. ابحث عن `@BotFather`.
3. أرسل:
```text
/newbot
```
4. أنشئ البوت وانسخ الـ Token.

## إضافة البوت إلى القناة

1. افتح قناتك في Telegram.
2. أضف البوت كمسؤول Admin.
3. أعطه صلاحية نشر الرسائل.

## إضافة أسرار GitHub

في GitHub:

`Settings` → `Secrets and variables` → `Actions` → `New repository secret`

أضف:

```text
TELEGRAM_BOT_TOKEN
```

وقيمته Token البوت.

ثم أضف:

```text
TELEGRAM_CHAT_ID
```

وقيمته username القناة مثل:

```text
@YourChannelUsername
```

## تشغيل يدوي للتجربة

من GitHub:

`Actions` → `Send two daily Telegram posts` → `Run workflow`

## إذا لم تستطع إضافة مجلد .github

من GitHub نفسه:

1. اضغط `Add file`
2. اختر `Create new file`
3. في اسم الملف اكتب:

```text
.github/workflows/send_daily.yml
```

4. الصق محتوى ملف:

```text
COPY_THIS_TO_GITHUB_ACTIONS.yml
```

5. اضغط `Commit changes`

## تغيير عدد المنشورات اليومية

في الملف:

```text
.github/workflows/send_daily.yml
```

غيّر:

```yaml
POSTS_PER_RUN: "2"
```

مثلاً إلى:

```yaml
POSTS_PER_RUN: "1"
```

أو:

```yaml
POSTS_PER_RUN: "3"
```

## تغيير وقت النشر

حاليًا مضبوط على:

```yaml
- cron: "0 5 * * *"
```

وهذا يعني 08:00 صباحًا بتوقيت تركيا/السعودية تقريبًا، لأن GitHub يستخدم UTC.
