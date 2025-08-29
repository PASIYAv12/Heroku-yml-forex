# Heroku-yml-forex

# Exness Bot Controller (Heroku YML Deploy)

> Heroku container-based worker that sends signals to Telegram and optionally forwards to a VPS/MT5 bot for execution.

## 1) Set up
- Copy this repo
- Configure env vars: `TELEGRAM_BOT_TOKEN`, `TELEGRAM_CHAT_ID`, `REMOTE_BOT_API` (optional), `ADMIN_IDS` (optional)

## 2) Heroku (container stack)
```bash
heroku login
heroku create your-exness-controller
heroku stack:set container -a your-exness-controller
heroku config:set TELEGRAM_BOT_TOKEN=XXX TELEGRAM_CHAT_ID=YYY -a your-exness-controller
# Optional:
heroku config:set REMOTE_BOT_API=http://<your-vps>:8000 -a your-exness-controller
heroku addons:create heroku-redis:hobby-dev -a your-exness-controller

# Build & release
heroku container:login
heroku container:push worker -a your-exness-controller
heroku container:release worker -a your-exness-controller

# Logs
heroku logs --tail -a your-exness-controller






---

## 🔐 Required ENV Vars on Heroku
- `TELEGRAM_BOT_TOKEN` – @BotFather token  
- `TELEGRAM_CHAT_ID` – your user/group/channel id  
- `REMOTE_BOT_API` – (optional) VPS endpoint to execute trades  
- `ADMIN_IDS` – (optional) comma-separated Telegram numeric IDs  
- `REDIS_URL` – auto-provided by addon

---

ඉතිං මේ **YML-based Heroku app** එක upload කරලා run කළාම, Telegram updates එනවා, VPS bot එකට signals push වෙනවා (ඔයාගේ VPS MT5 bot endpoint එක සකසා තියෙනවනම් auto-execute වෙනවා).  

තව නිකම්ම **“full code base”** එකක් VPS/MT5 side එකටත් ඔයාට ඕන නම්, මම ඒකත් දෙන්නම්—VPS Flask API + MT5 executor එක එක්ක.
