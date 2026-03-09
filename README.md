# Yihu Construction Document Generator
## Setup Instructions

---

## Files Required
Place these files in the same folder on your web server:
- `index.html` — Main application
- `manifest.json` — PWA manifest
- `sw.js` — Service worker (offline/install support)
- `smc logo.png` — Your company logo (rename your logo to this exact name)

---

## Step 1: Firebase Setup (Cloud History)

1. Go to https://console.firebase.google.com
2. Click **"Add project"** → Name it: `yihu-construction`
3. Disable Google Analytics (optional) → **Create Project**
4. Click **"Web"** icon (`</>`) to add a web app
5. App nickname: `yihu-docs` → Click **Register App**
6. **Copy the firebaseConfig object** — looks like:
   ```js
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "yihu-construction.firebaseapp.com",
     projectId: "yihu-construction",
     storageBucket: "yihu-construction.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abcdef"
   };
   ```
7. In the left sidebar: **Build → Firestore Database**
8. Click **"Create database"** → Start in **Test mode** → Choose your region → Enable

### Paste Config into index.html
Open `index.html` and find this section near the top:
```js
// ===== REPLACE WITH YOUR FIREBASE CONFIG =====
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  ...
```
Replace it with your copied config.

---

## Step 2: Deploy on Web Server

### Option A: Free hosting on Firebase Hosting
```bash
npm install -g firebase-tools
firebase login
firebase init hosting
firebase deploy
```

### Option B: Any web server (Nginx, Apache, etc.)
Copy all 4 files to your server's web root. The app must be served over **HTTPS** for PWA install to work.

### Option C: Local testing
Use a local server (not just opening the file directly):
```bash
# Python
python -m http.server 8000

# Node
npx serve .
```

---

## Step 3: Using the App

### Creating Documents
1. Select document type (Invoice / Quotation / Receipt)
2. Document number is **auto-generated** (e.g. YHC-INV-0001)
3. Fill in client name, date, subject
4. Add line items with quantity and rate
5. Amounts display in **thousands (K), millions (M), billions (B)**
6. Click ☁️ Save to store in Firebase cloud

### Downloading
- **PDF** → High quality A4 PDF
- **Image** → PNG screenshot

### Install as App
- On mobile (Android): A banner will appear at the bottom — tap **Install**
- On desktop Chrome: Look for the install icon in the address bar

---

## Firestore Data Structure

Each document is stored in the `documents` collection:
```json
{
  "type": "INVOICE",
  "docNumber": "YHC-INV-0042",
  "date": "2025-03-09",
  "client": "ABC Construction Ltd",
  "subject": "Site works at Mukono",
  "items": [
    { "desc": "Excavation works", "qty": 1, "price": 5000000, "total": 5000000 }
  ],
  "total": 5000000,
  "paid": 2000000,
  "createdAt": "2025-03-09T10:30:00.000Z"
}
```

---

## Company Details (pre-configured)
- **Company:** YIHU CONSTRUCTION SMC LIMITED
- **TIN:** 1046620017
- **Tel:** 0783933666
- **Email:** yihuconstruction88@gmail.com
- **Website:** www.yihuconstruction.com
- **Address:** Nakasajja Village, Mukono District, Gayaza–Kayunga Road, Uganda
- **Bank:** Pearl Bank — Account: 4020064000075
- **Account Name:** YIHU CONSTRUCTION COMPANY SMC LTD
