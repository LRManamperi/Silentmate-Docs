# Frequently Asked Questions (FAQ)

## General Questions

### What is Silent Mate?

Silent Mate is an intelligent Android app that automatically manages your phone's audio profile based on how you hold or place your device. It uses hardware sensors (accelerometer, gyroscope, proximity) to detect whether your phone is on a desk, in your pocket, or in your hand, and switches between Silent, Vibration, and General modes accordingly.

### How does Silent Mate work?

Silent Mate continuously monitors three hardware sensors:

1. **Accelerometer** - Detects orientation (face-up, face-down)
2. **Gyroscope** - Measures movement and rotation
3. **Proximity** - Detects nearby objects

Based on this sensor data, the app determines your phone's position and automatically adjusts the ringer mode (Silent, Vibrate, or Normal).

### Is Silent Mate free?

Yes! Silent Mate is completely free with:
- ✅ All features unlocked
- ✅ No ads
- ✅ No in-app purchases
- ✅ No subscriptions
- ✅ No data collection

---

## Privacy & Security

### Does Silent Mate collect my data?

**No.** Silent Mate:
- ❌ Does NOT collect any personal data
- ❌ Does NOT require internet connection
- ❌ Does NOT track your location
- ❌ Does NOT send data to servers
- ✅ All processing happens on-device
- ✅ Completely offline operation

### What permissions does it need?

Silent Mate requires only two permissions:

1. **Do Not Disturb Access** (Required)
   - Why: To change ringer modes (Silent/Vibrate/Normal)
   - What it does: Only modifies audio settings
   - What it doesn't do: Cannot access calls, messages, or contacts

2. **Notification Permission** (Optional)
   - Why: To notify you of profile changes
   - What it does: Shows status notifications
   - Can be disabled: App still works without notifications

**Sensor access is automatically granted by Android and cannot access sensitive data.**

### Is it safe to use?

Yes! Silent Mate is safe because:
- ✅ No internet connection required
- ✅ No access to personal data
- ✅ Minimal permissions required
- ✅ Transparent permission usage
- ✅ No background data collection
- ✅ Source code can be reviewed (if open source)

---

## Functionality Questions

### Does it work in the background?

**Yes!** Silent Mate continues monitoring even when:
- ✅ Screen is off
- ✅ Phone is locked
- ✅ Using other apps
- ✅ Phone is in standby mode

The app runs as a background service to continuously monitor your phone's position.

### Will it drain my battery?

Battery usage is minimal:

**Power Saver Mode** (Default):
- ~2-5% per day
- Recommended for daily use

**High Performance Mode**:
- ~5-10% per day
- Recommended for active use only

Battery consumption depends on:
- How often you change phone positions
- Which detection modes are enabled
- Performance mode setting

### Does it work with the screen off?

**Yes!** Silent Mate works regardless of screen state:
- Screen on → Works ✅
- Screen off → Works ✅
- Phone locked → Works ✅
- Always-on display → Works ✅

### Will it affect my alarms?

**No!** Silent Mate only affects:
- ✅ Ringtones (calls)
- ✅ Notification sounds
- ❌ **Alarms are NOT affected**

Your alarms will always ring at full volume, regardless of the audio profile.

### Can I still use Do Not Disturb manually?

**Yes!** You can:
- Use system DND alongside Silent Mate
- Manually override ringer mode anytime
- System DND takes precedence when active
- Silent Mate respects system DND rules

---

## Compatibility Questions

### What Android version is required?

**Minimum:** Android 5.0 (Lollipop)  
**Recommended:** Android 8.0 (Oreo) or higher  
**Latest tested:** Android 14

### Does it work on all devices?

Silent Mate works on **most** Android devices, but requires:

**Required Sensors:**
- ✅ Accelerometer (99% of devices have this)
- ✅ Gyroscope (90%+ of devices have this)

**Optional Sensors:**
- ⚠️ Proximity sensor (needed for pocket detection)
  - Budget devices may not have this
  - Face-down detection still works as fallback

**To check your device:**
1. Open Silent Mate
2. Go to Sensor screen
3. Check if sensor values change when you move the phone

### Does it work on tablets?

**Partial support.** Tablets can use Silent Mate, but:
- ⚠️ Tablets may lack proximity sensors
- ⚠️ Movement detection may be less accurate (larger device)
- ✅ Desk detection works normally
- ✅ Hand detection works if gyroscope present

### Does it work with custom ROMs?

**Usually yes!** Silent Mate works on:
- ✅ Stock Android
- ✅ LineageOS
- ✅ Pixel Experience
- ✅ /e/OS
- ✅ Most custom ROMs

**May require additional permissions on:**
- Some ROMs with aggressive battery optimization
- ROMs with modified permission systems
- Security-focused ROMs (GrapheneOS, CalyxOS)

---

## Feature Questions

### Can I customize detection sensitivity?

**Not currently.** Detection thresholds are optimized for most devices:

