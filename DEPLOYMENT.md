# Deployment Guide

See the comprehensive deployment guide in the artifacts folder for detailed instructions.

## Quick Start

### 1. Deploy to Render.com

```bash
# Push to GitHub
git init
git add .
git commit -m "Deploy High-Precision Fashion Assistant"
git branch -M main
git remote add origin YOUR_REPO_URL
git push -u origin main
```

Then:
1. Go to [render.com](https://render.com)
2. New Web Service → Connect your repo
3. Render auto-detects `render.yaml`
4. Add environment variables (see `.env.example`)
5. Deploy!

### 2. Configure Twilio Webhook

Set your Twilio WhatsApp webhook to:
```
https://YOUR_DEPLOYED_URL/webhook/whatsapp
```

### 3. Test

```bash
curl https://YOUR_DEPLOYED_URL/health
```

Send a WhatsApp message to your Twilio number!

---

**For detailed instructions, troubleshooting, and alternative deployment options, see the full deployment guide in the artifacts.**
