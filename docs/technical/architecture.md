# Architecture

This document describes the technical architecture of Silent Mate.

## Overview

Silent Mate is built using a modular architecture with clear separation of concerns:

```
┌─────────────────────────────────────────┐
│           User Interface Layer          │
│  (Activities, Fragments, ViewBinding)   │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│         Business Logic Layer            │
│    (SilentMateSensorManager)            │
└─────────────────┬───────────────────────┘
                  │
┌─────────────────▼───────────────────────┐
│          System Services Layer          │
│  (SensorManager, AudioManager, etc.)    │
└─────────────────────────────────────────┘
```

## Core Components

### 1. MainActivity

**Purpose:** Main entry point and navigation controller

**Responsibilities:**
- Fragment management and navigation
- Theme application (Dark/Light mode)
- Status bar color management
- Tutorial display on first launch
- Bottom navigation handling

**Key Methods:**
```kotlin
class MainActivity : BaseActivity() {
    private lateinit var binding: ActivityMainBinding
    
    override fun onCreate(savedInstanceState: Bundle?)
    private fun setupStatusBarColor()
    private fun showTutorialIfNeeded()
    private fun replaceFragment(fragment: Fragment)
}
```

**Navigation Flow:**
```
MainActivity
├── HomeFragment (default)
├── SensorFragment
└── SettingsFragment
```

---

### 2. BaseActivity

**Purpose:** Common base class for activities

**Responsibilities:**
- Common activity lifecycle management
- Shared initialization code
- Theme support

---

### 3. HomeFragment

**Purpose:** Main dashboard and overview

**Responsibilities:**
- Display current device position
- Show active audio profile
- Master sensor switching toggle
- Quick status information
- Navigation to detailed screens

**UI Components:**
- Status cards
- Position indicator
- Audio profile display
- Enable/disable toggle
- Quick action buttons

---

### 4. SensorFragment

**Purpose:** Detailed sensor monitoring and control

**Responsibilities:**
- Real-time sensor data display
- Individual mode toggles (On Desk, In Pocket, In Hand)
- Debug information visualization
- Position and profile status
- Live sensor value updates

**UI Components:**
- Detection mode switches
- Current position text
- Current profile text
- Debug info text (Z-axis, proximity, movement)
- Back button navigation

**Update Cycle:**
```
debugRunnable (500ms) → updateDebugInfo() → updatePositionDisplay()
```

---

### 5. SettingsFragment

**Purpose:** App configuration and preferences

**Responsibilities:**
- Performance mode toggle
- Notification preferences
- Dark mode toggle
- About information
- Settings persistence

**UI Components:**
- Performance mode switch
- Notifications switch
- Dark mode switch
- About section
- Version information

---

### 6. SilentMateSensorManager

**Purpose:** Core sensor logic and audio profile management

This is the **heart** of the application.

**Responsibilities:**
- Sensor registration and monitoring
- Position detection logic
- Audio profile switching
- Notification management
- Performance optimization
- State management

**Key Properties:**
```kotlin
private val sensorManager: SensorManager
private val audioManager: AudioManager
private val notificationManager: NotificationManager
private val sharedPreferences: SharedPreferences

private var accelerometer: Sensor?
private var gyroscope: Sensor?
private var proximity: Sensor?

private var currentPosition: DevicePosition
private var currentAudioProfile: AudioProfile

private var lastAccelerometerData: FloatArray
private var lastGyroscopeData: FloatArray
private var proximityDistance: Float
```

**Key Methods:**
```kotlin
fun startListening(callback: (DevicePosition, AudioProfile) -> Unit)
fun stopListening()
override fun onSensorChanged(event: SensorEvent?)
private fun detectDevicePosition(): DevicePosition
private fun mapPositionToAudioProfile(position: DevicePosition): AudioProfile
private fun applyAudioProfile(profile: AudioProfile)
private fun sendStatusChangeNotification(position: DevicePosition, profile: AudioProfile)
```

