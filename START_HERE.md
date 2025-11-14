# 🚀 Quick Start - Deploying Your Dashboard

Follow these steps **in order** to get your globally accessible asset dashboard up and running!

---

## Step-by-Step Setup (30 minutes)

### ✅ Step 1: Publish Google Sheets (5 minutes)

**File:** `GOOGLE_SHEETS_SETUP.md`

**What you'll do:**
- Open your Google Sheet
- File → Share → Publish to web
- Select "By Category" sheet → CSV format
- Copy the published URL

**Result:** You'll have a URL like:
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vQa3b.../pub?gid=0&single=true&output=csv
```

---

### ✅ Step 2: Configure Dashboard (2 minutes)

**File:** Edit `assets_dashboard.html`

**What you'll do:**
- Open `assets_dashboard.html` in a text editor
- Find line 373: `const GOOGLE_SHEETS_URL = 'PASTE_YOUR_GOOGLE_SHEETS_URL_HERE';`
- Replace with your actual URL from Step 1
- Save the file

**Result:** Dashboard is now configured to read from Google Sheets!

---

### ✅ Step 3: Test Locally (Optional, 5 minutes)

**File:** Double-click `START_DASHBOARD_SERVER.bat`

**What you'll do:**
- Run the local server
- Open http://localhost:8080/assets_dashboard.html
- Verify dashboard loads with your Google Sheets data

**Result:** Confirmed everything works before deploying!

---

### ✅ Step 4: Create GitHub Repository (3 minutes)

**File:** `GITHUB_PAGES_SETUP.md` (Steps 1-4)

**What you'll do:**
- Go to GitHub.com
- Create new public repository
- Name it: `nevatars-asset-dashboard`
- Copy the repository URL

**Result:** You have a GitHub repo ready for deployment!

---

### ✅ Step 5: Deploy to GitHub Pages (10 minutes)

**File:** `GITHUB_PAGES_SETUP.md` (Steps 2-6)

**What you'll do:**
```bash
cd S:\PROJECTS\060_NEVATARS\00_pipeline\_registry
git init
git add assets_dashboard.html GOOGLE_SHEETS_SETUP.md GITHUB_PAGES_SETUP.md README_DASHBOARD.md .github
git commit -m "Initial commit: Nevatars Asset Dashboard"
git remote add origin YOUR_REPO_URL_HERE
git branch -M main
git push -u origin main
```

Then enable GitHub Pages in repository settings.

**Result:** Dashboard is live on the internet!

---

### ✅ Step 6: Share with Team! (1 minute)

**What you'll do:**
- Copy your GitHub Pages URL
- Share with team via email/Slack/chat

**Your URL will be:**
```
https://YOUR_USERNAME.github.io/nevatars-asset-dashboard/assets_dashboard.html
```

**Result:** Everyone can access the dashboard from anywhere! 🎉

---

## Daily Usage (Super Simple!)

Once deployed, updating data is incredibly easy:

```
1. Open Maya
2. Click "Sync Registry" shelf button
3. Done!
```

The dashboard automatically shows updated data because it reads directly from Google Sheets!

**No Git commands needed for daily use!**

---

## When You Need Git Again

You only use Git when changing the dashboard design/code:

```bash
cd S:\PROJECTS\060_NEVATARS\00_pipeline\_registry
git add assets_dashboard.html
git commit -m "Update dashboard"
git push
```

---

## Files Guide

Here's what each file does:

| File | Purpose |
|------|---------|
| `START_HERE.md` | ← You are here! Quick start guide |
| `GOOGLE_SHEETS_SETUP.md` | How to publish Google Sheets to web |
| `GITHUB_PAGES_SETUP.md` | Complete GitHub Pages deployment guide |
| `README_DASHBOARD.md` | General dashboard documentation |
| `assets_dashboard.html` | The actual dashboard (edit to configure) |
| `START_DASHBOARD_SERVER.bat` | Local testing server (optional) |

---

## Quick Troubleshooting

### Dashboard shows "Error loading data"
→ Check Google Sheets URL is configured in `assets_dashboard.html` line 373

### Can't push to GitHub
→ Make sure you created a Personal Access Token (not regular password)

### GitHub Pages shows 404
→ Wait 2-3 minutes for deployment, make sure repository is Public

### Data doesn't update
→ Check Google Sheets was actually updated by "Sync Registry"

---

## Architecture Overview

Here's how everything connects:

```
Maya Scripts
    ↓
YAML Files (source of truth)
    ↓
"Sync Registry" Button
    ↓
Google Sheets (via API)
    ↓
Dashboard on GitHub Pages (reads Google Sheets)
    ↓
Your Team (views dashboard via browser)
```

**Key insight:** Data flows from YAML → Google Sheets → Dashboard. GitHub only hosts the HTML, not the data!

---

## Ready to Start?

1. Read `GOOGLE_SHEETS_SETUP.md` first
2. Then read `GITHUB_PAGES_SETUP.md`
3. Follow the steps carefully
4. Ask for help if you get stuck!

**Estimated total time:** 30 minutes for first-time setup

**After setup:** Zero maintenance! Just click "Sync Registry" in Maya and you're done.

---

**Made with ❤️ for the Nevatars Team**
**Let's get your dashboard live!**
