# ORBIT Android

Android Studio project archive for ORBIT, a compact floating AI assistant.

## Repository contents

The Android Studio project is currently stored in `ORBIT-Android-Project.zip`. Extract it and open the `ORBIT` folder in Android Studio.

## Build

The GitHub Actions workflow **ORBIT Android CI** installs JDK 17, Android SDK 35 and Gradle 8.9, unpacks the project, runs unit tests, builds a Debug APK and uploads the APK as a workflow artifact.

Open **Actions → ORBIT Android CI → latest run → Artifacts** to download the Debug APK (after a successful build).

## Current feature scope

- Floating assistant bubble and compact overlay.
- Gemini multimodal API integration (text and a user-selected screen/image snapshot).
- Voice input via Android SpeechRecognizer and spoken response via Android TextToSpeech.
- API key stored locally with AndroidX encrypted preferences.
- Network/API error messages.
- Screen capture only after the Android system consent dialog.

## Important

A single screen snapshot is not continuous video understanding. Screen capture is user-triggered and can be blocked by secure apps. Gemini access requires a valid API key and an internet connection. Never commit API keys, keystores or personal data.

The source archive is not artificially padded. APK size is determined by compiled code, resources and dependencies.
