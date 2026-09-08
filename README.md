# DualCall (Android - Kotlin & Jetpack Compose)

A clean, fast, and modern Android dialer application built with **Kotlin**, **Jetpack Compose**, and **Material 3**.

## Architecture & Features

The app is structured into four independent modules/packages:

1. **Dial Pad (`ui/screens/dialpad`)**:
   - Numeric dialer with DTMF audio feedback and alphanumeric labels.
   - Live phone number input with backspace and clear all on long press.
   - Dual Call Buttons:
     - **SIM Call**: Triggers native Android telephony via `Intent.ACTION_CALL` or `Intent.ACTION_DIAL`.
     - **Brilliant Call**: Decoupled call trigger invoking the `BrilliantCallService` interface.
2. **Call History (`ui/screens/history`)**:
   - Queries `android.provider.CallLog.Calls` with fallback cache.
   - Filter by All Calls and Missed Calls.
   - Displays caller identity, timestamp, call type, duration, and one-tap redial via SIM or Brilliant.
3. **Contacts (`ui/screens/contacts`)**:
   - Queries `android.provider.ContactsContract.CommonDataKinds.Phone`.
   - Real-time search by name or phone number.
   - Direct call actions for both SIM and Brilliant.
4. **Brilliant Call Integration (`brilliant/`)**:
   - `BrilliantCallService`: Interface defining `initiateCall(destinationNumber, options)`, `getStatus()`, `isReady()`, `endCall()`.
   - `BrilliantCallPlaceholderService`: Clean placeholder implementation returning `BrilliantCallResult.NotConfigured` without faking or simulating a call.
   - Ready for drop-in replacement with a real Brilliant Calling SDK or REST/WebRTC gateway.

## Permissions

Configured in `AndroidManifest.xml` and requested at runtime:
- `android.permission.CALL_PHONE`
- `android.permission.READ_PHONE_STATE`
- `android.permission.READ_CONTACTS`
- `android.permission.READ_CALL_LOG`
- `android.permission.INTERNET`

## How to Build in Android Studio

1. Open Android Studio (Hedgehog, Iguana, Jellyfish, or newer).
2. Select **Open an Existing Project** and choose the `android/` directory.
3. Sync Project with Gradle Files.
4. Connect your Android device or start an emulator running Android 8.0+ (API 26+).
5. Click **Run 'app'**.
