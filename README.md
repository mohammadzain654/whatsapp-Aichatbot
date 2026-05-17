
# AlphaBlue WhatsApp AI Chatbot 🤖💧

An AI-powered WhatsApp chatbot built with **n8n** for **AlphaBlue**, a mineral water delivery business in Karachi, Pakistan. The chatbot handles customer orders and complaints automatically — 24/7, with no human involvement.

---
<img width="1469" height="831" alt="Screenshot 2026-05-17 at 6 48 10 PM" src="https://github.com/user-attachments/assets/809dc096-5115-4c17-9c99-81e605178e42" />

## 🚀 Features

- **Automated Order Taking** — Guides customers through a full 12-step order flow via WhatsApp
- **Complaint Handling** — Detects and logs customer complaints instantly
- **Voice Note Support** — Transcribes voice notes to text using OpenAI Whisper
- **Area-Based Pricing** — Looks up real-time pricing from Google Sheets based on customer location
- **Auto Logging** — Saves all orders and complaints to Google Sheets automatically
- **Multi-Language** — Supports English, Urdu (script) and Roman Urdu
- **Payment Handling** — Shares COD, EasyPaisa, and Bank Transfer details on request
- **Conversation Memory** — Remembers the last 15 messages per customer session

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **n8n** | Workflow automation & chatbot logic |
| **OpenAI GPT-4** | AI conversation agent (Alpha1) |
| **OpenAI Whisper** | Voice note transcription |
| **WhatsApp Business API** | Customer messaging channel |
| **Google Sheets** | Orders, complaints & pricing database |

---

## ⚙️ How It Works

```
Customer sends WhatsApp message
        ↓
n8n receives via webhook (WhatsApp Trigger)
        ↓
Filter — checks if message exists
        ↓
IF Node — is it text or voice note?
   ↙ Text              ↘ Voice Note
   |              Whisper transcribes audio
   |                       ↓
   ↘         ← Clean text output
        ↓
   AI Agent (Alpha1)
   - Reads pricing from Google Sheets
   - Collects order/complaint details
        ↓
   Logs to Google Sheets
        ↓
   Sends reply to customer on WhatsApp
```

---

## 📋 Order Flow

Alpha1 collects the following before confirming an order:

1. Customer greeting & introduction
2. Weekly bottle usage (quantity)
3. Full name
4. Area (for price lookup)
5. Full street address
6. Contact number
7. Order quantity confirmation
8. Google Maps location (optional)
9. Price shown from Sheets
10. Payment method selection
11. Full order summary shown to customer
12. Customer confirms → logged to Google Sheets

---

## 📣 Complaint Flow

1. Customer reports an issue
2. Alpha1 collects name, number & description
3. Complaint logged to Google Sheets with status = "Open"
4. Customer receives confirmation within seconds

---

## 🗂️ Google Sheets Structure

The chatbot uses **3 sheets** in one Google Spreadsheet:

| Sheet | Purpose |
|---|---|
| `price_list` | Area-based pricing (read only) |
| `orders` | All confirmed customer orders |
| `complaints` | All logged complaints |

---

## 🔧 Setup Instructions

### Prerequisites
- n8n instance (cloud or self-hosted)
- OpenAI API key
- WhatsApp Business API access (Meta Developer Account)
- Google Sheets with the 3 tabs above

### Steps

1. **Clone this repo**
```bash
git clone https://github.com/YOUR_USERNAME/alphablue-whatsapp-chatbot.git
```

2. **Import workflow into n8n**
   - Open n8n → Click **"Import from file"**
   - Select `workflow.json`

3. **Set up credentials in n8n**
   - OpenAI API key
   - WhatsApp Business API token
   - Google Sheets OAuth2

4. **Update the workflow**
   - Replace Google Sheets document ID with your own
   - Update payment details in the system prompt
   - Update area names in your price_list sheet

5. **Activate the workflow**
   - Toggle the workflow to **Active**
   - Set your WhatsApp webhook URL to your n8n webhook

---

## 📁 Project Structure

```
alphablue-whatsapp-chatbot/
│
├── workflow.json          # n8n workflow (import this)
└── README.md              # Project documentation
```

---

## ⚠️ Important Notes

- Voice note transcription requires an active OpenAI API key with Whisper access
- WhatsApp Business API requires Meta app approval
- Pricing is fetched live from Google Sheets — never hardcoded
- Payment details are only shared after the customer selects a payment method

---

## 👤 Author

**Mohammad Zain Khan**
- Built for: AlphaBlue, Karachi, Pakistan
- Tools: n8n · OpenAI · WhatsApp Business API · Google Sheets

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

> *"Delivering water. Powered by AI."* 💧
