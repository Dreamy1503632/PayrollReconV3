# Payroll Reconciliation Tool

AI-powered payroll reconciliation between two payroll sources (e.g. Oracle Fusion HCM vs RAMCO Payroll).

## Tech Stack
- **Frontend**: React 18 + Vite + Recharts
- **AI Backend**: Vercel Serverless Function → Anthropic Claude API
- **Storage**: Browser localStorage (no database needed)

## Local Development

### 1. Install dependencies
```bash
npm install
```

### 2. Set up your API key
```bash
cp .env.example .env.local
# Edit .env.local and add your Anthropic API key
```

### 3. Run locally
```bash
npm run dev
```
Open http://localhost:5173

> The `/api/claude` serverless function runs automatically via Vite dev server proxy — no separate backend needed locally (see note below).

**Note for local dev**: Vite doesn't run Vercel serverless functions. For local API testing, either:
- Use `vercel dev` (install Vercel CLI: `npm i -g vercel`), OR
- The app works fine in Demo Mode without an API key

## Deploy to Vercel

See the full step-by-step guide in DEPLOY_GUIDE.md.

## Project Structure

```
payroll-recon/
├── api/
│   └── claude.js          ← Vercel serverless function (keeps API key secret)
├── src/
│   ├── App.jsx            ← Main application (3000+ lines, all-in-one)
│   └── main.jsx           ← React entry point
├── index.html
├── vite.config.js
├── vercel.json            ← Routing config for Vercel
└── package.json
```
