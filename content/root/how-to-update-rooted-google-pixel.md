+++
date = '2025-07-02T15:41:18+08:00'
title = 'How to Update a Rooted Google Pixel'
categories = ['Android Root']
tags = ['Root', 'Magisk', 'OTA Update']
+++

## How to Safely Update a Rooted Google Pixel

Updating a rooted Pixel device doesn't have to be risky or complicated. This
guide walks you through the process of updating your device while preserving
root access and user data.

> [!NOTE]
> ✅ **Your data will NOT be wiped** during this process. However, it's
> recommended to back up important data just in case.

Some rooted apps, Magisk modules, or LSPosed modules may not support the new
Android version. **Always verify compatibility** before proceeding - downgrading
is often not possible after an update.

### Step 1: Disable Magisk Modules

Magisk modules can interfere with OTA or factory image updates. To prevent
bootloops or failed installs:

1. Open the **Magisk** app.
2. Go to the **Modules** tab.
3. Disable (_untick_) **all installed modules**.
4. Reboot your phone.

### Step 2: Install the Firmware

1. Visit the
   [official Pixel factory images page](https://developers.google.com/android/images).
2. Locate the version you want (usually the latest one at the bottom).
   - Click **Link** to download the `.zip` image package for your device
     ([used for patching](#after)).
   - Click **Flash** to launch Google’s official web flashing tool.
3. When prompted, **allow ADB access** in your browser.
4. Enable **Developer Options** and **USB Debugging** on your phone.
5. If the device isn’t detected:
   - Run `adb kill-server` and reconnect the phone.
6. In the web UI:
   - Select your device.
   - Leave all advanced options **unchecked** (unless you're experienced).
   - Click **Install Build** and follow the on-screen instructions.

> ⚠️ **Do not disconnect the device** during installation. It may take several
> minutes depending on your internet speed.

Once completed, your device will reboot into the new Android version.

### Step 3: Patch the `init_boot.img` with Magisk

1. Extract the downloaded `.zip` firmware and locate `init_boot.img` inside a
   file like `image-<build>.zip`.
2. Push it to your phone:
   ```bash
   adb push init_boot.img /sdcard/
   ```
3. On your phone:
   - Open the **Magisk** app.
   - Tap **Install Magisk** on the home screen.
   - Choose **Select and patch a file**.
   - Select the `init_boot.img` file you just pushed.
   - Tap **LET’S GO**.
   - The app will output the location of the patched file, e.g.,
     `/sdcard/Download/magisk_patched.img`.
4. Pull the patched image back to your computer:
   ```bash
   adb pull /sdcard/Download/magisk_patched.img .
   ```

### Step 4: Flash the Patched Image

1. Power off your phone and boot into **Fastboot mode**:
   > [!INFO]
   > Typically, press and hold **Power + Volume Up** simultaneously.
2. Verify connection:
   ```bash
   fastboot devices
   ```
3. Flash the patched image:
   ```bash
   fastboot flash init_boot magisk_patched.img
   ```
4. Reboot your phone. You should now have root access restored.

### Final Step: Re-enable Modules

1. Open **Magisk** again.
2. Re-enable your desired **Magisk** and **LSPosed** modules.
3. Restart your phone once more.

✅ Done! You now have an updated Pixel device with full root access restored.
