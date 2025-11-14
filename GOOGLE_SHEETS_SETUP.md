# Google Sheets "Publish to Web" Setup

This guide shows you how to get the public URL from your Google Sheets so the web dashboard can read data directly.

---

## Step 1: Open Your Google Sheet

Open the Nevatars Asset Tracker in Google Sheets (the one that nev_sync_registry.py updates).

**Sheet URL should look like:**
```
https://docs.google.com/spreadsheets/d/YOUR_SHEET_ID/edit
```

---

## Step 2: Publish to Web

1. In Google Sheets, click **File** → **Share** → **Publish to web**

2. A dialog will open with two dropdowns:

   **First dropdown (What to publish):**
   - Select: **"By Category"** (or whichever sheet/tab you want to show in the dashboard)
   - You can also select "Entire document" to publish all sheets

   **Second dropdown (Format):**
   - Select: **CSV**

3. Click **Publish**

4. Google will show a warning: "Are you sure you want to publish this selection?"
   - Click **OK**

5. You'll see a URL like this:
   ```
   https://docs.google.com/spreadsheets/d/e/2PACX-1vQa3b.../pub?gid=0&single=true&output=csv
   ```

6. **Copy this entire URL** - you'll need it in the next step!

---

## Step 3: Configure the Dashboard

1. Open `assets_dashboard.html` in a text editor (Notepad, VS Code, etc.)

2. Find this line near the top of the `<script>` section (around line 373):
   ```javascript
   const GOOGLE_SHEETS_URL = 'PASTE_YOUR_GOOGLE_SHEETS_URL_HERE';
   ```

3. Replace `PASTE_YOUR_GOOGLE_SHEETS_URL_HERE` with your actual URL from Step 2:
   ```javascript
   const GOOGLE_SHEETS_URL = 'https://docs.google.com/spreadsheets/d/e/2PACX-1vQa3b.../pub?gid=0&single=true&output=csv';
   ```

4. Save the file

---

## Step 4: Test Locally (Optional)

Before deploying to GitHub Pages, test locally:

1. Double-click `START_DASHBOARD_SERVER.bat`
2. Open the Local URL in your browser
3. Dashboard should load data from Google Sheets!

**If you see an error:**
- Make sure the Google Sheets URL is correct
- Make sure you published the correct sheet (By Category, By Name, etc.)
- Check browser console (F12) for error messages

---

## Step 5: Deploy to GitHub Pages

Now that the dashboard is configured, you're ready to deploy to GitHub Pages!

See `GITHUB_PAGES_SETUP.md` for deployment instructions.

---

## Which Sheet Should I Publish?

Your Google Sheets has 4 tabs after running "Sync Registry":
1. **By Category** - Assets grouped by category (recommended)
2. **By Name** - Assets sorted alphabetically
3. **By Status** - Assets grouped by status (WIP, Done, etc.)
4. **By Type** - Assets grouped by type

**Recommendation:** Publish **"By Category"** sheet - it shows all assets with all columns, which gives the dashboard the most flexibility for filtering and sorting.

---

## Can I Change the Published Sheet Later?

Yes! Just repeat Step 2 and:
1. File → Share → Publish to web
2. Click "Published content & settings"
3. Change the dropdown to a different sheet
4. The URL stays the same - no need to update the HTML!

---

## Security & Privacy

**Important to understand:**

- **Published URL is PUBLIC** - Anyone with the link can view the data
- **Read-only** - No one can edit via this URL
- **Always up-to-date** - Shows current data from Google Sheets in real-time

**If you need private data:**
- Don't publish the sheet to web
- Use the local JSON option instead (not accessible via internet)
- Or use Google Sheets API with authentication (more complex)

For most teams, having asset data public is fine since:
- It's just asset metadata (names, status, categories)
- No sensitive information
- Read-only access
- Convenient for team collaboration

---

## Updating Data

**Great news:** Once published, the workflow is super simple!

```
Maya "Sync Registry"
  ↓
Updates Google Sheets
  ↓
Dashboard automatically shows new data (refresh browser)
  ↓
Done! No commits, no pushes, no Git!
```

The dashboard fetches fresh data from Google Sheets every time someone loads the page!

---

## Troubleshooting

### Dashboard shows "Error loading data"

**Problem:** Can't fetch from Google Sheets URL

**Solutions:**
1. Make sure the URL is published (File → Share → Publish to web)
2. Check the URL is correct in `assets_dashboard.html`
3. Make sure the URL format is CSV (ends with `output=csv`)
4. Try opening the URL directly in browser - should download a CSV file

### Dashboard shows old data

**Problem:** Data doesn't update after running "Sync Registry"

**Solutions:**
1. Check Google Sheets directly - does it have new data?
2. If yes, hard refresh browser: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)
3. Check browser console (F12) for caching issues
4. Clear browser cache

### "This page can't load Google Sheets"

**Problem:** CORS or network restrictions

**Solutions:**
1. Make sure you're using the "Publish to web" URL, not the regular sharing link
2. The published URL should start with: `https://docs.google.com/spreadsheets/d/e/2PACX-...`
3. Regular sharing links don't work - must use "Publish to web" URL

### Published URL shows "Access Denied"

**Problem:** Sheet is not actually published

**Solutions:**
1. Go to File → Share → Publish to web
2. Make sure you clicked "Publish" and confirmed
3. Check "Published content & settings" shows sheet is published

---

## URL Format Reference

**Correct format (Publish to web):**
```
https://docs.google.com/spreadsheets/d/e/2PACX-1vQa3b4c5d6e7f8g9h0/pub?gid=0&single=true&output=csv
```

**Wrong format (Regular sharing link - won't work):**
```
https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/edit#gid=0
```

The key difference:
- Published URL has `/e/2PACX-...` and `pub?...output=csv`
- Sharing link has `/d/1AbC...` and `/edit`

---

**Need Help?**

- Can't find "Publish to web"? → File menu → Share → Publish to web
- Dashboard not loading? → Check browser console (F12) for errors
- Want to unpublish? → File → Share → Publish to web → "Stop publishing"

---

**Made with ❤️ for the Nevatars Team**
