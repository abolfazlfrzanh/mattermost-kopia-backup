# kopia-mattermost-postgres-example
This guide explains how to create snapshots and restore Metermost data using Kopia.
Mattermost Backup with Kopia
این پروژه شامل دو سرویس Docker است:

Mattermost + PostgreSQL
Kopia Server برای گرفتن Snapshot و انجام Restore
راه‌اندازی Mattermost
وارد پوشه mattermost شوید و سرویس را اجرا کنید:

text
cd mattermost
docker compose up -d
این سرویس شامل دو کانتینر است:

postgres
mattermost
دیتابیس داخل این volume ذخیره می‌شود:

text
postgres-data:/var/lib/postgresql/data
راه‌اندازی Kopia
وارد پوشه kopia شوید:

text
cd kopia
docker compose up -d
برای دسترسی به رابط کاربری Kopia:

text
http://localhost:51515
اطلاعات ورود:

text
username: admin@local
password: admin
ارتباط Volume ها
Kopia برای بکاپ گرفتن، volume دیتابیس Mattermost را به صورت read-only mount می‌کند:

text
postgres-data → /data/postgres
بنابراین Kopia می‌تواند از دیتابیس snapshot بگیرد بدون اینکه تغییری در داده‌ها ایجاد کند.

گرفتن Snapshot
در رابط کاربری Kopia:

وارد بخش Snapshots شوید
گزینه New Snapshot را انتخاب کنید
مسیر زیر را وارد کنید:
text
/data/postgres
Restore کردن Snapshot
برای بازگردانی بکاپ:

وارد Snapshots شوید
یک Snapshot را انتخاب کنید
گزینه Restore را بزنید
مسیر مقصد را وارد کنید:
text
/restore
فایل‌های restore شده داخل این مسیر در سیستم میزبان ذخیره می‌شوند:

text
./restore-destination
ایمیج Kopia (فایل tar)
ایمیج Kopia در این پروژه به صورت فایل tar ذخیره شده است:

text
images/kopia-image.tar
برای load کردن ایمیج:

text
docker load -i images/kopia-image.tar
در صورت نیاز می‌توان ایمیج را با دستور زیر ساخت:

text
docker save hub.hamdocker.ir/kopia/kopia > images/kopia-image.tar
:::
