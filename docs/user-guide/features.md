# Features

Silent Mate offers intelligent, automatic audio profile switching based on how you hold and place your device.

## Core Features

### 🎯 Three Detection Modes

Silent Mate can detect three distinct phone positions and automatically adjust your audio profile accordingly.

### 📅 Event Scheduling

![Add Event](../assets/Addevent.jpg)

**Create Scheduled Audio Profiles:**

Silent Mate allows you to schedule audio profiles for specific times and locations, perfect for:
- Regular meetings or classes
- Gym sessions
- Sleep schedule
- Work hours
- Any recurring event

**Event Parameters:**

| Parameter | Description | Example |
|-----------|-------------|---------|
| **Event Name** | Custom label for the event | "Monday Meeting", "Gym Time" |
| **Time** | Start and end time | 9:00 AM - 10:00 AM |
| **Location** | Optional location name | "Conference Room", "Gym" |
| **Recurrence** | Repeat pattern | Daily, Weekly, Monthly, Custom |
| **Audio Profile** | Desired mode | Silent, Vibration, General |

**How It Works:**
1. Create event with name, time, location, and recurrence
2. Select desired audio profile for that event
3. App automatically switches profiles when event time arrives
4. Switches back to sensor-based detection when event ends

**Event Priority:**
- Scheduled events override sensor-based detection
- Multiple overlapping events: Latest created takes priority
- Events can be enabled/disabled individually
- Works alongside sensor switching

![Event List](../assets/Event.jpg)

**Use Cases:**
- **Work Meetings:** Silent mode during scheduled meetings
- **Gym Sessions:** General mode for music playback
- **Sleep Time:** Silent mode from 11 PM to 7 AM
- **Classes:** Silent mode during class hours
- **Commute:** Vibration mode during travel time

#### 📱 On Desk Detection

**What it does:**
- Detects when your phone is lying flat, face-up on a surface
- Automatically switches to **Silent Mode** 🔇

**How it works:**
- Monitors Z-axis acceleration (gravity)
- Checks for minimal movement (device is stable)
- Confirms face-up orientation

**Perfect for:**
- During meetings or presentations
- While working at your desk
- During sleep time
- In quiet environments (libraries, theaters)

**Technical Details:**
- **Trigger:** Z-axis > 7 (face-up) + movement < 0.1 (very stable)
- **Result:** RINGER_MODE_SILENT
- **Notification:** Silent notification (no sound/vibration)

---

#### 👖 In Pocket Detection

**What it does:**
- Detects when your phone is in your pocket or bag
- Automatically switches to **Vibration Mode** 📳

**How it works:**
- Uses proximity sensor to detect nearby objects
- Confirms face-down orientation (screen facing inward)
- Validates with accelerometer data

**Perfect for:**
- Walking around with phone in pocket
- Phone in a bag or purse
- Face-down on a table
- When you need discrete notifications

**Technical Details:**
- **Trigger:** Proximity < 5cm + Z-axis between -3 and -12 (face-down)
- **Fallback:** Proximity < 2cm (very close)
- **Result:** RINGER_MODE_VIBRATE
- **Notification:** Vibration pattern [0, 800, 300, 800]ms

---

#### 🤚 In Hand Detection

**What it does:**
- Detects when you're actively holding or using your phone
- Automatically switches to **General Mode** 🔊

**How it works:**
- Monitors accelerometer for face-up orientation
- Detects movement from gyroscope data
- Distinguishes between holding and active use

**Perfect for:**
- When you pick up your phone
- While browsing or texting
- During active phone use
- When you want full sound and vibration

**Technical Details:**
- **Trigger:** Z-axis 5-12 (face-up) + movement > 0.05 (holding) or > 0.5 (active)
- **Result:** RINGER_MODE_NORMAL
- **Notification:** Sound + vibration
- **Volume Check:** Ensures ring volume > 0, sets to 50% if muted

---

## Audio Profiles

### 🔇 Silent Mode

**What it does:**
- Mutes all ringtones and notification sounds
- No vibration
- Alarms still work normally

**When activated:**
- Phone on desk (face-up, stable)
- Unknown/default state

**System behavior:**
- RINGER_MODE_SILENT
- No sounds for calls or notifications
- DND-like behavior (but alarms still ring)

---

### 📳 Vibration Mode

**What it does:**
- Vibrates for calls and notifications
- No sound output
- Discrete alerts

**When activated:**
- Phone in pocket (proximity + face-down)
- Phone in bag or purse

**System behavior:**
- RINGER_MODE_VIBRATE
- Strong vibration patterns
- No audio output

---

### 🔊 General Mode

**What it does:**
- Full ringtone and notification sounds
- Vibration enabled
- Normal phone behavior

**When activated:**
- Phone in hand (face-up + movement)
- Active use detected

**System behavior:**
- RINGER_MODE_NORMAL
- Sound + vibration for calls/notifications
- Restores volume if muted

---

## Advanced Features

### ⚡ Performance Modes

Silent Mate offers two performance profiles to balance detection speed and battery life.

#### High Performance Mode

**Characteristics:**
- Faster sensor sampling rate (SENSOR_DELAY_NORMAL)
- Quicker position detection (~200-500ms)
- More frequent sensor checks
- Higher battery consumption

**Best for:**
- When you need instant detection
- During active phone use
- When battery isn't a concern
- Testing and debugging

