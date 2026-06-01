# 🍼 BabyLog — Setup Guide

## What You Built
A Progressive Web App (PWA) that works like an Android app. It stores all data in a Google Sheet that only you and your wife can access.

---

## Step 1 — Create a Google Cloud Project

1. Go to https://console.cloud.google.com/
2. Create a new project, e.g. "BabyLog"
3. Enable these APIs (search in "APIs & Services > Enable APIs"):
   - **Google Sheets API**
   - **Google Drive API**
4. Go to **APIs & Services > OAuth consent screen**
   - Choose "External"
   - Fill in App name: `BabyLog`, your email
   - Add scopes: `spreadsheets`, `drive.file`
   - Add **test users**: your Gmail + your wife's Gmail
5. Go to **APIs & Services > Credentials > Create Credentials > OAuth 2.0 Client ID**
   - Application type: **Web application**
   - Authorized JavaScript origins: add your hosting URL (e.g. `https://yourdomain.com`)
   - Copy the **Client ID**

---

## Step 2 — Edit index.html

Open `index.html` and replace the two placeholders:

```
const CLIENT_ID = 'YOUR_GOOGLE_CLIENT_ID';   // line ~280
data-client_id="YOUR_GOOGLE_CLIENT_ID"        // line ~140
```

Paste your Client ID in both places.

---

## Step 3 — Create the Google Sheet

1. Go to https://sheets.google.com and create a new blank spreadsheet
2. Name it "BabyLog Data"
3. Create 3 tabs (sheets): **Feedings**, **Diapers**, **Notes**
4. Share the spreadsheet with Edit access to both your Gmail and your wife's Gmail
5. Copy the Sheet ID from the URL:
   `https://docs.google.com/spreadsheets/d/**THIS_IS_THE_ID**/edit`

---

## Step 4 — Host the App

You need to host the files (Google Sign-In requires HTTPS). Options:

### Option A — GitHub Pages (free)
1. Create a GitHub account
2. New repository > upload `index.html` and `manifest.json`
3. Settings > Pages > Deploy from main branch
4. Your URL: `https://yourusername.github.io/babylog`

### Option B — Netlify (free, drag & drop)
1. Go to https://netlify.com
2. Drag your folder to deploy
3. Get a URL like `https://babylog-abc123.netlify.app`

### Option C — Firebase Hosting (free)
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

---

## Step 5 — Install on Android

1. Open Chrome on your Android phone
2. Go to your hosted URL
3. Sign in with Google
4. Paste your Sheet ID when prompted
5. Chrome will show **"Add to Home Screen"** — tap it
6. BabyLog is now installed like a native app! 📱

Your wife does the same steps on her phone — same Sheet ID, her Google account.

---

## Data Structure in Google Sheets

### Feedings tab
| Timestamp | Type | Side | Duration (min) | Amount (ml) | Content | Notes | LoggedBy |

### Diapers tab
| Timestamp | Type | Texture | Color | Notes | LoggedBy |

### Notes tab
| Timestamp | Category | Note | LoggedBy |

---

## Features
- ✅ Log breastfeeding (side + duration)
- ✅ Log bottle feeding (ml + content type)
- ✅ Log diapers (type + texture + color)
- ✅ Free-text notes with categories
- ✅ Today's summary dashboard
- ✅ 7-day stats + texture breakdown
- ✅ Chronological history timeline
- ✅ Shows who logged each entry
- ✅ Works offline (once installed)
- ✅ Both parents share the same Sheet