**Detection Flow:**
```
onSensorChanged()
    ↓
Store sensor data
    ↓
Check if enough time passed (500ms/2000ms)
    ↓
detectAndUpdatePosition()
    ↓
detectDevicePosition() [Priority-based logic]
    ↓
mapPositionToAudioProfile()
    ↓
applyAudioProfile()
    ↓
sendStatusChangeNotification()
    ↓
Invoke callback → Update UI
```

---

## Data Models

### DevicePosition Enum

```kotlin
enum class DevicePosition {
    UPSIDE_DOWN,    // Phone face-up on desk
    IN_POCKET,      // Phone in pocket/bag
    IN_HAND,        // Phone being held
    UNKNOWN         // Default/undetected state
}
```

### AudioProfile Enum

```kotlin
enum class AudioProfile {
    SILENT,         // No sound, no vibration
    VIBRATION,      // Vibration only
    GENERAL         // Full sound + vibration
}
```

---

## Sensor Processing

### Sensor Types Used

1. **TYPE_ACCELEROMETER**
   - Measures device acceleration including gravity
   - Used for: Orientation detection (face-up, face-down)
   - Axes: X (horizontal), Y (horizontal), Z (vertical)
   - Units: m/s²

2. **TYPE_GYROSCOPE**
   - Measures device rotation rate
   - Used for: Movement detection
   - Axes: X, Y, Z rotation rates
   - Units: rad/s

3. **TYPE_PROXIMITY**
   - Measures distance to nearest object
   - Used for: Pocket detection
   - Value: Distance in centimeters
   - Range: 0-5cm typically (device-dependent)

### Sensor Data Processing

```kotlin
// Accelerometer processing
val x = lastAccelerometerData[0]  // Horizontal tilt
val y = lastAccelerometerData[1]  // Horizontal tilt
val z = lastAccelerometerData[2]  // Vertical (gravity)

// Face-up: Z ≈ +9.8 (positive)
// Face-down: Z ≈ -9.8 (negative)

// Gyroscope processing
val movement = sqrt(
    gyroX² + gyroY² + gyroZ²
)

// Still: movement ≈ 0
// Moving: movement > 0.05
// Active: movement > 0.5

// Proximity processing
val isNear = proximityDistance < 5.0  // Within 5cm
val isVeryClose = proximityDistance < 2.0  // Within 2cm
```

---

## Detection Logic

### Priority-Based Detection

The detection system uses a **priority cascade**:

```
Priority 1: IN_POCKET (Vibration)
    ↓ (not matched)
Priority 2: IN_HAND (General)
    ↓ (not matched)
Priority 3: UPSIDE_DOWN (Silent)
    ↓ (not matched)
Default: UNKNOWN (Silent)
```

### Detection Algorithm

```kotlin
private fun detectDevicePosition(): DevicePosition {
    // Priority 1: Check for IN_POCKET
    if (featureEnabled[IN_POCKET]) {
        if (proximity < 5cm AND z between -3 and -12) {
            return IN_POCKET  // Vibration mode
        }
        if (proximity < 2cm) {
            return IN_POCKET  // Fallback for very close
        }
    }
    
    // Priority 2: Check for IN_HAND
    if (featureEnabled[IN_HAND]) {
        if (z between 5 and 12) {  // Face-up
            if (movement > 0.5) {
                return IN_HAND  // Active use
            }
            if (movement > 0.05) {
                return IN_HAND  // Holding
            }
        }
    }
    
    // Priority 3: Check for UPSIDE_DOWN (on desk)
    if (featureEnabled[UPSIDE_DOWN]) {
        if (z > 7 AND movement < 0.1) {
            return UPSIDE_DOWN  // Silent mode
        }
    }
    
    // Default
    return UNKNOWN  // Silent mode
}
```

### Thresholds

| Detection | Parameter | Threshold | Reason |
|-----------|-----------|-----------|---------|
| **On Desk** | Z-axis | > 7 | Face-up gravity |
| | Movement | < 0.1 | Very stable |
| **In Pocket** | Proximity | < 5cm | Object nearby |
| | Z-axis | -3 to -12 | Face-down |
| | Fallback | < 2cm | Very close |
| **In Hand** | Z-axis | 5 to 12 | Face-up |
| | Movement (hold) | > 0.05 | Slight movement |
| | Movement (active) | > 0.5 | Active use |

