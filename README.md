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
