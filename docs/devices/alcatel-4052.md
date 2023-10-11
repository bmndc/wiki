---
title: Alcatel GF3/SMARTFLIP
parent: Devices
layout: default
nav_order: 9
---
# Alcatel Go Flip 3 (4052woz)
{: .no_toc }
*also known as Alcatel SMARTFLIP (4052rc)*

<details markdown="block">
  <summary dir="rtl">View device specification table</summary>
<table>
  <thead><tr><th colspan="2">Alcatel Go Flip 3/SMARTFLIP (4052crowz)</th></tr></thead>
  <tbody>
    <tr><td>Announced</td><td>17–19 September 2019</td></tr>
    <tr><td>Released</td><td>27 September 2019</td></tr>
    <tr><td>Model</td><td>4052r (AT&T), 4052w (T-Mobile), 4052c (Cricket), 4052z (Metro by T-Mo), 4052o (Rogers/Canada)</td></tr>
  <tr><td colspan="2"><strong>Specifications</strong></td></tr>
    <tr><td>SoC</td><td>Qualcomm MSM8909 Snapdragon 210<br>(4 x 1.1GHz Cortex-A7)</td></tr>
    <tr><td>RAM</td><td>512MB LPDDR3</td></tr>
    <tr><td>GPU</td><td>Adreno 304</td></tr>
    <tr><td>Storage</td><td>4GB (+ up to 32GB microSDHC card)</td></tr>
    <tr><td>Network</td><td>2G GSM, 3G UMTS, 4G LTE<br><em>+ 4052rc: band 2, 4, 5, 12 (MFBI), 14<br>+ 4052woz: band 2, 4, 5, 12, 25, 26, 41 (HPUE), 66, 71</em><br>VoLTE support with HD Voice (all models), VoWiFi support (4052woz only)<br>Single SIM (Nano-SIM)</td></tr>
    <tr><td>Screen</td><td>Main: 320 * 240 (143 PPI), 2.8 inches TN TFT LCD<br>External: 128 * 128 (125 PPI), 1.44 inches TN TFT LCD</td></tr>
    <tr><td>Bluetooth</td><td>4.1/4.2, A2DP</td></tr>
    <tr><td>Wi-Fi</td><td>802.11b/g/n, 2.4GHz, Hotspot (up to 8 devices)</td></tr>
    <tr><td>Peripherals</td><td>- GPS, GLONASS<br>- Speaker size: 0.7W (4052rc), 1W (4052woz)<br>- Dual microphones with noise cancellation</td></tr>
    <tr><td>Cameras</td><td>Rear: 2MP with fixed focus, LED flash, video recording 720p@30fps</td></tr>
    <tr><td>Dimensions<br>(HWD)</td><td>104.9 * 53.1 * 20.1 (mm)<br>4.13 * 2.09 * 0.79 (in)</td></tr>
    <tr><td>Weight</td><td>118 g (4.16 oz)</td></tr>
    <tr><td>Ports</td><td>- microUSB charging &amp; USB 2.0 data transferring port<br>- 3.5mm headphone jack</td></tr>
    <tr><td>Specials</td><td>M4/T4 hearing aid compatibility</td></tr>
    <tr><td>Battery</td><td>Removable Li-Ion 1350mAh<br>(up to 13.3 days of 4G standby advertised)</td></tr>
  <tr><td colspan="2"><strong>KaiOS info</strong></td></tr>
    <tr><td>Version</td><td>KaiOS 2.5.2</td></tr>
    <tr><td>WA VoIP</td><td>Not supported</td></tr>
    <tr><td>Build no.</td><td>N/A</td></tr>
  </tbody>
</table>
</details>

Table of Contents
{: .text-delta }
- TOC
{:toc}

In mid-September 2019, after a series of trial models, Alcatel launched "two" new flip phones in the US market, in partnership with T-Mobile and AT&T. Both the Alcatel Go Flip 3 and the Alcatel SMARTFLIP are affordable devices that support 4G LTE connectivity on each network. Running on the same KaiOS 2.5.2 as the internationally-acclaimed Nokia 2720 Flip, people in the US can now enjoy some of the best KaiOS features such as WhatsApp messaging and voice dictation with a simplified version of Google Assistant.