---

## Audio Profile Management

### Ringer Mode Mapping

```kotlin
private fun applyAudioProfile(profile: AudioProfile) {
    when (profile) {
        SILENT -> {
            audioManager.ringerMode = RINGER_MODE_SILENT
        }
        VIBRATION -> {
            audioManager.ringerMode = RINGER_MODE_VIBRATE
        }
        GENERAL -> {
            audioManager.ringerMode = RINGER_MODE_NORMAL
            // Ensure volume > 0
            if (currentVolume == 0) {
                setVolume(maxVolume / 2)
            }
        }
    }
}
```

### Permission Requirements

**Do Not Disturb Access** is required:

```kotlin
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
    val notificationManager = getSystemService(NotificationManager::class.java)
    if (!notificationManager.isNotificationPolicyAccessGranted) {
        // Cannot change ringer mode
        return
    }
}
```

---

## Notification System

### Notification Channels

**Channel ID:** `SilentMateChannelV2`

**Properties:**
- Importance: HIGH
- Sound: System default
- Vibration: Enabled
- Lights: Enabled
- Visibility: Public (on lockscreen)

### Notification Behavior

```kotlin
when (position) {
    IN_HAND -> {
        // Sound + Vibration
        notification.setSound(defaultUri)
        notification.setVibrate([0, 300, 200, 300])
        notification.setPriority(PRIORITY_MAX)
    }
    IN_POCKET -> {
        // Vibration only
        notification.setSound(null)
        notification.setVibrate([0, 800, 300, 800])
        notification.setPriority(PRIORITY_HIGH)
    }
    UPSIDE_DOWN, UNKNOWN -> {
        // Silent
        notification.setSound(null)
        notification.setVibrate([0])
        notification.setPriority(PRIORITY_LOW)
    }
}
```

---

## Performance Optimization

### Sensor Sampling Rates

**High Performance Mode:**
```kotlin
sensorDelay = SensorManager.SENSOR_DELAY_NORMAL
// ~200ms between readings
sensorCheckInterval = 500ms
```

**Power Saver Mode:**
```kotlin
sensorDelay = SensorManager.SENSOR_DELAY_UI
// ~1000ms between readings
sensorCheckInterval = 2000ms
```

### Throttling

```kotlin
val currentTime = System.currentTimeMillis()
if (currentTime - lastSensorCheckTime > sensorCheckInterval) {
    lastSensorCheckTime = currentTime
    detectAndUpdatePosition()
}
```

This prevents excessive CPU usage from sensor callbacks.

### State Stability

```kotlin
positionStableTime = 5000ms  // 5 seconds

private fun isPositionStable(): Boolean {
    val timeSinceLastChange = currentTime - lastPositionChangeTime
    return timeSinceLastChange > positionStableTime
}
```

Prevents rapid switching between modes.

---

## Data Persistence

### SharedPreferences

**File:** `SilentMatePrefs`

**Keys:**
```kotlin
// Detection toggles
"upside_down_enabled" → Boolean
"in_pocket_enabled" → Boolean
"in_hand_enabled" → Boolean

// Settings
"sensor_switching_enabled" → Boolean
"performance_mode" → Boolean
"notifications_enabled" → Boolean
"dark_mode" → Boolean
"tutorial_seen" → Boolean
```

### Theme Persistence

```kotlin
// Apply theme BEFORE super.onCreate()
val isDarkMode = sharedPreferences.getBoolean("dark_mode", false)
val mode = if (isDarkMode) MODE_NIGHT_YES else MODE_NIGHT_NO
AppCompatDelegate.setDefaultNightMode(mode)
```

---

## Threading Model

### Main Thread

- UI updates
- Fragment transactions
- Sensor callback handling (Android delivers on main thread)

### Background Operations

