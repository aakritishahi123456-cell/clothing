# Clothing Revolution — Fashion Preview Assistant

A multi-channel assistant for online clothing sellers (WhatsApp + Instagram). Helps create *visual previews* of how garments might look—not exact fitting. Built with consent, privacy, and one-step-at-a-time guidance.

## Features

- **WhatsApp** (Twilio) and **Instagram** (Meta Messaging) support
- Step-by-step guided flow
- Consent collection before processing
- Photo validation (format, size)
- AI-generated fashion previews (OpenAI DALL·E 3 + GPT-4o-mini vision)
- Privacy-first messaging (images auto-deleted)
- Clear expectations: preview only, not exact fit

## Requirements

- Node.js 18+
- [Twilio](https://www.twilio.com) account (WhatsApp Sandbox or Business)
- [Meta for Developers](https://developers.facebook.com) app (Instagram Messaging)
- [OpenAI](https://platform.openai.com) API key

## Setup

1. **Install dependencies**

   ```bash
   npm install
   ```

2. **Environment variables**

   Copy `.env.example` to `.env` and fill in:

   ```
   PORT=3000
   BASE_URL=https://your-ngrok-or-domain.com

   TWILIO_ACCOUNT_SID=your_twilio_sid
   TWILIO_AUTH_TOKEN=your_twilio_token
   TWILIO_WHATSAPP_NUMBER=whatsapp:+14155238886

   META_PAGE_ACCESS_TOKEN=your_meta_page_token
   META_VERIFY_TOKEN=clothing-revolution

   OPENAI_API_KEY=your_openai_key
   ```

3. **Twilio WhatsApp**

   - Go to [Twilio Console → Messaging → Try it out → Send a WhatsApp message](https://console.twilio.com/us1/develop/sms/try-it-out/whatsapp-learn)
   - Use the Sandbox or connect your own WhatsApp Business number
   - Set the webhook URL: `https://YOUR_DOMAIN/webhook/whatsapp`

4. **Expose locally (for development)**

   ```bash
   npx ngrok http 3000
   ```

   Use the ngrok URL as `BASE_URL` and as the webhook in Twilio.

## Run

```bash
npm start
```

Or with auto-reload:

```bash
npm run dev
```

## User Flow

1. User sends any message → Welcome + consent request
2. User replies "yes" → Asked for garment photo
3. User sends garment photo → Validated, then asked for body/model photo
4. User sends body photo or "skip" → Preview generated and sent
5. Result labeled as preview, with privacy reminder

## Project Structure

```
src/
  index.js      — Express server, webhook routes
  whatsapp.js   — Twilio WhatsApp handling
  instagram.js  — Meta Instagram Messaging handling
  flow.js       — Conversation state & copy
  validation.js — Photo validation
  imageGen.js   — OpenAI vision + DALL·E 3
```

## Notes

- Images are not persisted; treat as auto-deleted after processing
- Preview is visual only—never promise exact fit or realism
- Use "start", "hi", or "hello" to restart the flow
