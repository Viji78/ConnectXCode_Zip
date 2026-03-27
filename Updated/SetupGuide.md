# Learn & Chat - Setup Guide

## Prerequisites

Install these on the new device before starting:

1. **Node.js** (v18 or later) - https://nodejs.org
2. **Yarn** - `npm install -g yarn`
3. **Expo CLI** - `npm install -g expo-cli eas-cli`
4. **Git** (optional) - https://git-scm.com

### For Android
- Android Studio (for emulator) - https://developer.android.com/studio
- OR Expo Go app on physical Android device - https://play.google.com/store/apps/details?id=host.exp.exponent

### For iOS (Mac only)
- Xcode from App Store
- OR Expo Go app on physical iPhone - https://apps.apple.com/app/expo-go/id982107779

---

## Step-by-Step Setup

### 1. Extract the zip
```bash
unzip LearnChatAdminNotification.zip -d LearnChatApp
cd LearnChatApp
```

### 2. Install dependencies
```bash
yarn install
```

### 3. Verify Firebase config
Check `firebase.config.ts` has the correct Firebase credentials. If you need to update them:
- Go to https://console.firebase.google.com
- Select your project
- Go to Project Settings > General > Your apps
- Copy the config values

### 4. Verify `google-services.json` (Android)
- This file should be in the project root
- Download from Firebase Console > Project Settings > Android app

---

## Running the App

### Run in Expo Go (quick testing)
```bash
npx expo start --go
```
- Scan the QR code with Expo Go app on your phone
- Note: Some features (crop UI theme, notifications) have limitations in Expo Go

### Run on Android emulator
```bash
yarn android
```

### Run on iOS simulator (Mac only)
```bash
yarn ios
```

---

## Building APK (Android)

### 1. Login to EAS
```bash
eas login
```

### 2. Build APK
```bash
eas build --profile preview --platform android
```

### 3. Build production AAB (for Play Store)
```bash
eas build --profile production --platform android
```

After build completes, EAS gives you a download link for the APK/AAB.

---

## Important Files to Check

| File | Purpose |
|------|---------|
| `firebase.config.ts` | Firebase connection credentials |
| `google-services.json` | Android Firebase config |
| `app.json` | App name, package ID, permissions, plugins |
| `eas.json` | Build profiles (preview/production) |

---

## Common Issues & Fixes

### "No development build installed"
```bash
npx expo start --go
```
This forces Expo Go mode instead of looking for a dev build.

### Yarn install fails
```bash
rm -rf node_modules
rm yarn.lock
yarn install
```

### Metro bundler cache issues
```bash
npx expo start --clear
```

### Firebase errors
- Check `firebase.config.ts` has correct API keys
- Ensure Firestore rules allow read/write
- Ensure Authentication is enabled in Firebase Console

### Build fails on EAS
- Run `eas whoami` to check you're logged in
- Run `eas build:configure` to reconfigure if needed
- Check `app.json` has correct `package` name under `android`

---

## Tech Stack

- **React Native** 0.81 + **Expo** SDK 54
- **Firebase** (Firestore + Auth)
- **TypeScript**
- **React Navigation** (Stack + Drawer)

---

## Project Structure

```
src/
  components/    - Reusable UI components
  screens/       - App screens
  services/      - Firebase service functions
  styles/        - Shared styles
  types/         - TypeScript types
  data/          - Static data
```
