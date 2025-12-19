# Equinox Shop Visual Audit - Deployment Guide

## 🚀 Quick Start (5 Minutes)

This guide will walk you through deploying your visual audit tool to Vercel with a secure backend.

---

## Step 1: Get Your Claude API Key

1. Go to **console.anthropic.com**
2. Sign up or log in
3. Click **Settings** → **API Keys**
4. Click **Create Key**
5. Name it "Equinox Audit"
6. **Copy the key** (starts with `sk-ant-`)
7. Add $10 in billing (Settings → Plans & Billing)

**IMPORTANT:** Don't share this key with anyone!

---

## Step 2: Set Up GitHub Repository

1. Go to **github.com** and create a new repository
2. Name it: `equinox-visual-audit`
3. Make it **Public** (required for free Vercel hosting)
4. Don't add README, .gitignore, or license yet

---

## Step 3: Upload Your Files

You have 4 files to upload:
- `index.html` (the frontend)
- `api/analyze.js` (the backend function)
- `vercel.json` (configuration)
- `README.md` (this file)

**Two ways to upload:**

### Option A: GitHub Web Interface (Easiest)
1. In your new repo, click **Add file** → **Upload files**
2. Drag all 4 files into the browser
3. Make sure `analyze.js` goes in an `api` folder:
   - Create folder: `api/analyze.js`
4. Click **Commit changes**

### Option B: Git Command Line (If you know Git)
```bash
git clone https://github.com/YOUR-USERNAME/equinox-visual-audit.git
cd equinox-visual-audit
# Copy all 4 files here
git add .
git commit -m "Initial commit"
git push
```

Your repo structure should look like:
```
equinox-visual-audit/
├── index.html
├── api/
│   └── analyze.js
├── vercel.json
└── README.md
```

---

## Step 4: Deploy to Vercel

1. Go to **vercel.com**
2. Sign up with your GitHub account
3. Click **Add New** → **Project**
4. Find your `equinox-visual-audit` repo
5. Click **Import**
6. **CRITICAL:** Before deploying, add environment variable:
   - Click **Environment Variables**
   - Name: `CLAUDE_API_KEY`
   - Value: [paste your API key here]
   - Click **Add**
7. Click **Deploy**
8. Wait 1-2 minutes...
9. **Done!** Your app is live!

---

## Step 5: Get Your URL

After deployment finishes:
1. You'll see: "🎉 Congratulations!"
2. Your URL will be: `https://equinox-visual-audit.vercel.app`
3. Click **Visit** to test it

---

## Step 6: Test It

1. Open your deployed URL
2. Select "Men's Wall Merchandising"
3. Upload a photo
4. Click "Analyze Display"
5. You should see results in ~5-10 seconds!

---

## 🔒 Security Notes

✅ **Your API key is secure:**
- Stored as environment variable in Vercel
- Never exposed in the frontend code
- Only accessible by your backend function

✅ **Team can use it safely:**
- Just share the URL: `https://equinox-visual-audit.vercel.app`
- No API keys needed
- Works on any device

✅ **Cost control:**
- Each evaluation costs ~$0.02
- 50 tests = ~$1
- Monitor usage at console.anthropic.com

---

## 📱 Share with Your Team

Just send them the URL:
```
https://equinox-visual-audit.vercel.app
```

They can:
- Open on phone or computer
- Upload photos
- Get instant evaluations
- No login or setup required

---

## 🛠️ Troubleshooting

**"API key not configured" error:**
- Go to Vercel dashboard → Your project → Settings → Environment Variables
- Make sure `CLAUDE_API_KEY` is set
- Redeploy: Deployments → Click ⋯ → Redeploy

**"CORS error" in browser:**
- The serverless function should handle this automatically
- If issues persist, check browser console for details

**Evaluations taking too long:**
- Normal: 5-10 seconds
- If >30 seconds, check Claude API status at status.anthropic.com

**"Module not found" error:**
- Make sure `analyze.js` is in the `api` folder
- File path must be: `api/analyze.js`

---

## 💰 Cost Tracking

Monitor your usage:
1. Go to console.anthropic.com
2. Click **Usage** in left sidebar
3. See real-time costs

Expected costs:
- 10 tests: $0.20
- 50 tests: $1.00
- 100 tests: $2.00

---

## 🔄 Making Updates

To update the rubric or UI:

1. Edit files in GitHub
2. Vercel automatically redeploys
3. Changes live in ~1 minute

Or:
1. Edit locally
2. Push to GitHub
3. Auto-deploys

---

## 🎯 Next Steps

After successful demo:
- Revoke old API keys (keep only production key)
- Set spending limits in Anthropic console
- Consider upgrading to paid Vercel plan for custom domain

---

## 📞 Need Help?

Common issues:
- **Won't deploy:** Check file structure matches exactly
- **API errors:** Verify API key is correct and has billing
- **Slow responses:** Claude API might be busy, try again

---

## ✨ You're Done!

Your secure, production-ready visual audit tool is live. Share the URL with your team and start testing!
