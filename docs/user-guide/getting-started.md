# Getting Started

Welcome to Silent Mate! This guide will help you get started with the app and set up automatic audio profile switching.

## Installation

### Requirements

- **Android Version:** 5.0 (Lollipop) or higher
- **Sensors Required:**
  - Accelerometer (all modern phones)
  - Gyroscope (most phones)
  - Proximity sensor (recommended for pocket detection)
- **Storage:** ~10 MB
- **RAM:** ~50 MB during active use

### Download & Install

1. Download the APK from the provided source
2. Enable "Install from Unknown Sources" if prompted
3. Open the APK file and tap "Install"
4. Wait for installation to complete
5. Tap "Open" to launch Silent Mate

## Initial Setup
 HomePage: /workspaces/Silentmate-Docs/docs/assets/HomeSM.jpg
 Dark mode: /workspaces/Silentmate-Docs/docs/assets/Dekmode.jpg
 Addevent: /workspaces/Silentmate-Docs/docs/assets/Addevent.jpg
 Event: /workspaces/Silentmate-Docs/docs/assets/Event.jpg
 Notifications: /workspaces/Silentmate-Docs/docs/assets/Notifications.jpg
 Sensor-based context switching: /workspaces/Silentmate-Docs/docs/assets/SensorbasedCSPage.jpg
 Settings: /workspaces/Silentmate-Docs/docs/assets/Settings.jpg
 

### Step 1: Grant Permissions

When you first launch Silent Mate, you'll need to grant essential permissions:

#### Do Not Disturb (DND) Access

This permission is **required** for the app to change audio profiles.

1. Tap "Grant Permission" when prompted
2. Find "Silent Mate" in the list
3. Toggle the switch to ON
4. Tap "Allow" if asked to confirm

**Why needed:** Android requires this permission to programmatically switch between Silent, Vibration, and General modes.

#### Notification Permission

This permission allows Silent Mate to notify you of profile changes.

1. Tap "Allow" when prompted
2. Or grant later in Settings → Apps → Silent Mate → Permissions

**Why needed:** To show you when your audio profile has changed (e.g., "Switched to Silent Mode").

### Step 2: Complete Tutorial

On first launch, you'll see a quick tutorial explaining:

- The three detection modes (On Desk, In Pocket, In Hand)
- How sensor-based switching works
- Key features and benefits

You can:
- Swipe through the tutorial screens
- Tap "Skip" to skip the tutorial
- Tap "Get Started" when finished

The tutorial only appears once. You can always refer to this documentation later.

### Step 3: Enable Sensor Switching

After the tutorial:

1. You'll land on the **Home Screen**
2. Toggle the main **"Enable Sensor Switching"** switch to ON
3. The app will start monitoring your device position

## First Use

### Test Each Detection Mode

It's a good idea to test each mode to see how it works:

#### Test 1: On Desk (Silent Mode)

1. Place your phone face-up on a flat surface (desk, table)
2. Leave it still for 2-3 seconds
3. You should see: "On Desk 📱 detected - Silent Mode 🔇"
4. Your phone should now be in Silent mode

#### Test 2: In Pocket (Vibration Mode)

1. Turn your phone face-down (screen facing down)
2. Cover the top of the phone with your hand (covering proximity sensor)
3. Wait 2-3 seconds
4. You should see: "In Pocket 👖 detected - Vibration Mode 📳"
5. Your phone should now be in Vibration mode

#### Test 3: In Hand (General Mode)

1. Pick up your phone normally (face-up)
2. Move it slightly or tilt it
3. Wait 2-3 seconds
4. You should see: "In Hand 🤚 detected - General Mode 🔊"
5. Your phone should now be in General mode with full sound

### Verify Settings

Go to the **Sensor Screen** (bottom navigation, center icon) to:

- See real-time sensor data
- Verify all three detection switches are ON
- Monitor current position and audio profile
- Check debug information (Z-axis, proximity, movement)

## Understanding the Interface

### Home Screen 🏠

**Main Elements:**

- **Status Card:** Shows current position and audio profile
- **Sensor Switching Toggle:** Master on/off switch
- **Quick Stats:** Overview of enabled features
- **Go to Sensors Button:** Opens detailed sensor monitoring

**Quick Actions:**

- Toggle sensor switching on/off
- View current status at a glance
- Navigate to other sections

### Sensor Screen 📱

**Main Elements:**

- **Detection Toggles:** Individual switches for each mode
  - On Desk 📱
  - In Pocket 👖
  - In Hand 🤚
- **Current Status:** Real-time position and profile display
- **Debug Info:** Live sensor readings
  - Z-axis value
  - Proximity distance (cm)
  - Movement magnitude

**What You Can Do:**

- Enable/disable specific detection modes
- Monitor live sensor data
- See exactly what the app is detecting
- Test different phone positions

### Settings Screen ⚙️

**Available Options:**

- **Notifications:** Toggle status change notifications
- **Performance Mode:** Switch between Power Saver and High Performance
- **Dark Mode:** Toggle dark/light theme
- **About:** App version and information

## Common First-Time Questions

### Q: Why isn't pocket detection working?

**A:** Make sure:
1. Proximity sensor is not blocked by a screen protector
2. Phone is face-down (screen facing inward)
3. "In Pocket" toggle is ON in Sensor screen
4. You're covering the top of the phone where the sensor is located

### Q: How do I know if it's working?

**A:** You'll see:
1. Toast notifications when position changes
2. Status updates in the Sensor screen
3. Audio profile changes (test by checking ringer mode in system settings)
4. Live debug info showing sensor readings

### Q: Can I disable certain modes?

**A:** Yes! Go to Sensor screen and toggle off any modes you don't want:
- Turn OFF "On Desk" if you don't want silent mode
- Turn OFF "In Pocket" if you don't need pocket detection
- Turn OFF "In Hand" if you want manual control

### Q: Does it work with the screen off?

**A:** Yes! Silent Mate continues monitoring even when:
- Screen is off
- Phone is locked
- You're using other apps
- Phone is in standby mode

### Q: How much battery does it use?

**A:** In Power Saver mode: ~2-5% per day
In High Performance mode: ~5-10% per day

Battery usage depends on how often your phone changes positions.

## Next Steps

Now that you're set up:

1. ✅ **Learn the Features** - Read the [Features](features.md) guide
2. ✅ **Customize Settings** - Check [How to Use](how-to-use.md) for detailed instructions
3. ✅ **Optimize Performance** - See tips in [Troubleshooting](troubleshooting.md)
4. ✅ **Get Help** - Visit [FAQ](faq.md) for common questions

## Need Help?

If you encounter issues during setup:

- Check [Troubleshooting Guide](troubleshooting.md)
- Review [FAQ](faq.md)
- Check sensor availability on your device
- Ensure all permissions are granted

**Welcome to Silent Mate! 🎯📱**