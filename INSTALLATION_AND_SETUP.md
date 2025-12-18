# HeartChat - Complete Installation & Setup Guide

## 🚀 Quick Start (3 Steps to Running the App)

### Step 1: Clone the Repository

```bash
git clone https://github.com/Sanskar0108/heartchat.git
cd heartchat
```

### Step 2: Install Dependencies

```bash
flutter pub get
```

### Step 3: Run the App

```bash
flutter run
```

---

## ✅ Prerequisites

Before you start, make sure you have:

- **Flutter SDK** (3.0+) - [Download here](https://flutter.dev/docs/get-started/install)
- **Dart** (3.0+) - Included with Flutter
- **Android Studio** - [Download here](https://developer.android.com/studio)
- **Java Development Kit (JDK)** 11+
- **Android Emulator** or **Physical Android Device**
- **Firebase Account** - [Create here](https://firebase.google.com)
- **Git** - [Download here](https://git-scm.com)

### Verify Installation

```bash
flutter --version
dart --version
```

---

## 📝 Firebase Setup (IMPORTANT!)

This is **CRITICAL** - the app won't run without Firebase!

### 1. Create Firebase Project

1. Go to [Firebase Console](https://firebase.google.com/console)
2. Click "Create a new project"
3. Name it `heartchat`
4. Enable Google Analytics (optional)
5. Click "Create project"
6. Wait for project creation to complete

### 2. Enable Authentication

1. In Firebase Console → Build → Authentication
2. Click "Get Started"
3. Choose "Email/Password" provider
4. Click "Enable" and save

### 3. Create Firestore Database

1. In Firebase Console → Build → Firestore Database
2. Click "Create database"
3. Choose "Start in production mode"
4. Select region: `asia-south1` (or closest to you)
5. Click "Create"

### 4. Set Up Cloud Storage

1. In Firebase Console → Build → Storage
2. Click "Get Started"
3. Choose "Start in production mode"
4. Select same region: `asia-south1`
5. Click "Done"

### 5. Get Google Services Configuration

1. In Firebase Console → Project Settings (⚙️ icon top-right)
2. Go to "Your apps" section
3. Click "Android" icon to add Android app
4. Package name: `com.heartchat.app`
5. App nickname: `HeartChat Android`
6. SHA-1 Certificate: Leave blank for now (optional for development)
7. Click "Register app"
8. Click "Download google-services.json"
9. **IMPORTANT**: Place this file in `android/app/google-services.json`

---

## 🔧 Android Studio Setup

### Open Project in Android Studio

1. Open Android Studio
2. File → Open → Navigate to `heartchat` folder
3. Select the folder and click "OK"
4. Android Studio will auto-detect it as a Flutter project
5. Wait for Gradle sync to complete (1-2 minutes)

### Connect Android Device/Emulator

**Option A: Using Android Emulator**
```bash
flutter emulators --launch Pixel_5  # Or your available emulator
```

**Option B: Using Physical Device**
- Enable "Developer Mode" on your Android device
- Connect via USB
- Allow USB Debugging when prompted
- Verify connection:
```bash
adb devices
```

### Run the App

```bash
flutter run
```

Or in Android Studio:
- Click the green **Run** button (▶️) at the top
- Or press `F5`

---

## 🏗️ Project Structure

The app will be organized as follows after first run:

```
heartchat/
├── android/                    # Android-specific code
│   └── app/
│       └── google-services.json # Firebase config (YOU NEED TO ADD THIS)
├── ios/                        # iOS-specific code
├── lib/                        # Main Dart code
│   ├── main.dart              # Entry point
│   ├── models/                # Data models
│   ├── screens/               # UI screens
│   ├── services/              # Business logic
│   ├── widgets/               # Reusable UI components
│   └── utils/                 # Utilities & themes
├── test/                       # Unit & widget tests
├── pubspec.yaml               # Dependencies
├── README.md                  # Documentation
└── .gitignore                 # Git ignore rules
```

---

## 🎨 First Launch Experience

When you first run the app:

1. **Splash Screen** - Loading screen with HeartChat logo
2. **Login/Signup Screen** - Create your account
3. **Main Chat Screen** - Empty initially (waiting for partner)
4. **Settings** - Choose your theme and enable biometric lock

---

## 🔐 Firestore Security Rules

After creating Firestore, you MUST add security rules:

1. Go to Firebase Console → Firestore → Rules tab
2. Replace all content with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth.uid == userId;
    }
    match /messages/{messageId} {
      allow read, write: if request.auth.uid == resource.data.senderId || request.auth.uid == resource.data.receiverId;
    }
    match /notes/{noteId} {
      allow read, write: if request.auth.uid in resource.data.userIds;
    }
    match /todos/{todoId} {
      allow read, write: if request.auth.uid in resource.data.userIds;
    }
  }
}
```

3. Click "Publish"

---

## 📱 Testing the App

### Sign Up

1. Open app on first device/emulator
2. Click "Sign Up"
3. Enter email (e.g., `user1@heartchat.com`)
4. Enter password (min 6 characters)
5. Enter your name
6. Click "Create Account"

### Add Partner

1. In Settings, find "Add Partner" option
2. Have your partner sign up on another device
3. Exchange unique IDs shown in Settings
4. Add each other
5. Start messaging!

---

## 🐛 Troubleshooting

### `Error: Could not find Android SDK`

```bash
flutter config --android-sdk /path/to/android-sdk
```

### `Gradle sync failed`

```bash
flutter clean
flutter pub get
flutter run
```

### `google-services.json not found`

1. Download from Firebase Console (see Step 5 of Firebase Setup)
2. Place in `android/app/google-services.json`
3. Run `flutter clean && flutter pub get && flutter run`

### `Unable to locate adb`

```bash
flutter doctor --android-licenses
```

Accept all licenses.

### `FirebaseException: [core/invalid-api-key]`

1. Your Firebase configuration is wrong
2. Re-download `google-services.json` from Firebase
3. Replace the file in `android/app/`
4. Run `flutter clean && flutter run`

### App crashes on startup

1. Make sure Firestore Database is created
2. Make sure Storage is enabled
3. Check that `google-services.json` is in the right location
4. Check Firebase Console for any errors in "Logs"

---

## 📊 System Requirements

| Requirement | Minimum | Recommended |
|---|---|---|
| Flutter SDK | 3.0.0 | Latest (3.16+) |
| Dart SDK | 3.0.0 | Latest |
| Android Version | 5.0 (API 21) | 10.0+ (API 29+) |
| RAM | 2GB | 4GB+ |
| Disk Space | 500MB | 2GB+ |
| Internet | Required | Required |

---

## ✨ Next Steps

1. ✅ Clone repository
2. ✅ Set up Firebase
3. ✅ Configure Android Studio
4. ✅ Run on emulator/device
5. Sign up with your email
6. Invite your partner to the app
7. Start messaging securely!

---

## 🆘 Need Help?

- 📖 Check [Flutter Documentation](https://flutter.dev/docs)
- 🔥 Check [Firebase Documentation](https://firebase.google.com/docs)
- 🐛 Open an [Issue on GitHub](https://github.com/Sanskar0108/heartchat/issues)
- 💬 Email: support@heartchat.app

---

**Your love, our priority. Your privacy, our promise. ❤️**
