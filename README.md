# Real-Time Edge Detection Viewer

This project demonstrates real-time camera edge detection using Android (Java + JNI + OpenCV + OpenGL ES) and a minimal TypeScript web viewer. Frames are captured natively on Android, processed using OpenCV (C++ via JNI), rendered via OpenGL, and can be previewed on a simple web viewer.

---

## Features Implemented

**Android App:**
- Live camera feed preview using TextureView
- Real-time frame processing via OpenCV (C++) using JNI bridge
- Canny edge detector and grayscale filters
- Output rendering with OpenGL ES 2.0 (targeting 10-15 FPS)
- Toggle between raw and processed views
- FPS display

**Web Viewer:**
- Minimal TypeScript and HTML viewer for displaying processed frames (static or dummy images)
- Displays frame statistics such as FPS and resolution
- Demonstrates the ability to bridge native processing results to a web interface

---

## Screenshots and Demo

Include screenshots or GIFs showing:
- Android app running raw and edge-detected camera feed
- Web viewer displaying processed frames and statistics

---

## Setup Instructions

### Android App

1. Requirements:
   - Android SDK
   - Android NDK (tested with NDK r25 or later)
   - OpenCV Android SDK (available at https://opencv.org/releases/)

2. Installing Dependencies:
   - Extract OpenCV SDK
   - Place required OpenCV native libraries from `sdk/native/libs` into `app/src/main/jniLibs`
   - Copy OpenCV Java SDK files to `app/libs` and reference them in `build.gradle`

3. Build Process:
   - Configure `local.properties` with paths for your SDK and NDK
   - Run Gradle build with:
     ```
     ./gradlew assembleDebug
     ```
   - Install the APK on your device via:
     ```
     adb install app/build/outputs/apk/debug/app-debug.apk
     ```

4. Running:
   - Grant camera permission to the app
   - Use the toggle to switch between raw and edge-detected views
   - Observe FPS and OpenGL rendered output

### Web Viewer

1. Requirements:
   - Node.js version 22 or higher
   - npm version 10 or higher

2. Installation and Running:
cd web
npm install
npm run build
npx serve .

- Open `http://localhost:5000` in a browser to view the demo

---

## Architecture Overview

- **app/**: Contains Android Java/Kotlin code managing camera and UI
- **jni/**: Native C++ OpenCV code receiving camera frames via JNI, applying edge detection and other filters
- **gl/**: OpenGL ES renderer for displaying processed frames on Android
- **web/**: TypeScript web viewer displaying sample processed frames with frame statistics, simulating native bridge

The typical frame processing flow:
1. Camera frame is captured in the Android Java/Kotlin layer
2. Frame is sent to native code using JNI
3. Native OpenCV C++ processes the frame (e.g., edge detection)
4. Processed output is rendered using OpenGL ES
5. Optionally, processed images are encoded (e.g., base64) and displayed via the TypeScript web viewer