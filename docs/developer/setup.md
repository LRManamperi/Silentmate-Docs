# Development Setup

This guide will help you set up your development environment for contributing to Silent Mate.

## Prerequisites

### Required Software

1. **Android Studio**
   - Version: Arctic Fox (2020.3.1) or later
   - Recommended: Latest stable version
   - Download: [developer.android.com/studio](https://developer.android.com/studio)

2. **Java Development Kit (JDK)**
   - Version: JDK 11 or JDK 17
   - Recommended: JDK 17 (for latest Android features)
   - Download: [Oracle JDK](https://www.oracle.com/java/technologies/downloads/) or [OpenJDK](https://openjdk.org/)

3. **Android SDK**
   - Minimum SDK: API 21 (Android 5.0 Lollipop)
   - Target SDK: API 34 (Android 14)
   - Compile SDK: API 34
   - Installed via Android Studio

4. **Git**
   - Version: 2.0 or later
   - Download: [git-scm.com](https://git-scm.com/)

### System Requirements

**Minimum:**
- OS: Windows 10, macOS 10.14, or Linux (Ubuntu 18.04+)
- RAM: 8 GB
- Disk Space: 4 GB (IDE) + 2 GB (Android SDK)
- Screen Resolution: 1280 x 800

**Recommended:**
- RAM: 16 GB or more
- Disk Space: 8 GB+ free
- SSD for faster builds
- Screen Resolution: 1920 x 1080 or higher

---

## Getting Started

### Step 1: Clone the Repository

```bash
# Clone the repository
git clone https://github.com/yourusername/silent-mate.git

# Navigate to project directory
cd silent-mate
```

### Step 2: Open in Android Studio

1. Launch Android Studio
2. Click **"Open an Existing Project"**
3. Navigate to the `silent-mate` directory
4. Click **"OK"**

Android Studio will:
- Index the project
- Download required dependencies
- Sync Gradle files
- Set up build configuration

**Initial sync may take 5-10 minutes depending on your internet speed.**

### Step 3: Configure Android SDK

If prompted, Android Studio will ask to install missing SDK components:

1. Click **"Install missing platforms"** if prompted
2. Accept licenses
3. Wait for download and installation

**Manual SDK Configuration:**
1. File → Settings (or Android Studio → Preferences on macOS)
2. Appearance & Behavior → System Settings → Android SDK
3. SDK Platforms tab: Ensure API 21-34 are installed
4. SDK Tools tab: Ensure these are installed:
   - Android SDK Build-Tools
   - Android SDK Platform-Tools
   - Android Emulator
   - Google Play Services

---

## Project Structure

```
silent-mate/
├── app/                          # Main application module
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/example/silentmate/
│   │   │   │   ├── MainActivity.kt
│   │   │   │   ├── BaseActivity.kt
│   │   │   │   ├── HomeFragment.kt
│   │   │   │   ├── SensorFragment.kt
│   │   │   │   ├── SettingsFragment.kt
│   │   │   │   ├── SilentMateSensorManager.kt
│   │   │   │   └── TutorialDialogFragment.kt
│   │   │   ├── res/              # Resources
│   │   │   │   ├── layout/       # XML layouts
│   │   │   │   ├── values/       # Colors, strings, themes
│   │   │   │   ├── drawable/     # Images and icons
│   │   │   │   └── mipmap/       # App icons
│   │   │   └── AndroidManifest.xml
│   │   ├── test/                 # Unit tests
│   │   └── androidTest/          # Instrumented tests
│   └── build.gradle.kts          # App-level Gradle config
├── gradle/                       # Gradle wrapper
├── build.gradle.kts              # Project-level Gradle config
├── settings.gradle.kts           # Gradle settings
├── gradle.properties             # Gradle properties
└── local.properties              # Local SDK path (not in git)
```

---

## Build Configuration

### Gradle Files

**Project-level `build.gradle.kts`:**
```kotlin
plugins {
    id("com.android.application") version "8.1.0" apply false
    id("org.jetbrains.kotlin.android") version "1.9.0" apply false
}
```

**App-level `build.gradle.kts`:**
```kotlin
plugins {
    id("com.android.application")
    id("org.jetbrains.kotlin.android")
}

android {
    namespace = "com.example.silentmate"
    compileSdk = 34

    defaultConfig {
        applicationId = "com.example.silentmate"
        minSdk = 21
        targetSdk = 34
        versionCode = 1
        versionName = "1.0"

        testInstrumentationRunner = "androidx.test.runner.AndroidJUnitRunner"
    }

    buildTypes {
        release {
            isMinifyEnabled = true
            proguardFiles(
                getDefaultProguardFile("proguard-android-optimize.txt"),
                "proguard-rules.pro"
            )
        }
        debug {
            isMinifyEnabled = false
        }
    }

    compileOptions {
        sourceCompatibility = JavaVersion.VERSION_17
        targetCompatibility = JavaVersion.VERSION_17
    }

    kotlinOptions {
        jvmTarget = "17"
    }

    buildFeatures {
        viewBinding = true
    }
}

dependencies {
    // AndroidX Core
    implementation("androidx.core:core-ktx:1.12.0")
    implementation("androidx.appcompat:appcompat:1.6.1")
    implementation("androidx.constraintlayout:constraintlayout:2.1.4")
    implementation("androidx.fragment:fragment-ktx:1.6.2")
    
    // Material Design
    implementation("com.google.android.material:material:1.11.0")
    
    // Lifecycle
    implementation("androidx.lifecycle:lifecycle-runtime-ktx:2.7.0")
    
    // Testing
    testImplementation("junit:junit:4.13.2")
    androidTestImplementation("androidx.test.ext:junit:1.1.5")
    androidTestImplementation("androidx.test.espresso:espresso-core:3.5.1")
}
```

---

## Building the Project

### Using Android Studio

**Debug Build:**
1. Build → Make Project (Ctrl+F9 / Cmd+F9)
2. Build → Build Bundle(s) / APK(s) → Build APK(s)
3. APK location: `app/build/outputs/apk/debug/`

**Release Build:**
1. Build → Generate Signed Bundle / APK
2. Select APK or Bundle
3. Configure signing (see Signing section below)
4. Select release build variant
5. Click Finish

### Using Gradle Command Line

**Debug Build:**
```bash
# Build debug APK
./gradlew assembleDebug

# Output: app/build/outputs/apk/debug/app-debug.apk
```

**Release Build:**
```bash
# Build release APK (unsigned)
./gradlew assembleRelease

# Output: app/build/outputs/apk/release/app-release-unsigned.apk
```

**Clean Build:**
```bash
# Clean previous builds
./gradlew clean

# Clean and build
./gradlew clean assembleDebug
```

**Install on Device:**
```bash
# Install debug build
./gradlew installDebug

# Uninstall
./gradlew uninstallDebug
```

---

## Running the App

### Using Android Studio

1. Connect Android device via USB (with USB Debugging enabled)
   - OR -
   Start Android Emulator (see Emulator Setup below)

2. Select device from device dropdown (top toolbar)

3. Click **Run** button (Shift+F10 / Ctrl+R)

### Using ADB Command Line

```bash
# Install APK on connected device
adb install app/build/outputs/apk/debug/app-debug.apk

# Launch app
adb shell am start -n com.example.silentmate/.MainActivity

# View logs
adb logcat | grep SilentMate
```

---

## Emulator Setup

### Creating an AVD (Android Virtual Device)

1. Tools → Device Manager (or AVD Manager)
2. Click **"Create Device"**
3. Select hardware profile:
   - Recommended: Pixel 6 (1080 x 2400, 411 dpi)
4. Select system image:
   - Recommended: Android 13 (API 33) or Android 14 (API 34)
   - Download if not already installed
5. Configure AVD:
   - Name: e.g., "Pixel_6_API_33"
   - Startup orientation: Portrait
   - Enable hardware acceleration (HAXM/KVM)
6. Click **"Finish"**

### Emulator Configuration

**Enable sensors in emulator:**
1. Run emulator
2. Click **"..." (Extended Controls)** on emulator toolbar
3. Go to **"Virtual sensors"**
4. Test accelerometer, gyroscope, proximity

**Note:** Proximity sensor may not work reliably in emulator. Physical device testing is recommended.

---

## Testing on Physical Device

### Enable Developer Options

**Android 11+:**
1. Settings → About Phone
2. Tap "Build Number" 7 times
3. Enter PIN/password if prompted
4. "Developer options" now appears in Settings

### Enable USB Debugging

1. Settings → System → Developer Options
2. Toggle **"USB debugging"** ON
3. Connect device via USB
4. Allow USB debugging when prompted

### Verify Connection

```bash
# List connected devices
adb devices

# Should show:
# List of devices attached
# <device-id>    device
```

---

## IDE Configuration

### Recommended Android Studio Settings

**Code Style:**
1. File → Settings → Editor → Code Style → Kotlin
2. Set from: Kotlin style guide
3. Apply and OK

**Inspections:**
1. File → Settings → Editor → Inspections
2. Enable: Kotlin → Probable bugs
3. Enable: Android → Lint

**Version Control:**
1. File → Settings → Version Control → Git
2. Set Git executable path
3. Enable: "Use credential helper"

**Logcat Colors:**
1. File → Settings → Editor → Color Scheme → Android Logcat
2. Customize colors for ERROR, WARN, INFO, DEBUG

---

## Troubleshooting Setup Issues

### Issue: Gradle Sync Failed

**Solution:**
```bash
# Clean Gradle cache
./gradlew clean

# Invalidate caches
File → Invalidate Caches / Restart → Invalidate and Restart
```

### Issue: SDK Not Found

**Solution:**
1. Create `local.properties` in project root:
   ```
   sdk.dir=/path/to/Android/Sdk
   ```
2. Or set in Android Studio:
   - File → Project Structure → SDK Location

### Issue: Build Takes Too Long

**Solution:**
Add to `gradle.properties`:
```properties
org.gradle.jvmargs=-Xmx4096m -XX:MaxMetaspaceSize=1024m
org.gradle.parallel=true
org.gradle.caching=true
```

### Issue: Emulator Won't Start

**Solution:**
- Check virtualization is enabled in BIOS
- Install HAXM (Windows) or KVM (Linux)
- Allocate more RAM to emulator (2GB minimum)

---

## Code Style Guidelines

### Kotlin Style

```kotlin
// Use camelCase for variables and functions
val sensorManager = context.getSystemService(Context.SENSOR_SERVICE)

// Use PascalCase for classes
class SilentMateSensorManager

// Use UPPER_SNAKE_CASE for constants
const val PROXIMITY_THRESHOLD = 5.0f

// Prefer expression bodies for simple functions
fun isEnabled(): Boolean = sharedPreferences.getBoolean("enabled", false)

// Use explicit types when not obvious
val position: DevicePosition = detectPosition()
```

### Documentation

```kotlin
/**
 * Detects the current device position based on sensor data.
 *
 * @return The detected position: UPSIDE_DOWN, IN_POCKET, IN_HAND, or UNKNOWN
 */
private fun detectDevicePosition(): DevicePosition {
    // Implementation
}
```

---

## Git Workflow

### Branch Naming

```bash
# Features
git checkout -b feature/event-scheduling

# Bug fixes
git checkout -b fix/proximity-detection

# Documentation
git checkout -b docs/api-reference
```

### Commit Messages

```bash
# Format: <type>: <description>

git commit -m "feat: Add event scheduling feature"
git commit -m "fix: Improve proximity sensor detection"
git commit -m "docs: Update API reference"
git commit -m "refactor: Extract sensor logic to separate class"
```

---

## Next Steps

Now that your environment is set up:

1. ✅ **Read Architecture** - Understand system design
2. ✅ **Review Code** - Familiarize yourself with codebase
3. ✅ **Run Tests** - Ensure everything works
4. ✅ **Make Changes** - Start contributing!
5. ✅ **Submit PR** - Follow contribution guidelines

**Happy coding! 🚀**

---

**Next:** [Building](building.md) for detailed build instructions