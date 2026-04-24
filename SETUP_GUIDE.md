# 🥁 Azlan's Percussion Hub — Deployment Guide
## PWA on GitHub Pages + PIN Sync (No Google Login Required)

---

## What You'll Have When Done
- A real URL like: `https://YOUR-USERNAME.github.io/azlan-percussion/`
- Works on **Android phone**, **Chromebook**, and **PC**
- Installs to home screen like a real app (no App Store needed)
- All progress syncs across devices using a **6-digit PIN** — no Google account needed
- Works **offline** too once installed

---

## STEP 1 — Get a Free JSONbin API Key (5 min)

JSONbin.io stores Azlan's data in the cloud for free. No account age restrictions.

1. Go to **https://jsonbin.io**
2. Click **Sign Up** — use your (parent) email
3. After signing in, click your profile icon (top right) → **API Keys**
4. Copy your **X-Master-Key** (looks like: `$2a$10$abc123...`)

**Free tier:** 10,000 requests/month — more than enough for one student.

---

## STEP 2 — Add Your API Key to the App (2 min)

1. Open `index.html` in any text editor
2. Near the top, find this line:
```
const JSONBIN_KEY = '$2a$10$REPLACE_WITH_YOUR_JSONBIN_MASTER_KEY';
```
3. Replace the placeholder with your actual key from Step 1
4. Save the file

That's the only code change needed.

---

## STEP 3 — Generate App Icons (2 min)

1. Open `generate-icons.html` in Chrome
2. Two download links appear — click both
3. Move `icon-192.png` and `icon-512.png` into the `icons/` folder

---

## STEP 4 — Deploy to GitHub Pages (10 min)

1. Go to **https://github.com** → Sign up (free)
2. Click **+** → **New repository** → name it `azlan-percussion` → **Public** → Create
3. Click **"uploading an existing file"**
4. Drag all 5 items from `azlan-pwa` folder: `index.html`, `manifest.json`, `sw.js`, `generate-icons.html`, `icons/` folder
5. Click **"Commit changes"**
6. Click **Settings** → **Pages** → Source: **main / root** → Save
7. Wait 2-3 minutes → your URL: `https://YOUR-USERNAME.github.io/azlan-percussion/`

---

## STEP 5 — Create Azlan's 6-Digit PIN

1. Open the app URL in Chrome
2. Tap **"Create PIN"** tab
3. Enter any 6 digits (write it down — use it on every device!)
4. Tap **"Create & Connect"**

**Write the PIN down somewhere safe. Same PIN = same data on all devices.**

---

## STEP 6 — Install on Each Device

**Android:** Chrome menu (⋮) → Add to Home screen → Add → Enter PIN
**Chromebook:** Address bar install icon (⊕) → Install → Enter PIN
**PC:** Address bar install icon (⊕) → Install → Enter PIN

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| Connect button spins forever | Check JSONbin API key is correct in index.html |
| Data not syncing | Confirm exact same 6-digit PIN on all devices |
| Forgot PIN | Check browser DevTools → Application → localStorage → `azlan_saved_pin` |
| App not updating | Hard refresh: Ctrl+Shift+R |

---

## Checklist

- [ ] JSONbin account + API key copied
- [ ] `index.html` updated with real API key
- [ ] Icons in `icons/` folder
- [ ] Files uploaded to GitHub + Pages enabled
- [ ] PIN created and written down
- [ ] Installed on Android phone + Chromebook
- [ ] Tested: progress on one device appears on another ✓

---
*Azlan's Percussion Hub · Scoggins Band · Frisco ISD 2026-2027*
