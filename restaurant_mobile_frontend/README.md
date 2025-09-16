# restaurant_mobile_frontend

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

---

## Configuration

This app requires environment configuration and third-party integrations for Google OAuth and PayHere. Follow the steps below.

### 1) Environment variables (.env)

- Copy .env.example to .env in the project root:
  - Linux/macOS: `cp .env.example .env`
  - Windows: `copy .env.example .env`
- Fill the variables with your values:
  - API_BASE_URL: Base URL of your backend REST API (e.g., `https://api.myrestaurant.com` or `http://10.0.2.2:8000` for Android emulator).
  - GOOGLE_WEB_CLIENT_ID: Google OAuth 2.0 Web Client ID.
  - PAYHERE_MERCHANT_ID: Your PayHere Merchant ID.
  - PAYHERE_NOTIFY_URL: Public notify URL endpoint that receives payment status updates from PayHere.
  - PAYHERE_MODE: `sandbox` for testing, `live` for production.

Note: `.env` is already included in pubspec assets and will be bundled automatically.

### 2) Google OAuth (Google Sign-In)

a) Create/Select a Google Cloud project and enable OAuth:
- Go to Google Cloud Console (or Firebase Console if you prefer).
- Enable "Google Sign-In" / "Google Identity Services".
- Create OAuth 2.0 credentials:
  - Web client ID (copy to `GOOGLE_WEB_CLIENT_ID` in `.env`).
  - Android client ID is typically auto-configured via SHA-1 fingerprints, but the Web client ID may be required for ID token verification in backends.

b) Add SHA-1 certificate fingerprints for Android:
- For debug builds, generate SHA-1 from your debug keystore:
  ```
  keytool -list -v -alias androiddebugkey -keystore ~/.android/debug.keystore -storepass android -keypass android
  ```
- Add the SHA-1 to the OAuth consent screen / credentials as needed (or to Firebase project settings → Your app → Add fingerprint).
- Ensure the Android package name matches your appId in `android/app/build.gradle.kts` (default: `com.example.restaurant_mobile_frontend`).

c) Update your backend (if applicable) to verify Google ID tokens against your Web client ID.

### 3) PayHere Setup

a) Create a PayHere merchant account:
- For testing, use the Sandbox environment; for production, use Live environment.

b) Collect values and configure:
- PAYHERE_MERCHANT_ID: from PayHere dashboard.
- PAYHERE_NOTIFY_URL: public endpoint on your backend to receive payment notifications (HTTP POST callbacks).
- PAYHERE_MODE: `sandbox` while testing; switch to `live` for production.

c) Backend considerations:
- Ensure your notify URL is reachable over the public internet (e.g., https://api.myrestaurant.com/payments/payhere/notify).
- Verify signatures and transaction status per PayHere’s documentation.

### 4) Install dependencies and run

- Fetch packages:
  ```
  flutter pub get
  ```
- Run on Android:
  ```
  flutter run
  ```

Note: INTERNET permission is enabled for both debug/profile and release builds (AndroidManifest updated).

---
