# 2021-samsung-galaxy-nexus-i9250-tuna-maguro

This document describes how to install on Samsung Galaxy Nexus
a decently up-to-date version of Android able to install apps requiring Google Play Store
as of Mar 2021.

## Specs

[GSMArena](https://www.gsmarena.com/samsung_galaxy_nexus_i9250-4219.php).

## Factory

Latest image: [Google, 4.3 (JWR66Y)](https://developers.google.com/android/images#yakju).

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
