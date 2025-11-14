# GitHub Pages Setup Guide

Deploy the Nevatars Asset Dashboard to GitHub Pages for permanent, globally accessible hosting.

## Why GitHub Pages?

- **No server needed** - Works 24/7 without running .bat files
- **Global access** - Anyone with the link can view from anywhere
- **Free hosting** - Completely free for public repositories
- **Simple updates** - Just push HTML changes (data comes from Google Sheets!)

---

## How It Works

```
Maya "Sync Registry"
  ↓
Updates Google Sheets (via API)
  ↓
Dashboard on GitHub Pages reads from Google Sheets
  ↓
Everyone sees latest data instantly!
```

**Key benefit:** No need to commit/push data files! Dashboard always shows live Google Sheets data.

---

## Prerequisites

Before starting, make sure you have:

1. ✅ Google Sheets published to web (see `GOOGLE_SHEETS_SETUP.md`)
2. ✅ Dashboard configured with Google Sheets URL
3. ✅ GitHub account created
4. ✅ Git installed on your computer

---

## Setup Instructions

### Step 1: Create GitHub Repository

1. Go to [GitHub](https://github.com) and log in

2. Click the **+** button (top right) → **New repository**

3. Configure repository:
   - **Repository name:** `nevatars-asset-dashboard` (or any name you like)
   - **Visibility:** **Public** (required for free GitHub Pages)
   - **Description:** "Nevatars Asset Dashboard - YAML → Google Sheets → Web"
   - ⚠️ **DO NOT** check "Add a README file"
   - ⚠️ **DO NOT** add .gitignore or license yet

4. Click **Create repository**

5. **Copy the repository URL** shown on the next page:
   ```
   https://github.com/YOUR_USERNAME/nevatars-asset-dashboard.git
   ```

---

### Step 2: Initialize Git in _registry Folder

Open a terminal/command prompt and run these commands:

```bash
cd S:\PROJECTS\060_NEVATARS\00_pipeline\_registry
```

Initialize Git repository:
```bash
git init
```

---

### Step 3: Add Files to Git

Add the necessary files:

```bash
git add assets_dashboard.html
git add GOOGLE_SHEETS_SETUP.md
git add GITHUB_PAGES_SETUP.md
git add README_DASHBOARD.md
git add .github
```

**Note:** We are NOT adding `assets_data.json` or `start_server.py` since they're not needed on GitHub Pages!

Create first commit:
```bash
git commit -m "Initial commit: Nevatars Asset Dashboard with Google Sheets integration"
```

---

### Step 4: Push to GitHub

Connect to your GitHub repository:

```bash
git remote add origin https://github.com/YOUR_USERNAME/nevatars-asset-dashboard.git
```

**Replace `YOUR_USERNAME/nevatars-asset-dashboard` with your actual repository URL from Step 1!**

Push to GitHub:
```bash
git branch -M main
git push -u origin main
```

**Note:** GitHub may ask for your username and password:
- **Username:** Your GitHub username
- **Password:** Use a Personal Access Token (not your account password)
  - Create token at: https://github.com/settings/tokens
  - Select scope: `repo`
  - Copy token and use as password

---

### Step 5: Enable GitHub Pages

1. Go to your GitHub repository page:
   ```
   https://github.com/YOUR_USERNAME/nevatars-asset-dashboard
   ```

2. Click **Settings** (top menu)

3. Click **Pages** (left sidebar)

4. Under **Source**:
   - **Branch:** Select `main`
   - **Folder:** Select `/ (root)`

5. Click **Save**

6. GitHub will show you the URL where your site is published:
   ```
   Your site is live at https://YOUR_USERNAME.github.io/nevatars-asset-dashboard/
   ```

7. **Wait 1-2 minutes** for the first deployment to complete

---

### Step 6: Access Your Dashboard

Your dashboard is now live at:

```
https://YOUR_USERNAME.github.io/nevatars-asset-dashboard/assets_dashboard.html
```

**Share this URL with your team!** Everyone can access it from anywhere.

---

## Updating the Dashboard

### When Do You Need to Update GitHub?

**You DON'T need to update GitHub when:**
- ✅ Asset data changes (Google Sheets updates automatically!)
- ✅ Running "Sync Registry" in Maya
- ✅ Adding/moving/archiving assets

**You ONLY need to update GitHub when:**
- ❌ Changing the HTML/CSS design
- ❌ Fixing bugs in the dashboard
- ❌ Adding new features

---

### How to Update Dashboard Code

If you modify `assets_dashboard.html`:

```bash
cd S:\PROJECTS\060_NEVATARS\00_pipeline\_registry
git add assets_dashboard.html
git commit -m "Update dashboard design"
git push
```

Wait 1-2 minutes, then refresh browser to see changes!

---

## Workflow Summary

### Daily workflow (updating data):

```
1. Open Maya
2. Click "Sync Registry" button
3. Done! 🎉
```

That's it! The dashboard automatically shows updated data from Google Sheets.

### Occasional workflow (updating dashboard design):

```
1. Edit assets_dashboard.html
2. git add assets_dashboard.html
3. git commit -m "Update dashboard"
4. git push
5. Wait 1-2 minutes
6. Refresh browser
```

---

## Troubleshooting

### "404 Page Not Found"

**Problem:** GitHub Pages URL shows 404

**Solutions:**
1. Wait 2-3 minutes - first deployment takes time
2. Check repository is **Public** (Settings → Change visibility)
3. Check Settings → Pages shows "Your site is live at..."
4. Make sure you're accessing the full URL with `/assets_dashboard.html`

---

### "Error loading data" in Dashboard

**Problem:** Dashboard loads but shows error

**Solutions:**
1. **Most common:** Google Sheets URL not configured
   - Open `assets_dashboard.html` in text editor
   - Check line 373: `const GOOGLE_SHEETS_URL = '...'`
   - Make sure it has your actual published Google Sheets URL
   - See `GOOGLE_SHEETS_SETUP.md` for instructions

2. Google Sheets not published:
   - File → Share → Publish to web
   - Make sure you clicked "Publish" and confirmed

3. CORS issue:
   - Make sure you're using "Publish to web" URL (starts with `2PACX-...`)
   - Regular sharing links won't work

---

### Dashboard Shows Old Data

**Problem:** Dashboard doesn't update after "Sync Registry"

**Solutions:**
1. Check Google Sheets directly - does it have new data?
   - If NO → Run "Sync Registry" again in Maya
   - If YES → Continue to next step

2. Hard refresh browser:
   - Windows: Ctrl+Shift+R
   - Mac: Cmd+Shift+R

3. The dashboard always fetches fresh data from Google Sheets on page load

---

### "Permission denied" When Pushing

**Problem:** Git push fails with authentication error

**Solutions:**
1. Create Personal Access Token:
   - https://github.com/settings/tokens
   - Click "Generate new token (classic)"
   - Select scope: `repo`
   - Copy token

2. Use token as password when Git asks

3. Or configure credential helper:
   ```bash
   git config --global credential.helper wincred
   ```

---

### GitHub Pages Shows Old Version

**Problem:** Pushed changes but site doesn't update

**Solutions:**
1. Check Actions tab - deployment should be running
2. Wait 2-3 minutes for deployment to complete
3. Hard refresh browser (Ctrl+Shift+R)
4. Check commit appeared on GitHub (look at commit history)

---

## Advanced: Custom Domain (Optional)

Want to use your own domain like `dashboard.nevatars.com`?

### Step 1: Add CNAME File

```bash
cd S:\PROJECTS\060_NEVATARS\00_pipeline\_registry
echo dashboard.nevatars.com > CNAME
git add CNAME
git commit -m "Add custom domain"
git push
```

### Step 2: Configure DNS

At your domain registrar (GoDaddy, Namecheap, etc.):

1. Add a **CNAME record**:
   - Host: `dashboard` (or `@` for root domain)
   - Points to: `YOUR_USERNAME.github.io`

### Step 3: Enable in GitHub

1. Settings → Pages
2. Custom domain: `dashboard.nevatars.com`
3. Check "Enforce HTTPS"
4. Wait 5-10 minutes for DNS propagation

Your dashboard will now be at: `https://dashboard.nevatars.com/assets_dashboard.html`

---

## Security & Privacy

**Important to understand:**

- **Public repository** = Anyone can see the HTML code on GitHub
- **Private repository** = Requires GitHub Pro/Team ($4-7/month per user)
- **Google Sheets published** = Anyone with link can view data (read-only)
- **Dashboard is read-only** = No one can modify your assets via web

**For most teams this is fine because:**
- Asset metadata is not sensitive information
- Read-only access keeps data safe
- Convenient for team collaboration
- YAML files remain private on your network

**If you need private hosting:**
- Upgrade to GitHub Pro (private repos with Pages)
- Use Netlify/Vercel (free tier with password protection)
- Host on company's internal server

---

## Files in GitHub Repository

After setup, your repository will have:

```
nevatars-asset-dashboard/
├── assets_dashboard.html          ← The web dashboard
├── GOOGLE_SHEETS_SETUP.md         ← Google Sheets publish instructions
├── GITHUB_PAGES_SETUP.md          ← This file
├── README_DASHBOARD.md            ← General dashboard documentation
└── .github/
    └── workflows/
        └── deploy.yml             ← Auto-deployment workflow
```

**Files NOT in repository (stay local):**
- `assets_data.json` - Not needed (using Google Sheets!)
- `start_server.py` - Not needed (GitHub Pages is the server!)
- `START_DASHBOARD_SERVER.bat` - Not needed (only for local testing)
- Any `.yaml` files - Stay private on your network

---

## Complete Workflow Diagram

```
┌─────────────────────────────────────────────────────────────┐
│ Your Computer                                               │
│                                                             │
│  Maya → Sync Registry → Updates Google Sheets (via API)    │
│         (No Git needed!)                                    │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ Google Sheets (Cloud)                                       │
│                                                             │
│  - Always up-to-date                                        │
│  - Published to web (CSV format)                            │
│  - Public read-only URL                                     │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ GitHub Pages (Cloud)                                        │
│                                                             │
│  - Hosts assets_dashboard.html                              │
│  - Fetches data from Google Sheets                          │
│  - Globally accessible                                      │
└─────────────────────────────────────────────────────────────┘
                              ↓
┌─────────────────────────────────────────────────────────────┐
│ Your Team (Anywhere in the world!)                          │
│                                                             │
│  Opens: https://YOUR_USERNAME.github.io/.../dashboard.html  │
│  Sees: Live data from Google Sheets                         │
└─────────────────────────────────────────────────────────────┘
```

---

## Next Steps

1. ✅ Complete `GOOGLE_SHEETS_SETUP.md` first (publish Google Sheets)
2. ✅ Configure dashboard with Google Sheets URL
3. ✅ Follow this guide to deploy to GitHub Pages
4. ✅ Share URL with team!
5. 🎉 Enjoy effortless asset tracking!

---

## Need Help?

- **Can't create repository?** → Make sure you're logged into GitHub
- **Git commands failing?** → Make sure Git is installed (`git --version`)
- **Dashboard won't load?** → Check `GOOGLE_SHEETS_SETUP.md` for configuration
- **Data not updating?** → Check Google Sheets is actually being updated by Maya script

---

**Made with ❤️ for the Nevatars Team**
**Enjoy your globally accessible, always up-to-date Asset Dashboard!**
