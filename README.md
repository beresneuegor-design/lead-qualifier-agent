# 🎯 Lead Qualifier Agent — n8n

> New lead hits your webhook → Groq AI scores and qualifies → hot leads get instant personalized email + manager alert on Telegram.

![n8n](https://img.shields.io/badge/n8n-workflow-FF6B6B?style=flat-square)
![Groq](https://img.shields.io/badge/Groq-LLaMA%203.3%2070B-F55036?style=flat-square)
![Gmail](https://img.shields.io/badge/Gmail-API-EA4335?style=flat-square&logo=gmail&logoColor=white)
![Telegram](https://img.shields.io/badge/Telegram-Bot%20API-26A5E4?style=flat-square&logo=telegram)
![License](https://img.shields.io/badge/license-MIT-green?style=flat-square)

## ✨ What it does

1. **Receives** lead from website form via webhook
2. **Scores** lead with Groq AI (budget, need, urgency, fit)
3. **Routes**: hot leads → immediate action, cold leads → nurture sequence
4. **Sends** personalized email to hot leads automatically
5. **Alerts** sales manager on Telegram with lead score + summary

## 🏗️ Architecture

```
Website Form
      │
      ▼
┌─────────────┐
│   Webhook    │  receives: name, email, company, message
└──────┬──────┘
       │
       ▼
┌─────────────┐
│   Groq AI    │  scores lead 1-10
│              │  extracts: budget, urgency, fit, intent
└──────┬──────┘
       │
       ▼
┌─────────────┐
│  IF Node     │  score >= 7 → HOT / score < 7 → COLD
└──────┬──────┘
       │
  ┌────┴────┐
  ▼         ▼
HOT        COLD
  │           │
  ▼           ▼
Gmail      Log to
+ Telegram  Sheets
```

## 💡 Example Scoring Prompt Output

```json
{
  "score": 8,
  "budget": "confirmed",
  "urgency": "high",
  "fit": "perfect",
  "summary": "E-commerce owner, 50k PLN budget, needs automation ASAP"
}
```

## 🚀 Setup

1. Import `workflow.json` into n8n
2. Set webhook URL in your contact form
3. Add credentials: Groq API, Gmail OAuth2, Telegram Bot
4. Configure scoring threshold in IF node (default: 7)
5. Activate workflow

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation | n8n |
| AI Scoring | Groq — LLaMA 3.3 70B |
| Email | Gmail API |
| Alerts | Telegram Bot API |
| Storage | Google Sheets |

---
*Built by [VinteliVision](https://vintelivision.com) — AI automation for Polish SMBs.*
