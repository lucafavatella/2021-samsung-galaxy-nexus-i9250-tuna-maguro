# 2021-samsung-galaxy-nexus-i9250-tuna-maguro

This document describes how to install on Samsung Galaxy Nexus
a decently up-to-date version of Android able to install apps requiring Google Play Store
as of Mar 2021.

## Specs

[GSMArena](https://www.gsmarena.com/samsung_galaxy_nexus_i9250-4219.php).

## Install Factory Image

Latest image: [Google, 4.3 (JWR66Y)](https://developers.google.com/android/images#yakju).
Includes:
* Booloader - to be installed by `fastboot -v flash bootloader bootloader-maguro-....img`.
* Radio - to be installed by `fastboot -v flash radio radio-maguro-....img`.
* Boot, recovery, system, userdata - to be installed by `fastboot -v -w update image-....zip` (that also wipes userdata).

Before installing the image,
unlock the bootloader by `fastboot -v oem unlock` (also erases data),
finally lock it again by `fastboot -v oem lock`.

For good measure, reboot after each step by `fastboot -v reboot-bootloader`.

## Custom System and Recovery

[TWRP recovery](https://dl.twrp.me/maguro/) (unmaintained after 3.4.0).

LineageOS support (unmaintained):
[info](https://wiki.lineageos.org/devices/maguro),
[installation](https://wiki.lineageos.org/devices/maguro/install),
[Google apps as Open GApps](https://wiki.lineageos.org/gapps.html).

Unlegacy Android (apparently unmaintained):
[based on Android 7.1](https://builds.unlegacy-android.org/aosp-7.1/tuna/),
with latest build from June 2020;
[XDA thread](https://forum.xda-developers.com/t/rom-aosp-4-4-6-0-7-1-unlegacy-android-project.3334574/).

DivestOS (unofficial fork of LineageOS) - system and recovery:
[based on LineageOS 14.1 (based on Android 7.1)](https://divestos.org/index.php?page=devices&base=LineageOS#device-maguro),
apparently built monthly;
[XDA thread](https://forum.xda-developers.com/t/rom-divestos-14-1-for-maguro-toro-toroplus.4249415/).

### GApps

Open GApps:
[pico](https://github.com/opengapps/opengapps/wiki/Package-Comparison),
[FAQ on devices with system partition of 1GB or less](https://github.com/opengapps/opengapps/wiki/FAQ#11-open-gapps-install-failed-with-the-message-insufficient-storage-space-available-in-system-partition-my-device-has-16gb-or-more-of-storage-available-how-can-this-be),
[`gapps-config.txt`](https://github.com/opengapps/opengapps/wiki/Advanced-Features-and-Options#gapps-config-file-location).

Resizing the system partition at the expense of either the data partition or the cache one
is complex,
may require binaries usually not in recoveries (e.g. `parted`),
may require rework when re-flashing or updating system (unclear, anecdotal evidence).

## Install decently up-to-date Android

Wipe / format device at will.
For each partition:
* Power off.
* Boot to bootloader
  by pressing volume up&down and power button.
* Boot TWRP recovery
  by `fastboot -v boot twrp-3.4.0-0-maguro.img`.
* Wipe / format partition.

Install factory image.

Check that factory image boots.
If it does not (e.g. glowing X logo),
boot TWRP recovery and look for any errors
when mounting / wiping / formatting / resizing
any partitions / filesystems;
depending on errors may include also creating folder.

As per DivestOS documentation,
unlock bootloader,
flash DivestOS recovery,
sideload DivestOS package.
Do not sideload GApps
(for signature verification error, rather boot TWRP - see below).

Boot (not flash) TWRP recovery,
attempt to sideload ARM pico Open GApps: will err for lack of space.
Read the log file referred to by the error,
create minimum `gapps-config.txt` in the same folder:
```
Include
Core
```
Attempt to sideload ARM pico Open GApps: will err for lack of space.
Find the largest APKs in the system partition that can be installed from F-Droid
(e.g. FairEmail, Simple Gallery, Silence),
and delete their folders (or move them to the data partition).
Attempt to sideload ARM pico Open GApps: shall succeed.

Lock booloader.

Check that it boots.
