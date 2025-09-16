هذا البوت يسمح لك بتحميل الفيديوهات من التليجرام واستخراج النصوص منها أو ترجمتها وإضافة الترجمة إلى الفيديو بخط عربي أنيق.
## طريقة التشغيل على VPS (Ubuntu 20.04/22.04)

### المتطلبات
- سيرفر VPS (مثل DigitalOcean أو Contabo) مع 8GB RAM (كافية لفيديوهات قصيرة).
- نظام Ubuntu 20.04 أو 22.04.

🚀 المتطلبات

1. تحديث النظام

sudo apt update && sudo apt upgrade -y

2. تثبيت بايثون و ffmpeg

sudo apt install python3 python3-pip -y
sudo apt install ffmpeg -y

3. إنشاء بيئة افتراضية (اختياري)

python3 -m venv venv
source venv/bin/activate

4. تثبيت المكتبات

pip install --upgrade pip
pip install pyTelegramBotAPI openai-whisper moviepy deep-translator pillow numpy torch

5. تثبيت الخطوط

sudo apt install fonts-noto fonts-dejavu -y

أو ضع الخطوط يدويًا في نفس مجلد المشروع:

NotoNaskhArabic-Regular.ttf

DejaVuSans.ttf



---

⚙️ الإعداد

افتح ملف videoai.py وعدل السطر التالي:

TOKEN = "your_tokenbot"

استبدل your_tokenbot بالتوكن من BotFather.


---

▶️ التشغيل

لتشغيل البوت:

python3 videoai.py


---

🛠️ تشغيل دائم

باستخدام screen:

sudo apt install screen -y
screen -S bot
python3 videoai.py

للخروج بدون إيقاف البوت:

اضغط Ctrl + A بعدها D


للعودة للبوت:

screen -r bot

باستخدام systemd (اختياري):

أنشئ ملف خدمة:

sudo nano /etc/systemd/system/videoai.service

ضع فيه:

[Unit]
Description=VideoAI Telegram Bot
After=network.target

[Service]
ExecStart=/usr/bin/python3 /path/to/videoai.py
WorkingDirectory=/path/to/
Restart=always
User=root

[Install]
WantedBy=multi-user.target

ثم:

sudo systemctl daemon-reload
sudo systemctl enable videoai
sudo systemctl start videoai


---

✅ جاهز!

الآن البوت يعمل ويستقبل الفيديوهات ويعالجها مباشرة.
