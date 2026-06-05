# Enable Google Sign-In for LatihanJawara

## Quick Setup (2 minutes)

### Step 1: Open Firebase Authentication Console
Click this link or copy it to your browser:
https://console.firebase.google.com/project/latihan-jawara/authentication

### Step 2: Enable Google Sign-In
1. Click on **"Get Started"** (if first time) OR
2. Click on **"Sign-in method"** tab
3. Find **"Google"** in the list
4. Click on it to enable
5. Toggle **"Enable"** to ON
6. Enter a **project support email** (your email)
7. Click **"Save"**

### Step 3: Test Your App
Open: https://latihan-jawara.web.app
- Click "Login Google" button
- Sign in with your Google account
- Your progress will sync across devices.

---

## What's Already Done
- [x] Firebase project created (latihan-jawara)
- [x] Firebase web app created
- [x] Firebase SDK configured in index.html
- [x] Firebase config moved to runtime file ignored by git
- [x] App deployed to Firebase Hosting
- [x] Firestore will auto-create when needed

## What You Need to Do
- [ ] Enable Google Sign-In provider (Step 2 above)
- [ ] Create `public/firebase-config.js` from `public/firebase-config.example.js` using a rotated Firebase web API key.

---

## Firebase Console Links
**Project Overview**: https://console.firebase.google.com/project/latihan-jawara/overview
**Authentication**: https://console.firebase.google.com/project/latihan-jawara/authentication
**Firestore Database**: https://console.firebase.google.com/project/latihan-jawara/firestore
**Hosting**: https://console.firebase.google.com/project/latihan-jawara/hosting

---

## Runtime Firebase Configuration
Create this ignored file before deploying:

```bash
cp public/firebase-config.example.js public/firebase-config.js
```

Then edit `public/firebase-config.js` and paste the rotated Firebase web API key.

---

## Live App URL
**https://latihan-jawara.web.app**
