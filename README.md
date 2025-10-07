# suc-nanobrowser

Orian (Ollama WebUI) is a Chrome extension
https://github.com/KarthikeyaKollu/browserAI.01



حسنًا، بما أنك نفذت:

curl -fsSL https://ollama.com/install.sh | sh


وظهرت الرسالة:

>>> Creating ollama systemd service...
>>> Enabling and starting ollama service...


فهذا يعني أن التثبيت اليدوي أنشأ لك خدمة systemd باسم ollama تعمل تلقائيًا عند الإقلاع.




















which ollama
و

bash
Copy code
ls -l /usr/local/bin/ollama
ls -l /usr/bin/ollama













✅ تفعيل الخدمة

بعد حفظ الملف:

sudo systemctl daemon-reload
sudo systemctl enable ollama
sudo systemctl start ollama

🔍 التحقق من الحالة
sudo systemctl status ollama












افتح ملف الخدمة مجددًا:

sudo nano /etc/systemd/system/ollama.service


[Unit]
Description=Ollama Service
After=network-online.target


[Service]
ExecStart=/usr/local/bin/ollama serve
User=ollama
Group=ollama
Restart=always
RestartSec=3
Environment="OLLAMA_HOST=0.0.0.0"
Environment="OLLAMA_ORIGINS=*"
# إذا أردت تحديد PATH مخصص، يمكنك إضافته بالشكل الصحيح، وإلا احذف السطر التالي:
# Environment="PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
Environment="OLLAMA_ORIGINS=chrome-extension://*"

[Install]
WantedBy=multi-user.target





:




احفظ وأغلق (Ctrl+O, Enter, ثم Ctrl+X).

أعد تحميل وضبط الخدمة:

sudo systemctl daemon-reload
sudo systemctl restart ollama


تحقق من حالة الخدمة:

sudo systemctl status ollama


اختبر CORS الآن:

curl -X OPTIONS http://localhost:11434 -H "Origin: chrome-extension://some-id" -I

