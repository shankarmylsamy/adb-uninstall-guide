# 📱 Android Debloating Using ADB (No Root Required)

This guide explains how to remove preinstalled (bloatware) apps from Android devices using ADB (Android Debug Bridge) without root access.

Tested on:
- Xiaomi device (codename: riva)
- Xiaomi device (codename: pine)
- Windows OS

---

# ⚠️ Important Notes

- This does NOT permanently delete system apps.
- Apps are removed only for the current user (`--user 0`).
- Factory reset will restore them.
- Be careful not to remove critical system apps.

---

# ✅ Prerequisites

1. Windows PC
2. USB Cable
3. Android phone
4. ADB Platform Tools

---

# 📥 Step 1: Download ADB Platform Tools

Download from official Google website:
https://developer.android.com/studio/releases/platform-tools

Extract the ZIP file to:

C:\platform-tools

---

# 📱 Step 2: Enable Developer Options on Phone

1. Go to:
   Settings → About Phone
2. Tap **Build Number** 7 times
3. Go back to Settings → Developer Options
4. Enable:
   - USB Debugging

---

# 🔌 Step 3: Connect Phone to PC

Connect the device using USB cable.

Open Command Prompt and run:

```
cd C:\platform-tools
```

If you see:
```
The system cannot find the path specified.
```

Make sure the folder exists at:
```
C:\platform-tools
```

---

# 🔍 Step 4: Verify Device Connection

Run:

```
adb devices
```

First time output may be:

```
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
35c8e46a7d64    unauthorized
```

Check your phone screen and tap:
**Allow USB Debugging**

Run again:

```
adb devices
```

Expected output:

```
List of devices attached
35c8e46a7d64    device
```

Now your device is successfully connected.

---

# ❌ Important: Do NOT Run pm Directly in CMD

If you run:

```
pm uninstall -k --user 0 com.google.android.music
```

You will get:

```
'pm' is not recognized as an internal or external command
```

Reason:
`pm` command works only inside Android shell.

---

# 🖥️ Step 5: Enter ADB Shell

Run:

```
adb shell
```

You will see:

For riva device:
```
riva:/ $
```

For pine device:
```
pine:/ $
```

Now you can execute uninstall commands.

---

# 📦 Device 1 (riva) – Removed Apps

Inside adb shell:

```
pm uninstall -k --user 0 com.google.android.music
pm uninstall -k --user 0 com.google.android.apps.docs
```

Output:
```
Success
```

---

# 📦 Device 2 (pine) – Removed Apps

Inside adb shell:

```
pm uninstall -k --user 0 com.android.browser
pm uninstall -k --user 0 com.google.android.apps.tachyon
pm uninstall -k --user 0 com.facemoji.lite.xiaomi
pm uninstall -k --user 0 com.xiaomi.mipicks
pm uninstall -k --user 0 com.google.android.googlequicksearchbox
pm uninstall -k --user 0 com.google.android.videos
pm uninstall -k --user 0 com.google.android.music
pm uninstall -k --user 0 com.xiaomi.payment
pm uninstall -k --user 0 com.mipay.wallet.in
pm uninstall -k --user 0 com.miui.videoplayer
pm uninstall -k --user 0 com.google.android.apps.photos
pm uninstall -k --user 0 com.xiaomi.scanner
pm uninstall -k --user 0 com.xiaomi.midrop
pm uninstall -k --user 0 com.miui.weather2
```

---

# ❗ Special Case

For:

```
pm uninstall -k --user 0 com.facemoji.lite.xiaomi
```

Output:
```
Failure [-1000]
```

This means:
- App is protected
- System restricted removal
- Cannot uninstall for user 0

This can be ignored if not critical.

---

# 🔄 How to Reinstall Removed App

To restore an app:

```
cmd package install-existing <package-name>
```

Example:

```
cmd package install-existing com.google.android.music
```

---

# 🔎 How to Find Installed Packages

List all packages:

```
pm list packages
```

Search specific keyword:

```
pm list packages | grep google
```

(Note: grep may not work on all devices.)

---

# 🚪 Exit ADB Shell

To exit:

```
exit
```

---

# 🎯 Summary

1. Install ADB
2. Enable USB Debugging
3. Connect device
4. Run adb devices
5. Enter adb shell
6. Run pm uninstall -k --user 0 <package>
7. Verify Success

---

# 🛡️ Disclaimer

Use at your own risk.
Removing essential system apps may cause system instability.

Factory reset will restore removed apps.
