# Telegram Code Analyzer Bot

.py, .js, .zip (aur baaki code files) bhejo, bot batayega ki code/bot kya karta hai
aur security ke hisaab se safe hai ya nahi. Bheja gaya code kabhi RUN nahi hota.

## Setup
1. Python 3.10+ install ho.
2. Dependencies:
       pip install -r requirements.txt
3. @BotFather se bot banao aur token lo. console.anthropic.com se API key lo.
4. `.env.example` ko `.env` naam se copy karo aur keys bharo.
5. Run:
       python bot.py

(Optional venv: `python -m venv venv` phir `source venv/bin/activate`, Windows: `venv\Scripts\activate`)

## Docker se
    docker build -t code-analyzer-bot .
    docker run -d --restart unless-stopped --env-file .env code-analyzer-bot

## Deploy (24/7)
Railway / Render / VPS par deploy karo. Keys ko hamesha "Environment Variables" me daalo,
code ya GitHub me nahi.

### Render Web Service
- Build command: `pip install -r requirements.txt`
- Start command: `python bot.py`
- Health check path: `/health`
- `TELEGRAM_BOT_TOKEN`, `ANTHROPIC_API_KEY`, aur `ALLOWED_USER_IDS` ko Render ke Environment settings me set karo.

### UptimeRobot
Ek HTTP(s) monitor banao jo Render ke URL ke end me `/health` lagakar check kare, jaise `https://<service>.onrender.com/health`.

## Settings (.env)
- TELEGRAM_BOT_TOKEN : zaroori
- ANTHROPIC_API_KEY  : zaroori
- CLAUDE_MODEL       : optional
- ALLOWED_USER_IDS   : optional, sirf in Telegram IDs ko access (apni ID @userinfobot se pata karo)

## Limits
File 20MB tak, har file ke 12k characters, total 90k characters. Zip me max 400 files.
Zip memory me hi padha jata hai, disk pe extract nahi hota.

## Security
- Analysis ke liye bheja gaya code Anthropic API ko bheja jata hai; confidential code ya secrets upload na karein.
- `ALLOWED_USER_IDS` set karein. Khali chhodne par bot har Telegram user ko allow karta hai, jisse API usage/cost ho sakti hai.
- Keys kabhi chat/GitHub par share mat karo. Leak ho jaye to turant revoke karo.
- Telegram token: @BotFather -> /revoke
