# ❤️ HeartChat - Secure Messaging App for Couples

A beautiful, secure, and private messaging application built with Flutter and Firebase. Designed specifically for long-distance couples who value privacy and security.

## Features

✅ **End-to-End Encryption** - All messages are encrypted using AES-256
✅ **Text & Image Sharing** - Send messages and photos securely
✅ **Voice & Video Calls** - Make unlimited encrypted calls
✅ **Shared Notes** - Create and share private notes together
✅ **To-Do Lists** - Collaborative task management
✅ **Biometric Lock** - Fingerprint/Face recognition security
✅ **Multiple Themes** - Romantic, Sunset, Ocean, Forest, Midnight, Cherry themes
✅ **Message Read Receipts** - See when messages are delivered and read
✅ **Auto-Backup** - Automatic encrypted backups
✅ **No Ads or Tracking** - Completely private, no third parties

## Tech Stack

- **Frontend**: Flutter + Dart
- **Backend**: Firebase (Auth, Firestore, Storage, Cloud Messaging)
- **Encryption**: AES-256 for E2E encryption
- **Voice/Video**: Agora SDK
- **UI**: Material Design 3 with custom themes

## Quick Start

### Prerequisites

- Flutter 3.0+
- Dart 3.0+
- Android Studio or VS Code
- Firebase Account

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/Sanskar0108/heartchat.git
cd heartchat
```

2. **Install dependencies**
```bash
flutter pub get
```

3. **Set up Firebase**
   - Go to [Firebase Console](https://firebase.google.com)
   - Create a new project
   - Enable Authentication (Email/Password)
   - Enable Firestore Database
   - Enable Cloud Storage
   - Download `google-services.json` and place in `android/app/`

4. **Update firebase_options.dart**
   - Replace YOUR_API_KEY, YOUR_PROJECT_ID, etc. with your Firebase credentials

5. **Run the app**
```bash
flutter run
```

## Project Structure

```
heartchat/
├── lib/
│   ├── main.dart                 # Entry point
│   ├── firebase_options.dart     # Firebase configuration
│   ├── encryption_service.dart   # E2E encryption
│   ├── models/
│   │   ├── user_model.dart
│   │   ├── message_model.dart
│   │   ├── call_model.dart
│   │   ├── note_model.dart
│   │   └── todo_model.dart
│   ├── screens/
│   │   ├── splash_screen.dart
│   │   ├── login_screen.dart
│   │   ├── signup_screen.dart
│   │   ├── chat_screen.dart
│   │   ├── call_screen.dart
│   │   ├── settings_screen.dart
│   │   ├── notes_screen.dart
│   │   └── todos_screen.dart
│   ├── services/
│   │   ├── auth_service.dart
│   │   ├── firestore_service.dart
│   │   └── call_service.dart
│   ├── widgets/
│   │   ├── chat_bubble.dart
│   │   ├── message_input.dart
│   │   └── theme_selector.dart
│   └── utils/
│       ├── theme.dart
│       ├── constants.dart
│       └── helpers.dart
├── pubspec.yaml                  # Dependencies
├── android/
│   └── app/
│       └── google-services.json  # Firebase config
└── README.md
```

## Security Features

### End-to-End Encryption
- All messages are encrypted on the device before sending
- Only your partner can decrypt and read messages
- Firebase servers never see unencrypted content

### Authentication
- Email/Password signup and login
- Optional biometric authentication (Fingerprint/Face)
- Secure password hashing

### Firebase Security Rules
- Only authenticated users can access their data
- Users can only read/write their own messages
- No cross-user data access

## Firebase Firestore Rules

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
  }
}
```

## Dependencies

Key dependencies used in the project:

```yaml
firebase_core: ^2.24.0
firebase_auth: ^4.14.0
cloud_firestore: ^4.14.0
firebase_storage: ^11.4.0
google_fonts: ^6.1.0
provider: ^6.0.0
image_picker: ^1.0.4
encrypt: ^4.0.5
agora_uikit: ^1.4.3
local_auth: ^2.1.1
```

## Setup for Android Studio

1. Open Android Studio
2. File → Open → Select the `heartchat` folder
3. Android Studio will auto-detect it as a Flutter project
4. Wait for dependencies to sync
5. Connect an Android device or emulator
6. Run → Run (or press F5)

## Usage

### First Time Setup

1. **Sign Up**: Create an account with your email
2. **Verify Email**: Confirm your email address
3. **Add Partner**: Share your unique ID with your partner or search by email
4. **Start Chatting**: Begin your secure conversations!

### Theme Selection

Go to Settings → Themes to choose from 6 beautiful romantic themes:
- 💗 **Romantic** (Pink/Rose)
- 🌅 **Sunset** (Orange/Purple)
- 🌊 **Ocean** (Blue/Teal)
- 🌿 **Forest** (Green/Brown)
- 🌙 **Midnight** (Purple/Black)
- 🍒 **Cherry** (Red/Pink)

## Troubleshooting

### Build Errors

If you encounter build errors:

```bash
# Clean build
flutter clean
flu flutter pub get
flutter run
```

### Firebase Connection Issues

- Ensure `google-services.json` is in the correct location
- Check Firebase project settings match your app
- Verify internet connection

### Missing Dependencies

```bash
flutter pub get
flutter pub upgrade
```

## Privacy & Data

- **No Ads**: We don't show advertisements
- **No Tracking**: We don't track your behavior
- **No Data Selling**: Your data is never sold
- **Encrypted Storage**: All data is encrypted at rest
- **User Control**: Delete your account anytime

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

MIT License - See LICENSE file for details

## Support

Have questions or found a bug?

- Open an issue on GitHub
- Email: support@heartchat.app

## Roadmap

- [ ] Group chats
- [ ] Message reactions
- [ ] Message search
- [ ] File sharing
- [ ] Screen sharing in calls
- [ ] Desktop app (Windows, Mac, Linux)
- [ ] Web version

## Credits

Built with ❤️ for long-distance couples everywhere.

---

**Your love, our priority. Your privacy, our promise.**
