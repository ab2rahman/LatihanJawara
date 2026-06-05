# Firebase Firestore Permissions Fix

## 🔒 ERROR: Missing or insufficient permissions

This error means Firebase Firestore security rules are blocking the app from reading/writing data.

---

## 🔧 QUICK FIX (5 minutes)

### Step 1: Open Firestore Rules

**Direct Link:** https://console.firebase.google.com/project/latihan-jawara/firestore/rules

**Or navigate:**
1. Go to: https://console.firebase.google.com/project/latihan-jawara/overview
2. Click "Firestore Database" in left menu
3. Click "Rules" tab

### Step 2: Update Security Rules

**Choose ONE of the options below:**

---

### Option A: Production Rules (Recommended)

**Use this for secure, authenticated access:**

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    // Allow authenticated users to access their own data
    match /studentProgress/{userId} {
      allow read, write: if request.auth != null;
    }
  }
}
```

**What this does:**
- ✅ Allows logged-in users to read/write data
- ✅ Secure - requires authentication
- ✅ Good for production use

**Publish the rules:**
1. Replace everything in the rules editor with the code above
2. Click "Publish" button
3. Wait for "Rules published successfully" message

---

### Option B: Test Mode (For Development)

**Use this for easy testing (NOT for production):**

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if true;
    }
  }
}
```

**What this does:**
- ✅ Allows ANYONE to read/write (no authentication required)
- ⚠️ NOT secure - use only for testing
- ⚠️ Must change to secure rules before production

**Publish the rules:**
1. Replace everything in the rules editor with the code above
2. Click "Publish" button
3. Wait for confirmation

---

## ✅ Verify Fix

After publishing rules:

1. **Refresh the app:**
   - Go to: https://latihan-jawara.web.app
   - Hard refresh: Ctrl+Shift+R (Windows) or Cmd+Shift+R (Mac)

2. **Check browser console (F12):**
   - Should NO LONGER see "Missing or insufficient permissions"
   - Should see: "Data siswa dimuat dari Firebase" or similar

3. **Test the app:**
   - Login with Google
   - Answer some questions
   - Check Firestore Console → should see your data!

---

## 🔍 How to Check Current Rules

**In Firebase Console:**
1. Go to Firestore → Rules tab
2. Look at the current rules
3. If you see `allow read, write: if false;` → This is the problem!
4. Replace with one of the options above

---

## 📋 Rules Comparison

| Rule Type | Secure? | Auth Required | Best For |
|-----------|---------|---------------|-----------|
| **Production Rules** | ✅ Yes | ✅ Yes | Live app with real users |
| **Test Mode** | ❌ No | ❌ No | Development & testing only |
| **Default Rules** | ❌ No | ❌ No | Blocks everything (causes your error) |

---

## 🎯 Recommended Workflow

### For Development (Now):
```javascript
allow read, write: if true;  // Easy testing
```

### For Production (Later):
```javascript
allow read, write: if request.auth != null;  // Secure
```

### For Extra Security (Advanced):
```javascript
allow read, write: if request.auth != null
                  && request.auth.token.email == userId;
// Users can ONLY access their own data by email
```

---

## 🆘 Still Getting Errors?

### Error: "Missing or insufficient permissions"
**Solution:**
- Make sure you clicked "Publish" after changing rules
- Wait 1-2 minutes for rules to propagate
- Hard refresh the app (Ctrl+Shift+R)

### Error: "FirebaseError: Permission denied"
**Solution:**
- Check that you're logged in to the app
- Verify Google Sign-In is enabled in Firebase Console
- Try using Test Mode rules first

### Error: "Firestore has not been created"
**Solution:**
- Go to Firestore Console
- Click "Create database"
- Choose "Start in test mode"
- Select your region
- Then update rules as above

---

## 🔗 Quick Links

| Task | Link |
|------|------|
| **Firestore Rules** | https://console.firebase.google.com/project/latihan-jawara/firestore/rules |
| **Firestore Data** | https://console.firebase.google.com/project/latihan-jawara/firestore/data |
| **Firebase Console** | https://console.firebase.google.com/project/latihan-jawara/overview |
| **Authentication** | https://console.firebase.google.com/project/latihan-jawara/authentication |
| **Live App** | https://latihan-jawara.web.app |

---

## 📊 Current Status

- ✅ Firebase project: `latihan-jawara`
- ✅ Firestore database: Created
- ❌ Security rules: Blocking access (needs fix)
- ⏳ Google Sign-In: Needs to be enabled

**Next steps:**
1. Update Firestore rules (above)
2. Enable Google Sign-In in Authentication
3. Test the app
4. Verify data in Firestore Console

---

**Last Updated:** 2025-06-18
**Project:** LatihanJawara (latihan-jawara)
