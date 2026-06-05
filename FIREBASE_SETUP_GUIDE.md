# Firebase Firestore Setup Guide for LatihanJawara

## 🔗 Quick Links

**Firebase Console:** https://console.firebase.google.com/project/latihan-jawara/overview

**Firestore Database:** https://console.firebase.google.com/project/latihan-jawara/firestore

**Authentication:** https://console.firebase.google.com/project/latihan-jawara/authentication

---

## 📊 How Data is Stored

### Database Type: **Firebase Firestore** (Cloud Firestore)

```
📁 Collection: studentProgress
   │
   ├──📄 Document: boss@gmail.com (your email)
   │    ├──👤 profile
   │    │   ├── email: "boss@gmail.com"
   │    │   ├── name: "Muhammad Abdu Ar Rahman"
   │    │   ├── googleName: "Muhammad Abdu Ar Rahman"
   │    │   └── photoURL: "https://..."
   │    │
   │    ├──📈 progress
   │    │   ├── scores: { "Religi::Soal...": 85, ... }
   │    │   ├── answers: { "Religi::Soal...::0": 2, ... }
   │    │   └── essays: { "Religi::Soal...::0": "Jawaban...", ... }
   │    │
   │    └──🕐 updatedAt: "2025-06-18T10:30:45.000Z"
   │
   └──📄 Document: student2@gmail.com
        └── ... (same structure)
```

---

## 🔧 Setup Steps

### Step 1: Create Firestore Database

1. Open Firebase Console: https://console.firebase.google.com/project/latihan-jawara/firestore
2. Click **"Create database"** button
3. Choose **"Start in test mode"** (for development)
   - Allows read/write access for 30 days
   - You can add security rules later
4. Select a location (choose closest to your users):
   - **asia-southeast2** (Jakarta) - Recommended for Indonesia
   - or **asia-southeast1** (Singapore)
5. Click **"Done"**

### Step 2: Verify Firestore is Active

After creation, you should see:
- **Firestore Database** in the left menu
- **"Collection data"** tab (may be empty initially)
- **"Rules"** tab (for security rules)

### Step 3: Enable Google Sign-In (if not done)

1. Go to: https://console.firebase.google.com/project/latihan-jawara/authentication
2. Click **"Sign-in method"** tab
3. Find **"Google"** and enable it
4. Enter your support email
5. Click **"Save"**

---

## 🧪 Testing Data Storage

### Method 1: Use the App (Recommended)

1. Open https://latihan-jawara.web.app
2. Login with Google
3. Answer some questions
4. Check Firestore Console - you should see your data!

### Method 2: Test with Code

Open browser console (F12) and run:

```javascript
// Check if Firebase is ready
console.log('Firebase ready:', firebaseState.ready);
console.log('User:', firebaseState.user);
console.log('Student Doc ID:', studentDocId());
```

---

## 📋 Data Structure Details

### Document ID Format
```
studentProgress/{user_email_lowercase}
```

Example: `studentProgress/boss@gmail.com`

### Data Schema

```json
{
  "profile": {
    "email": "boss@gmail.com",
    "name": "Muhammad Abdu Ar Rahman",
    "googleName": "Muhammad Abdu Ar Rahman",
    "photoURL": "https://lh3.googleusercontent.com/..."
  },
  "progress": {
    "scores": {
      "Religi::Soal Latihan Agama Islam": 85,
      "Math::Membilang Angka 51 - 100": 90
    },
    "answers": {
      "Religi::Soal Latihan Agama Islam::0": 2,
      "Math::Membilang Angka 51 - 100::3": 1
    },
    "essays": {
      "Religi::Soal Latihan Agama Islam::0": "Tuliskan jawaban...",
      "Math::Membilang Angka 51 - 100::5": "Urutan bilangan..."
    }
  },
  "updatedAt": "2025-06-18T10:30:45.000Z"
}
```

---

## 🔍 How to View Data

### In Firebase Console

1. Go to: https://console.firebase.google.com/project/latihan-jawara/firestore
2. Click on **"studentProgress"** collection
3. You'll see all students' documents
4. Click on any document to see:
   - Profile information
   - All scores
   - All quiz answers
   - All essay responses

### Data Updates

Data is updated automatically:
- ✅ When student name is changed
- ✅ After each quiz answer
- ✅ After each essay response
- ✅ Before logout

---

## 📊 When Data is NOT Saved

Data is only saved to Firebase when:
- ✅ User is logged in with Google
- ✅ Firebase is properly configured
- ✅ Firestore database exists

If these conditions aren't met:
- Data is saved to **localStorage** only
- Works offline
- Will sync when Firebase becomes available

---

## 🔒 Security Rules (Future)

After testing, update Firestore rules:

```javascript
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /studentProgress/{userId} {
      allow read, write: if request.auth != null
                        && request.auth.token.email == userId;
    }
  }
}
```

This ensures:
- Only authenticated users can access data
- Users can only access their own data
- Uses email as user identifier

---

## 🆘 Troubleshooting

### No data appearing in Firestore?

1. **Check Firestore is created**
   - Go to Firestore console
   - If you see "Create database", create it

2. **Check user is logged in**
   - Look for profile chip in the app
   - Should show name and email

3. **Check browser console**
   - Open F12 Developer Tools
   - Look for Firebase errors

4. **Check Firebase config**
   - Open the app
   - Check sync status message
   - Should say "Firebase belum dikonfigurasi" or "Tersimpan ke Firebase"

### Collection exists but no documents?

- This is normal if no one has used the app yet
- Login and answer some questions
- Data will appear automatically

---

## 📞 Quick Reference

| Task | Link |
|------|------|
| Firebase Console | https://console.firebase.google.com/project/latihan-jawara/overview |
| Firestore Data | https://console.firebase.google.com/project/latihan-jawara/firestore |
| Authentication | https://console.firebase.google.com/project/latihan-jawara/authentication |
| Live App | https://latihan-jawara.web.app |

---

**Project:** latihan-jawara
**Database:** Cloud Firestore
**Collection:** studentProgress
**Last Updated:** 2025-06-18