Note that despite having different names and [multiple variants being released under different carriers](https://www.reddit.com/r/dumbphones/comments/lu36eh/alcatel_go_flip_3_4052_o_variant/), all variants are basically the same device, with the receiving LTE bands tailored to each of the carriers.

## Tips and tricks
- To take a screenshot, press both * and # keys simultaneously.
- This phone includes a screen reader feature that's hidden by default, possibly because some third-party apps did not label their buttons correctly. To toggle the hidden Readout feature, press both the volume keys repeatedly until you hear a robotic sound.

## Secret codes
*Tip: You can save these codes as contacts for quick dialing later. When the phone suggests a saved code, you'll have to press Call to activate the code's function.*

Big thanks to [u/dhruvkar on Reddit](https://www.reddit.com/r/KaiOS/comments/hav4qp/comment/fv5lw7p/?context=3) for pulling the system apps on his SMARTFLIP and documenting this list of secret codes. Note that some codes here may not work in normal userspace: if you happen to also have a Go Flip 3 or SMARTFLIP and stumble when dialing any of these codes, please let me know!

- `*#*#33284#*#*`: Toggle debugging mode, allowing the phone to be accessed with ADB (more on this later). A bug will appear in the status bar letting you know debugging mode is on.
- `*#*#28865625#*#*`: Display a pop-up allowing you to enter Device unlock code to free the phone from network restrictions.
- `#865625#`/`#825625688#`: Attempt to unlock the phone from network restrictions.
- `*#*#3646633#*#*`: Switch network types between LTE, GSM, WCDMA and Automatic. This can also be toggled under Settings, Network & Connectivity, Mobile network & Data.
- `*#06#`: Display the hidden International Mobile Equipment Identity (IMEI) on GSM networks and SVN numbers. Do not show them to anyone else: they're crucial for calling functions on the phone.
- `##6343#`: Display the Mobile Equipment Identifier (MEID) number to uniquely identify a specific cell phone on CDMA networks.
- `*#07#`: Open More information page under Settings, Device, Device information.
- `*#16#`: Check the `ro.sar.enabled` property, if enabled check the current SAR level and display SAR-related health and safety information.
- `*#33#` (call): Check the [Call barring](https://www.communityphone.org/blogs/call-barring) service status from carrier for blocking or whitelisting calls, whether incoming or outgoing, domestic or international. Requires a 4-digit passcode to use. To toggle, go to Settings, Network & Connectivity, Calling, Call barring.
- `*#43#` (call): Check the [Call waiting](https://en.wikipedia.org/wiki/Call_waiting) service status from carrier. To toggle, go to Settings, Network & Connectivity, Calling, Call waiting.
- `*#2886#`: Open KaiOS MMI Test, an internal tool to test hardware performance of a KaiOS device through an automatic routine or manually by hand, including LCD backlight, T9 keyboard, camera, LED flash, RTC, speaker, microphone, vibrator, 3.5mm audio jack, SIM trays, Wi-Fi, Bluetooth, NFC, microSD and microUSB slots etc.
- `*#3228#`: Display internal version numbers of system partitions such as /boot, /system, /recovery, /modem and the bootloader.
- `*#4636#`: Display the production code, hardware revision and software build number.
- `*#7810#`/`##4382#`: Open Wireless Emergency Alerts settings under Settings, Network & Connectivity, allowing to toggle if you want to receive Required Monthly Test, Exercise Alert or Commercial Mobile Service Providers (CMSP) Alert from the government, specifically the Federal Emergency Management Agency.
- `*#*#825364#*#*`: Toggle Power Saving Mode under Settings, Device, Battery, which would turn off Wi-Fi, mobile data and Bluetooth to reserve remaining battery juice.
- `*#8378269#`/`*#*#2637643#*#*`: Open Testbox engineering menu with predecessor Firefox OS design,  usually used by OEMs to test various hardware of the phone.
- `###232#`: Check the total call duration since the phone was last turned on.
- `###3424#`: Open a menu, allowing to toggle Qualcomm diagnostic port and serial port for fixing null/invalid IMEI or baseband via QPST.
- `*#*#123321#*#*`: DM Configuration (?)
- `##66236#`: Edit DMAcc (?)

Codes that don't work/Unknown codes
{:.text-delta}
- `*#*#0574#*#*`: Open LogManager utility which allows you to fully enable ADB and DevTools on Spreadtrum devices.
- `*#*#212018#*#*`: Toggle privileged access (including rooted ADB shell) to the phone.
- `*#*#2887#*#*`
- `*#*#86583#*#*`
- `*#*#9663223#*#*`
- `*#22384#*`
- `*#573564#`

## Secret boot modes
- **Recovery mode**: With the device powered off, hold the Power/End call button and the Volume up key.
- **EDL mode**: With the device powered off, hold the Power/End call button and both the volume keys, then hold Volume up to enter Download mode upon confirmation. Allows you to read and write partitions in low-level with proprietary Qualcomm tools. Remove the battery to exit.