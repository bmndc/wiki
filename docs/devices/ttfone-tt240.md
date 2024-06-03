---
title: TTfone TT240
parent: Devices
layout: default
nav_exclude: true
last_modified_date: 2024-06-02

released: "27 November 2020"
model: "FS361"
soc: "Spreadtrum SC7731E (4 × 1.3GHz Cortex-A7)"
ram: "512MB LPDDR3"
gpu: "Mali-400 MP1"
storage: "4GB (+ up to 32GB microSDHC slot)"
network: >
    2G GSM, 3G UMTS<br>
    Single SIM (standard SIM)
screen: "320 × 240 (167 PPI), 2.4 inches QVGA TFT LCD"
bluetooth: "4.0, A2DP"
wifi: "802.11b/g/n, Hotspot (up to 8 devices)"
peripheral: "GPS &amp; GLONASS"
camera: >
    Rear: VGA with fixed focus, LED flash<br>
    Front: VGA with fixed focus
dimension: "123 × 52 × 12 (mm) 4.84 × 2.05 × 0.47 (in)"
weight: "With battery: 99 g (3.49 oz)"
port: >
    - microUSB charging &amp; USB 2.0 data transferring port<br>
    - 3.5mm headphone jack
battery: "Removable Li-Ion 1400mAh (up to 11d 16h of standby advertised)"
kaios_ver: "KaiOS 2.5.1.1"
wavoip: "Not supported"
buildno: "I324MS_TTFONE_V05-030323"
---
# TTfone TT240
{:.no_toc}

{% include spec.html %}

Table of Contents
{: .text-delta }
- TOC
{:toc}

*.yarnamite in our Discord server contributed to this documentation.*

Amidst the concerns of the COVID-19 pandemic and the adoption of social distancing practices, TTfone saw an oppotunity for the elderly and disabled to get access to the Internet, seek the latest information and stay connected with relatives. This resulted in the release of the budget-friendly TT240 in November 2020. It features:
- a textured back and large T9 keys for comfy while holding, with ABS plastic shell for durability;
- VGA front camera for selfies and video calling

Reviews of the phone are critical: in active usage, the 1400mAh battery doesn't last very long.

## Secret codes
*Tip: You can save these codes as contacts for quick dialing later. When the phone suggests a saved code, you'll have to press Call to activate the code's function.*
- `*#*#33284#*#*`: Toggle debugging mode, allowing the phone to be accessed with ADB and DevTools. A bug icon will appear in the status bar letting you know debugging mode is on. This can also be turned on under Settings, Device, Developer, Debugger, ADB and DevTools.
- `*#*#0574#*#*`: Open LogManager utility which allows you to fully enable ADB and DevTools on certain Spreadtrum devices.
- `*#4224876#`: Toggle engineering mode, allowing privileged access (including rooted ADB shell) to the phone.
- `*#76809320#`: Display hardware information.
- `*#999*#`: Display the hardware revision.
- `*#06#`: Display the hidden International Mobile Equipment Identity number or IMEI to uniquely identify a specific cell phone on GSM networks. Do not show them to anyone else: they're crucial for calling functions on the phone.
- `*#07#`: Check the current SAR level and display SAR-related health and safety information.
- `*#23#` (call): Request your carrier to turn on [Call forwarding](https://en.wikipedia.org/wiki/Call_forwarding) service to forward a call to another number when yours isn't available. Requires PIN code to use. To toggle, go to Settings, Network & Connectivity, Calling, Call forwarding.
- `*#33#` (call): Check the [Call barring](https://www.communityphone.org/blogs/call-barring) service status from carrier for blocking or whitelisting calls, whether incoming or outgoing, domestic or international. Requires PIN code to use. To toggle, go to Settings, Network & Connectivity, Calling, Call barring.
- `*#43#` (call): Check the [Call waiting](https://en.wikipedia.org/wiki/Call_waiting) service status from carrier. To toggle, go to Settings, Network & Connectivity, Calling, Call waiting.
- `*#2886#`/`*#37*#`/`*#81#`: Open KaiOS MMI Test, an internal tool to test device hardware through an automatic routine or manually by hand: LCD backlight, T9 keyboard, camera, LED flash, RTC, speaker, microphone, vibrator, 3.5mm audio jack, SIM trays, Wi-Fi, Bluetooth, NFC, microSD and microUSB slots etc.

**Code that doesn't work**
- `*#0606#`: Display the Mobile Equipment Identifier (MEID) number to uniquely identify a specific cell phone on CDMA networks. This phone doesn't operate on CDMA, thus the MEID is undefined.
- `*#8378269#`/`*#*#2637643#*#*`: Open Testbox engineering menu with predecessor Firefox OS design, usually used by OEMs to test various hardware of the phone. This menu can be manually opened using Luxferre's [CrossTweak](https://gitlab.com/luxferre/crosstweak).
- `*133#`: Should obtain APN information from carrier.

## Special boot modes
- **Recovery mode**: With the device powered off, hold both Power/End call and * keys, or type `adb reboot recovery` when connected to a computer. Allows you to factory reset the device by wiping /data and /cache, view boot and kernel logs, and install patches from `adb sideload` interface or SD card.

## Sideloading and debugging
See [Sideloading and debugging/WebIDE]({% link development/webide.md %}).

## ROOT
To get read/write ADB access to the phone's filesystem, download and run Wallace Spreadtrum KitKat from [old B-Hackers Store](https://sites.google.com/view/b-hackers-store/home/settings). If you run into `NoModificationAvailableError`, reboot the phone and re-run the utility again.