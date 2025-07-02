+++
date = '2025-07-02T15:41:18+08:00'
title = 'How to Update Rooted Google Pixel'
categories = ['android root']
tags = ['root', 'magisk', 'OTA update']
+++

## Content

### Heads up

\* Updating your phone **will keep** so you don't need to worry about it.

Some rooted apps, Magisk modules, and LSPosed modules might not support the new versions of Android you are trying to install so just make sure before installing the updates cause once you are update you cannot revert to an old version


### Disable Existing Modules

Sometimes Magisk modules can effect can brake OTA updates or get broken by the upadates
the safest thing we can do is just disable them (we will enable them after the update is completed)

- Open your Magisk app
- Navigate to the "Modules" tab
    - Tick off _ALL_ of the installed modules.
- Restart your phone.

### Update the firmware

- Navigate to [factory images for Pixel](https://developers.google.com/android/images) 
- Find your wanted version (usually the most bottom one in your model section - for the newest version)
    - click on **link** this will download the `img` to your computer as we will need it for our next step [patching the images](#install-magisk-patch)
- click on **flash** under your selected version, this will redirect you to the google flashing site (that work suprisnly well)
- It will pop-up and prompt you to **Allow ADB access** - make sure you ~~Allow~~
- Connect your devices make sure developer options is enable with USB Debugging
    - If the sites doesnt recognize your phone and you dont see a prompt to acept the key there is a chance your device is connected to your local `adb` 
        - Run `adb kill-server` and reconnect your phone to the computer.
- Select the device in the UI
- Check box your wanted options - **I leave everything unchecked - only check if you know what you are doing**
- Click **Install Build** and follow the instructions
- Should take a cuple of minutes depends on your internet speed. make sure to leave your devices connected until the install is done!!

Great now your phone is updated 😎 time to add the Magisk Patch to gain back the root access.

### Install Magisk patch

- Download the firmware and extract the `init_boot.img` file:
    - this usually will be inside the zip file called called something like `"image-[BUILD_NUMBER].zip"`
- Connect your phone - make sure USB Debugging is enabled.
```bash
adb push init_boot.img /sdcard/
```
- this will push the img file to the home directory of your phone so it will be easy to find in the magisk app.

