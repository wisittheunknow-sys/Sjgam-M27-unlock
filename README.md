<p align="center">
  <img src="teardown_photos/IMG_20260705_162503_260.jpg" width="600">
</p>

# Sjgam-M27-unlock
Community-driven reverse engineering project for the SJGam M27 handheld console. Exploring the hidden Android 4.4 system and its RK3188 chipset (yes, really...), firmware internals, hardware interfaces, and custom software possibilities.

# OpenM27

The SJGam M27 is a 7 inch emulation handheld built on top of a heavily stripped-down Android 4.4 system running on Rockchip hardware Rk3188.

This project aims to document the hardware and software architecture of the console and explore possibilities such as:

- Accessing the hidden Android environment
- Launcher replacement
- ADB restoration
- Custom firmware development
- Hardware documentation
- Alternative operating systems

## Current Status

### factory Check access
- press select and (A,B,X,Y) in the original template launch testmode.apk

### Hardware access
- Loader mode accessible using `VOL-` during boot.
- Full NAND backup successfully dumped using Rockchip tools.
- Console remains recoverable even after corrupted firmware flashes.

### Firmware analysis
- Complete partition dump obtained:
  - `boot.bin`
  - `kernel.bin`
  - `system.bin`
  - `userdata.bin`
  - `recovery.bin`
  - ...

### Android discovery
- Hidden Android 4.4.2 environment confirmed.
- `GameTemplate.apk` identified as the main launcher/frontend.
- Removing `GameTemplate.apk` boots directly into Android.

### Custom software
- Custom APK installation through `system.bin` modifications works.
- `ATV Launcher` works correctly.
- `Total Commander` works correctly.
- Third-party applications can be installed and launched.

### Reverse engineering
- `testmode_r10.apk` analyzed.
- Hardware GPIO access discovered:
  - `gpio169`
  - `gpio264`
- Hardware diagnostics application identified.

### USB investigation
- `adb` binary found in `/system/bin`.
- `adbd` daemon found in `/sbin/adbd` inside boot ramdisk.
- Boot configuration already contains:
  - `ro.debuggable=1`
  - `persist.sys.usb.config=adb`
- ADB still not visible over USB.
- Current hypothesis: missing Android USB gadget driver or disabled USB gadget subsystem.

### Alternative firmware experiments
- RK3188 Android images partially boot on the device.
- Generic ARM SD card boot attempts unsuccessful.
- Device appears to boot exclusively from internal NAND/eMMC.

### Current objectives
- Restore ADB access.
- Enable a TV-compatible virtual keyboard.
- Obtain local shell access.
- Investigate possibility of rebuilding a more complete Android environment.