Sensor processing is lightweight and runs on main thread, but uses Handler for delayed operations:

```kotlin
private val handler = Handler(Looper.getMainLooper())

handler.postDelayed({
    detectAndUpdatePosition()
}, 1000)
```

---

## Error Handling

### Sensor Availability

```kotlin
accelerometer = sensorManager.getDefaultSensor(TYPE_ACCELEROMETER)
if (accelerometer == null) {
    Log.e("SensorManager", "Accelerometer not available")
    // Gracefully degrade or notify user
}
```

### Permission Errors

```kotlin
try {
    audioManager.ringerMode = newMode
} catch (e: SecurityException) {
    Log.e("SensorManager", "Permission denied", e)
    // Notify user to grant DND permission
}
```

### Notification Errors

```kotlin
try {
    NotificationManagerCompat.from(context).notify(id, notification)
} catch (e: SecurityException) {
    Log.e("SensorManager", "Notification permission not granted", e)
}
```

---

## Lifecycle Management

### Activity Lifecycle

```
onCreate() → Apply theme → Setup UI → Load fragment
    ↓
onResume() → Reapply status bar color
    ↓
onPause() → Keep sensors running (background service)
    ↓
onDestroy() → Cleanup if finishing
```

### Fragment Lifecycle

```
onCreateView() → Initialize views → Setup sensors
    ↓
onViewCreated() → Start monitoring → Begin updates
    ↓
onDestroyView() → Stop monitoring → Cleanup handlers
```

### Sensor Lifecycle

```
startListening() → Register sensors → Start detection loop
    ↓
Continuous monitoring...
    ↓
stopListening() → Unregister sensors → Stop callbacks
```

---

## Dependencies

### Core Android

- `androidx.appcompat` - Activity and Fragment support
- `androidx.core` - Core utilities
- `androidx.lifecycle` - Lifecycle components
- `androidx.fragment` - Fragment management

### Material Design

- `com.google.android.material` - Material components
- Material3 theme support

### View Binding

- `viewBinding` - Type-safe view access

### Kotlin

- Kotlin standard library
- Coroutines (for async operations)

---

## Build Configuration

### Minimum SDK

```gradle
minSdk = 21  // Android 5.0 (Lollipop)
```

### Target SDK

```gradle
targetSdk = 34  // Android 14
```

### Required Features

```xml
<uses-feature android:name="android.hardware.sensor.accelerometer" android:required="true" />
<uses-feature android:name="android.hardware.sensor.gyroscope" android:required="false" />
<uses-feature android:name="android.hardware.sensor.proximity" android:required="false" />
```

---

## Security Considerations

### Permissions

- Minimal permissions requested
- Clear explanation for each permission
- Runtime permission handling
- Graceful degradation when denied

### Data Protection

- No network access
- No external storage access
- All data stored locally
- No personal information collected

### Attack Surface

- Limited to changing ringer mode
- Cannot access calls, messages, or contacts
- Cannot make network requests
- No content provider exposure

---

## Testing Strategy

### Unit Tests

- Sensor data processing logic
- Position detection algorithm
- Audio profile mapping
- Threshold validation

### Integration Tests

- Sensor manager integration
- Audio manager integration
- Notification delivery
- Fragment navigation

### Manual Testing

- Physical device testing required
- Test all sensor combinations
- Verify battery usage
- Test on multiple devices

---

## Future Improvements

### Planned Architecture Changes

1. **Dependency Injection**
   - Use Hilt/Dagger for cleaner dependency management

2. **MVVM Architecture**
   - Introduce ViewModels
   - Use LiveData/StateFlow
   - Better separation of concerns

3. **Repository Pattern**
   - Abstract sensor data access
   - Easier testing and mocking

4. **Use Cases / Interactors**
   - Clean architecture principles
   - Business logic encapsulation

5. **Modularization**
   - Core module (sensor logic)
   - UI module (fragments)
   - Data module (persistence)

---

**Next:** [Sensor Logic](sensor-logic.md) for detailed detection algorithms