- On Desk: Z > 7, Movement < 0.1
- In Pocket: Proximity < 5cm, Z between -3 and -12
- In Hand: Z 5-12, Movement > 0.05

**Coming in future updates:**
- Custom threshold adjustments
- Calibration wizard
- Per-device profiles

### Can I set custom vibration patterns?

**Not currently.** Current vibration patterns:

- General Mode: [0, 300, 200, 300]ms
- Vibration Mode: [0, 800, 300, 800]ms

**Planned for future versions:**
- Custom vibration patterns
- Multiple pattern options
- Pattern intensity control

### Can I schedule automatic switching?

**Not currently.** Manual workarounds:

1. Disable sensor switching during specific times
2. Use Android's Bedtime mode + Silent Mate
3. Manually toggle detection modes

**Coming soon:**
- Time-based profiles
- Work hours mode
- Sleep time mode
- Weekend vs. weekday schedules

### Can I use it with location-based rules?

**Not currently.** Location features planned:

- Home location → specific profile
- Work location → specific profile
- Custom location rules
- Geofencing support

### Does it support multiple audio profiles?

Currently supports 3 standard profiles:

1. **Silent Mode** 🔇 - No sound, no vibration
2. **Vibration Mode** 📳 - Vibration only
3. **General Mode** 🔊 - Sound + vibration

**Cannot currently:**
- ❌ Create custom profiles
- ❌ Set custom volume levels per mode
- ❌ Define app-specific rules

**Planned features:**
- Custom profile creation
- Volume level customization
- App-specific behaviors

---

## Usage Questions

### How accurate is the detection?

**Very accurate** when used correctly:

| Mode | Accuracy | Notes |
|------|----------|-------|
| On Desk | ~95% | Requires flat, stable surface |
| In Pocket | ~90% | Needs proximity sensor + face-down |
| In Hand | ~95% | Detects movement reliably |

**Factors affecting accuracy:**
- Phone case thickness (affects proximity)
- Surface stability (affects desk detection)
- Movement patterns (affects hand detection)
- Sensor quality (varies by device)

### Can I disable specific modes?

**Yes!** Each mode can be independently controlled:

1. Go to Sensor screen 📱
2. Toggle individual switches:
   - On Desk 📱
   - In Pocket 👖  
   - In Hand 🤚

**Use cases:**
- Only silent on desk → Enable only "On Desk"
- Only vibrate in pocket → Enable only "In Pocket"
- Full automation → Enable all three

### What happens if multiple modes detect simultaneously?

**Priority order:**
1. **In Pocket** (highest priority) → Vibration
2. **In Hand** (medium priority) → General
3. **On Desk** (low priority) → Silent
4. **Unknown** (default) → Silent

The highest priority matching mode takes effect.

### How long does it take to detect position changes?

**Detection speed:**

**Power Saver Mode:**
- Initial detection: 500-1000ms
- Position change: 500-2000ms

**High Performance Mode:**
- Initial detection: 200-500ms
- Position change: 200-1000ms

**Why not instant?**
- Prevents false positives
- Confirms stable position
- Filters out brief movements

### Can I use it while driving?

**Yes, but be cautious:**

✅ **Good:** Phone in holder (hands-free)
- Will likely detect as "In Hand" (movement)
- General mode = full sound for navigation/calls

⚠️ **Caution:** Phone on passenger seat
- May detect as "On Desk" (stable)
- Silent mode = missed calls/alerts

**Recommendation:**
- Disable sensor switching while driving
- Use Android Auto / car mode instead
- Re-enable when parked

---

## Troubleshooting FAQs

### Why isn't pocket detection working?

**Common causes:**

1. **No proximity sensor** - Check if your device has one
2. **Sensor blocked** - Remove thick screen protectors/cases
3. **Wrong orientation** - Phone must be face-down
4. **Too far** - Sensor must detect < 5cm

