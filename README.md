# ORBIT — floating AI companion for Android

ORBIT is an Android assistant that stays available as a small movable orb above other apps. Tapping the orb opens a compact black glass-style panel inspired by the supplied visual reference, with a gradient voice ring, prompt field, image attachment, web search and user-approved screen capture.

## Download the source

Download `ORBIT-Android-Project.tar.xz` from the repository root, extract it, and open the extracted `ORBIT` folder in Android Studio.

## Current implementation

- Kotlin + Jetpack Compose Android application (minimum Android 8 / API 26, target API 35).
- Dark premium home screen and custom white ORBIT star mark.
- Movable system overlay bubble and compact bottom panel.
- Foreground notification with an explicit Stop ORBIT action.
- Gemini 3.8 Flash multimodal REST client (text + JPEG image), asynchronous requests, timeouts and readable network/API errors.
- API key stored locally with AndroidX EncryptedSharedPreferences; no key is committed to source control.
- Android SpeechRecognizer for voice input and local TextToSpeech from the overlay service for spoken answers.
- One-shot screen capture using Android's system consent prompt and a MediaProjection foreground service. The frame is resized and attached to the next prompt only.
- Image attachment through the Android document picker.
- Unit tests for network/API error mapping.
- GitHub Actions workflow runs unit tests and builds a Debug APK artifact.

## Important behavior and limitations

- ORBIT does **not** continuously watch or record the screen. The user must tap the screen-analysis button and approve Android's system capture dialog. Only one frame is captured and attached to the next message.
- A single frame cannot provide a full understanding of a video's earlier/later frames or audio. The assistant is instructed not to claim otherwise.
- Android secure windows and some streaming apps can block screen capture; protected content may appear black.
- Speech recognition availability and language support depend on the device's installed speech services. Android TextToSpeech uses the device's selected/default voice.
- Gemini requests require internet and a valid Gemini API key. Free-tier quota and availability are controlled by Google and can change.
- A client-side API key is suitable for a personal prototype only. A public production release should route requests through a secured backend with rate limits and abuse protection.

## Build locally

Requirements: Android Studio, JDK 17, Android SDK Platform 35, and Gradle 8.9.

1. Extract `ORBIT-Android-Project.tar.xz`.
2. Open the extracted `ORBIT` folder in Android Studio and sync Gradle.
3. Build with `gradle --no-daemon testDebugUnitTest assembleDebug` or use **Build → Build APK(s)**.
4. Install `app/build/outputs/apk/debug/app-debug.apk` on a test phone.
5. Open ORBIT and add your Gemini API key from Google AI Studio.
6. Grant **Display over other apps** permission and start the floating assistant.
7. Tap the image/screen button and approve Android's screen-capture dialog before asking about the displayed content.
8. Tap the microphone button and grant microphone permission when prompted.

## GitHub Actions

Every push or pull request to `main` runs unit tests and builds the Debug APK. Open **Actions → ORBIT Android CI → latest successful run → Artifacts** and download `ORBIT-debug-apk-and-test-reports`.

The repository intentionally does not contain a prebuilt APK, signing key, API key, or fake binary padding. APK size is determined by the actual compiled app and dependencies; source archive size is not a quality metric.

## Security

Never commit a Gemini API key, signing keystore, `local.properties`, or personal test data. Before publishing ORBIT publicly, move Gemini requests to a backend so a distributed APK cannot expose a reusable provider key.

## License

MIT — see [LICENSE](LICENSE).
