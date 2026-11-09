# Photo AI Pro — Android starter project

This starter contains:
- Android app (Kotlin + Jetpack Compose): select a photo, send it to your backend, preview the enhanced result.
- FastAPI backend: securely stores the Stability AI API key on the server and calls Stability's ESRGAN upscaler.
- No API key is embedded in the Android APK.

## Requirements
- Android Studio (current stable), JDK 17, Android SDK 35
- Python 3.10+
- A Stability AI API key with API access

## 1. Run the backend
```bash
cd backend
python -m venv .venv
# Windows: .venv\Scripts\activate
# macOS/Linux: source .venv/bin/activate
pip install -r requirements.txt
```
Set your key as an environment variable:
```bash
# Windows PowerShell
$env:STABILITY_API_KEY="YOUR_KEY"
# macOS/Linux
export STABILITY_API_KEY="YOUR_KEY"
```
Then:
```bash
uvicorn main:app --host 0.0.0.0 --port 8000
```

For a physical Android phone, `BASE_URL` in `app/build.gradle.kts` must point to a publicly reachable HTTPS backend URL. `10.0.2.2` works only for the Android emulator when the backend runs on the same computer. Do not expose a development server publicly without HTTPS, authentication, rate limits, and upload limits.

## 2. Open Android app
Open this folder in Android Studio and let Gradle sync. Set `BASE_URL` in `app/build.gradle.kts` to your backend URL, then build:
**Build > Build Bundle(s) / APK(s) > Build APK(s)**

## Important
- The Stability API's documented ESRGAN endpoint returns a 2x upscale and has a maximum output pixel count of 4,194,304.
- API usage may incur charges. Check current pricing and terms before public release.
- This is a starter/MVP source project, not a compiled or signed APK.
- Before publishing, add user authentication, abuse protection, privacy policy, image retention/deletion rules, and a production backend deployment.