**Solution:**
See detailed guide in [Troubleshooting](troubleshooting.md#in-pocket-detection-not-working)

### Why does it keep switching modes?

**Common causes:**

1. **High Performance Mode** - Too sensitive
2. **Unstable surface** - Table/desk vibrating
3. **Multiple modes enabled** - Conflicting detections

**Solutions:**
- Enable Power Saver mode
- Place on stable surface
- Disable unused detection modes

### Why doesn't it work with screen protectors?

**Issue:** Some screen protectors block proximity sensor

**Solutions:**
1. Use protectors with sensor cutouts
2. Remove protector temporarily to test
3. Use face-down detection as fallback (works without proximity)

---

## Comparison Questions

### How is it different from Tasker?

| Feature | Silent Mate | Tasker |
|---------|-------------|--------|
| Sensor-based detection | ✅ Built-in | ⚠️ Complex setup |
| User-friendly | ✅ Simple | ❌ Learning curve |
| Battery usage | ✅ Optimized | ⚠️ Varies |
| Cost | ✅ Free | 💰 Paid |
| Automation scope | Audio only | Everything |

**Use Silent Mate if:** You only need automatic audio switching  
**Use Tasker if:** You need complex, multi-app automation

### How is it different from Do Not Disturb?

| Feature | Silent Mate | System DND |
|---------|-------------|-----------|
| Automatic detection | ✅ Yes | ❌ Manual |
| Position-based | ✅ Yes | ❌ No |
| Time-based | ❌ No | ✅ Yes |
| App exceptions | ❌ No | ✅ Yes |
| Contact priorities | ❌ No | ✅ Yes |

**Use both together for maximum control!**

### How is it different from other profile apps?

**Silent Mate advantages:**
- ✅ Truly automatic (sensor-based)
- ✅ No manual switching needed
- ✅ Works in background without user action
- ✅ Free and ad-free
- ✅ Privacy-focused (no data collection)

**Other apps:**
- ⚠️ Usually require manual triggers
- ⚠️ Location-based (drains battery, privacy concerns)
- ⚠️ Time-based only (not contextual)
- ⚠️ Often have ads or paid features

---

## Advanced Questions

### Can I integrate it with other apps?

**Not currently.** No API or integration support yet.

**Planned features:**
- Intent broadcast on profile changes
- Tasker plugin support
- IFTTT integration
- Webhook support

### Does it have widget support?

**Not currently.** Widgets planned for future releases:

- Quick toggle widget
- Status display widget
- Mode selector widget

**Current workaround:**
- Add app shortcut to home screen
- Use notification quick settings tile (if available)

### Can I export/import settings?

**Not currently.** Settings are stored locally in SharedPreferences.

**Planned features:**
- Backup to file
- Restore from backup
- Cloud sync (optional)
- Device transfer

### Is the source code available?

This depends on your distribution model:

- If **open source**: Link to GitHub repository
- If **closed source**: "Not currently available"

### Can I contribute to development?

If open source:
- Yes! See [Contributing Guide](../developer/contributing.md)
- Report bugs on GitHub Issues
- Submit feature requests
- Contribute code via pull requests

If closed source:
- Submit feedback via app
- Request features
- Report bugs
- Beta testing opportunities

---

## Performance FAQs

### Why does it use battery?

**Reasons:**
1. **Continuous sensor monitoring** - Accelerometer, gyroscope, proximity
2. **Background service** - Always running for instant detection
3. **Audio profile switching** - System calls consume energy
4. **Notifications** - Display, sound, vibration

**Optimization:**
- Use Power Saver mode
- Disable unused detection modes
- Reduce notifications

### Can I make it more power efficient?

**Yes!** Try these tips:

1. **Enable Power Saver Mode:**
   - Settings → Performance Mode → OFF

2. **Disable unused modes:**
   - Sensor screen → Toggle off what you don't need

3. **Reduce notifications:**
   - Settings → Notifications → OFF

4. **Battery optimization:**
   - Settings → Battery → Optimize Silent Mate

**Expected result:**
- Power Saver + minimal modes = 1-3% per day

### Does it affect other apps?

**No!** Silent Mate:
- ✅ Runs independently
- ✅ Doesn't interfere with other apps
- ✅ Only changes system ringer mode
- ✅ No conflicts with normal apps

**Possible conflicts:**
- ⚠️ Other audio automation apps
- ⚠️ Apps that also control ringer mode
- ⚠️ Aggressive task killers

**Solution:** Last app to make changes wins (standard Android behavior)

---

## Future Features

### What's coming next?

**Planned features:**

- 🔄 Custom sensitivity adjustments
- ⏰ Time-based profiles
- 📍 Location-based switching
- 🔊 Custom vibration patterns
- 📈 Usage statistics
- 🎨 Custom themes
- 🔗 Tasker integration
- ☁️ Settings backup/restore
- 📱 Widget support
- 🌐 Multi-language support

### Can I request a feature?

**Yes!** Submit feature requests via:
- App's feedback form (if available)
- GitHub Issues (if open source)
- Email support
- User forums

**Most requested features get priority!**

---

## Support

### How do I get help?

1. **Read documentation:**
   - [Getting Started](getting-started.md)
   - [Features Guide](features.md)
   - [Troubleshooting](troubleshooting.md)

2. **Check app logs:**
   - Sensor screen shows debug information

3. **Contact support:**
   - In-app support (if available)
   - Email support address
   - GitHub Issues (if open source)

### How do I report a bug?

**Include this information:**

1. **Device details:**
   - Phone model
   - Android version
   - Custom ROM (if applicable)

2. **Issue description:**
   - What happened
   - What you expected
   - Steps to reproduce

3. **Debug info:**
   - Sensor screen values
   - Which modes are enabled
   - Recent actions before bug

4. **Screenshots/video:**
   - If applicable

---

**Still have questions?** Check the [Troubleshooting Guide](troubleshooting.md) or contact support!