**Battery Impact:** ~5-10% per day

#### Power Saver Mode (Default)

**Characteristics:**
- Slower sensor sampling rate (SENSOR_DELAY_UI)
- Slightly delayed detection (~500-1000ms)
- Less frequent sensor checks
- Minimal battery consumption

**Best for:**
- All-day usage
- When battery life is important
- Normal daily use
- Background monitoring

**Battery Impact:** ~2-5% per day

---

### 🔔 Smart Notifications

Silent Mate notifies you when your audio profile changes, with intelligent notification behavior based on the mode.

#### Notification Types

**For General Mode (In Hand):**
- ✅ Sound alert
- ✅ Vibration pattern
- ✅ High priority notification
- 🔊 Audible ringtone plays

**For Vibration Mode (In Pocket):**
- ❌ No sound
- ✅ Strong vibration (800ms patterns)
- ✅ Normal priority
- 📳 Discrete alert

**For Silent Mode (On Desk):**
- ❌ No sound
- ❌ No vibration
- ✅ Low priority notification
- 🔇 Silent notification only

#### Notification Content

Each notification shows:
- Current position (On Desk / In Pocket / In Hand)
- Active audio profile (Silent / Vibration / General)
- Status icon
- Timestamp

**Customization:**
- Enable/disable notifications in Settings
- Notifications can be turned off without affecting detection
- Notification behavior adapts to each mode automatically

---

### 🎛️ Customizable Detection

Each detection mode can be independently enabled or disabled, giving you full control over which features you use.

#### Individual Mode Control

**Toggle On Desk Detection:**
- When ON: Phone on desk → Silent mode
- When OFF: Desk position is ignored

**Toggle In Pocket Detection:**
- When ON: Phone in pocket → Vibration mode
- When OFF: Pocket position is ignored

**Toggle In Hand Detection:**
- When ON: Phone in hand → General mode
- When OFF: Hand position is ignored

#### Use Cases

**Only Silent When on Desk:**
- ✅ Enable: On Desk
- ❌ Disable: In Pocket, In Hand
- Result: Manual control except when on desk

**Only Vibrate in Pocket:**
- ❌ Disable: On Desk
- ✅ Enable: In Pocket
- ❌ Disable: In Hand
- Result: Manual control except in pocket

**Full Automation:**
- ✅ Enable: All three modes
- Result: Complete automatic audio management

---

### 📊 Real-Time Monitoring

The Sensor screen provides live debugging and monitoring capabilities.

**Live Sensor Data:**
- **Z-axis:** Current vertical acceleration (gravity)
- **Proximity:** Distance to nearest object (cm)
- **Movement:** Gyroscope magnitude (rotation speed)
- **Position:** Currently detected state

**Debug Information:**
- Sensor readings update every 500ms
- Color-coded status indicators
- Real-time position tracking
- Movement visualization

**Benefits:**
- Troubleshoot detection issues
- Understand how sensors work
- Verify sensor availability
- Test different positions

---

### 🌙 Dark Mode Support

Silent Mate includes a full dark theme for comfortable use in low-light conditions.

**Features:**
- System-wide dark theme
- OLED-friendly colors
- Preserves battery on OLED screens
- Smooth theme transitions
- Persists across app restarts

**How to Enable:**
1. Go to Settings ⚙️
2. Toggle "Dark Mode"
3. App immediately switches theme

---

### 🔐 Privacy & Security

**Data Privacy:**
- ✅ No internet connection required
- ✅ No data collection or tracking
- ✅ No ads or analytics
- ✅ All processing happens on-device
- ✅ No account required

**Permissions Used:**
- **Do Not Disturb Access:** Only to change ringer mode
- **Notification Permission:** Only for status alerts
- **Sensor Access:** Automatically granted (hardware access)

**Security:**
- No sensitive data stored
- No network communication
- Open-source code (if applicable)
- Transparent permission usage

---

## Feature Comparison

| Feature | Free Version |
|---------|--------------|
| On Desk Detection | ✅ |
| In Pocket Detection | ✅ |
| In Hand Detection | ✅ |
| Performance Modes | ✅ |
| Smart Notifications | ✅ |
| Dark Mode | ✅ |
| No Ads | ✅ |
| Offline Operation | ✅ |
| Real-time Monitoring | ✅ |
| Customizable Modes | ✅ |

---

## Coming Soon

**Planned Features:**

- 🔄 Custom sensitivity adjustments
- ⏰ Time-based profiles (work hours, sleep time)
- 📍 Location-based switching
- 🔊 Custom vibration patterns
- 📈 Usage statistics and analytics
- 🎨 Custom themes and colors
- 🔗 Integration with other automation apps
- ☁️ Backup and restore settings

---

## Feature Benefits

### For Office Workers
- Silent during meetings (phone on desk)
- Vibrate when in pocket
- Sound when actively using

### For Students
- Silent during classes (phone on desk)
- Discrete vibration in bag
- Full sound when studying alone

### For Busy Professionals
- Never miss calls when holding phone
- Discrete in meetings (pocket mode)
- Silent during focused work (desk mode)

### For Everyone
- Hands-free audio management
- No more manual switching
- Intelligent automation
- Battery efficient
- Privacy-focused

---

**Next:** Learn [How to Use](how-to-use.md) these features in detail.