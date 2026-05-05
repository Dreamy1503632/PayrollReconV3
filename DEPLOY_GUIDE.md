# Step-by-Step Deployment Guide

## Prerequisites
- A GitHub account
- A Vercel account (free tier is fine) → vercel.com
- An Anthropic API key → console.anthropic.com

---

## STEP 1 — Push to GitHub

### Option A: Using GitHub Desktop (easiest, no command line)
1. Download GitHub Desktop → desktop.github.com
2. Open GitHub Desktop → File → Add Local Repository
3. Select the `payroll-recon` folder
4. Click "Publish repository" (top right)
5. Name it `payroll-recon`, choose Private or Public → Publish

### Option B: Using Git command line
```bash
cd payroll-recon

git init
git add .
git commit -m "Initial commit: Payroll Reconciliation App"

# Create a new repo on github.com first, then:
git remote add origin https://github.com/YOUR_USERNAME/payroll-recon.git
git branch -M main
git push -u origin main
```

---

## STEP 2 — Deploy on Vercel

1. Go to **vercel.com** → Sign in (use GitHub login)
2. Click **"Add New Project"**
3. Click **"Import Git Repository"** → Select `payroll-recon`
4. Vercel auto-detects Vite. Framework Preset should show **"Vite"**
5. Leave Build Command as `vite build` and Output Directory as `dist`
6. **IMPORTANT — Add Environment Variable:**
   - Scroll down to **"Environment Variables"**
   - Name: `ANTHROPIC_API_KEY`
   - Value: `sk-ant-xxxxxxxxxxxx` (your Anthropic key)
   - Click **Add**
7. Click **"Deploy"**
8. Wait ~60 seconds → Your app is live! 🎉

Vercel gives you a URL like: `https://payroll-recon-xyz.vercel.app`

---

## STEP 3 — Every future update

Just push to GitHub and Vercel auto-redeploys:
```bash
git add .
git commit -m "your change description"
git push
```

---

## Getting your Anthropic API Key

1. Go to **console.anthropic.com**
2. Sign in / Sign up (free to create account)
3. Click **"API Keys"** in the left sidebar
4. Click **"Create Key"** → Copy it
5. ⚠️ Save it somewhere safe — you can't see it again

> **Cost note**: Claude API is pay-as-you-go. The AI analysis in this app uses `claude-sonnet-4-20250514`. Typical usage for reconciling 100 employees costs less than $0.05. You get some free credits on signup.

---

## Troubleshooting

| Problem | Fix |
|---|---|
| "ANTHROPIC_API_KEY not configured" | Add the env var in Vercel → Settings → Environment Variables, then redeploy |
| AI analysis not working but app loads | Check Vercel → Functions tab for error logs |
| Build fails | Check Vercel build logs; ensure `package.json` is in root folder |
| Blank page after deploy | Open browser console (F12) and check for errors |

---

## Local Development (optional)

```bash
npm install
npm install -g vercel       # Install Vercel CLI

cp .env.example .env.local  # Add your API key here

vercel dev                  # Runs both Vite + serverless functions locally
```

Open http://localhost:3000
