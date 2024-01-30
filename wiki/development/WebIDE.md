---
title: ADB and WebIDE
parent: Sideloading and debugging
nav_order: 1
layout: default
last_modified_date: 2023-11-28
---
# ADB and WebIDE
{:.no_toc}

Table of Contents
{:.text-delta}
- TOC
{:toc}

{:.warning}
> KaiOS 2.5 only. To sideload apps on debug-enabled KaiOS 3 devices, follow the instructions on using KaiOS's in-house `appscmd` on [the official Developer Portal](https://developer.kaiostech.com/docs/sfp-3.0/getting-started/env-setup/os-env-setup).

According to [How-To Geek](https://www.howtogeek.com/773639/what-is-sideloading-and-should-you-do-it), sideloading is 'the practice of installing software on a device without using the approved app store or software distribution channel'. This can be useful if you want to use an app that is either not eligible for distributing over KaiStore, not available in your region, or if you want to test an app that you are developing.

This is where Android Debug Bridge (ADB) and WebIDE come in. Inherited from the now-defunct Firefox OS, WebIDE allows you to manage installed applications and configurations on KaiOS phones. It works by communicating with a specific port on your phone over ADB, an internal protocol for engineers usually found on Android devices.

Before you ask: no, despite using Android compatibility layer for hardware support, KaiOS isn't Android and cannot run APKs. It uses Gecko the browser engine for rendering apps, and they typically come in the form of ZIP archive files, which consists of HTML, styling and JavaScript code for functionality.

## Sideloading 101
### What we'll need
- a computer with command-line tool installed: Command Prompt on Windows, Terminal on macOS/Linux
- [a debug-enabled phone running KaiOS 2.5]({% link devices.md %})
- an USB cable with data transferring
- an Internet connection to download tools and navigate to W2D (optional if there are debug codes)
- an archive extractor installed to extract our tools:
  - on macOS/Linux, use Finder, built-in file manager or `unzip`;
  - on Windows, use [7-Zip](https://www.7-zip.org) or WinRAR if you prefer
- [Android Developers' SDK Platform Tools](https://developer.android.com/tools/releases/platform-tools) or install ADB via your package manager (we'll guide you below)
- [Waterfox Classic](https://classic.waterfox.net): most up-to-date pre-Photon fork of Firefox with WebIDE
- most importantly, computer skills and patience

*Need a video tutorial? If you're on Linux, KaiOS Technologies officially made one for their own WebIDE client KaiOSRT which can be found [here](https://www.youtube.com/watch?v=wI-HW2cLrew). Alternatively, there's also one on BananaHackers' YouTube channel [here](https://www.youtube.com/watch?v=SoKD7IBTvM4).*

<div class="w2d">
  <img width="100%" alt="Demostration of the W2D website opened in KaiOS browser, with a huge Launch developer menu button shown in front" src="../assets/webide/w2d.jpeg">
  <p class="fs-2"><em>W2D website</em></p>
</div>

### Turn on debugging mode on your phone
1. Check whether your phone can be debugged and any special notes to follow on the [Devices page]({% link devices.md %}).
   - Some may have specific codes that can be dialed to quickly activate debugging mode, i.e. `*#*#33284#*#*` for Nokia devices and both `*#*#33284#*#*` and `*#*#0574#*#*` for Energizers and others. Details can be found on each device page.
2. Navigate to https://w2d.bananahackers.net using default Browser on the phone. Use D-Pad keys to move the cursor and click on the big front <kbd>Launch Developer menu</kbd> button.
3. In the newly opened Developer menu, select the first <kbd>Debugger</kbd> option, then <kbd>ADB and DevTools</kbd> from the dropdown menu. You should see a bug icon in the status bar letting you know ~~your phone has bugs inside~~ you're in debugging mode.
4. If you're connecting to a Linux-based PC, you may need to go to Settings, Storage and turn on <kbd>USB Storage</kbd> for `udev` to properly register your phone as an USB peripheral. An icon in the status bar will appear indicating storage access via USB.
   - If you need to skip this step, feel free to go through the painstaking [Setting up USB access on Linux](#setting-up-usb-access-on-linux) process below.

<p align="center">
  <img width="240" alt="Demostration of the Debugger menu with three options Disabled, ADB only and ADB and DevTools shown. The last is highlighted and selected. An icon in shape of a bug can be seen in the status bar" src="../assets/webide/developer_menu.jpeg">
  <img width="240" alt="Demostration of the Storage page within Settings where the USB Storage option is highlighted and shown as Enabled. An icon in shape of the USB logo can be seen in the status bar" src="../assets/webide/usb_storage.jpeg">
</p>

5. Connect the phone to your computer with the USB cable.
{:style="counter-reset:none"}

### Download and set up ADB
> Now, if your operating system has a package manager, you can utilize that to quickly install and set up ADB:
> * Windows: `choco install adb` 
> (`winget` unfortunately [prohibits installing executables with symlinks](https://github.com/microsoft/winget-pkgs/issues/4082))
> * macOS: `brew install android-platform-tools`
> * Linux (Debian/Ubuntu): `sudo apt-get install adb fastboot`
> * Linux (Fedora): `sudo dnf install android-tools`
> * Linux (Arch): `sudo pacman -S android-tools`
> 
> Skip to next part when you're done.

6. On your computer, visit [Android Developers' SDK Platform Tools](https://developer.android.com/tools/releases/platform-tools) website and click on the link correspond to your operating system under the Downloads section. Read the terms if you want to, tick the box and click the green button to have the SDK downloaded to your computer.
{:style="counter-reset:none"}

![Screenshot of Android Developers' SDK download page with download links for three operating systems under the Downloads section](../assets/webide/sdk_website.png)

7. Extract the downloaded archive to a folder (double-click the file on macOS/Linux, 7-Zip > <kbd>Extract here</kbd> on Windows), navigate to its `platform-tools` root and open a command-line window by that directory.
{:style="counter-reset:none"}

8. Type `adb devices` to start the ADB binary server. ADB will automatically detect all devices with active debugging mode connected to the computer over USB. If a `device` shows, you're good to go! Otherwise, go back, check if you've missed any steps or whether [your phone supports ADB]({% link devices.md %}).
{:style="counter-reset:none"}
   - Note that if you're unable to run `adb`, you may need to make it an executable: `chmod +x ./adb`

```
$ adb devices
* daemon not running; starting now at tcp:5037
* daemon started successfully
List of devices attached
1a2b3c4d	device
```

9. If you use other WebIDE clients, or if you have trouble connecting later on as `adbd` fails to detect your phone, forward ADB access to TCP socket 6000 for debugging:
{:style="counter-reset:none"}

```
$ adb forward tcp:6000 localfilesystem:/data/local/debugger-socket
6000
```
*Tip: If you've downloaded the SDK package from Android Developers' website, for quicker access next time, include the extracted ADB folder in PATH. We won't cover this here as this would be a lengthy process. This will be automatically handled if you've installed ADB via package manager.*

<details>
  <summary>Connect to ADB over Wi-Fi</summary>
WIP
</details>

### Connect to WebIDE

10. We'll use [Waterfox Classic](https://classic.waterfox.net) for WebIDE (Firefox 59 and Pale Moon <28.6.1 will also do the job just fine). To download, head to the browser's homepage, download and install the version correspond to your OS.
{:style="counter-reset:none"}

![Screenshot of Waterfox Classic browser's homepage with blue download buttons for three operating systems at the middle of the page](../assets/webide/waterfox_classic.png)

11. Open Waterfox Classic and press the hamburger menu button at the right end of the toolbar, click the <kbd>Developer</kbd> entry (tenth option from top to bottom, left to right), then click <kbd>WebIDE</kbd>.
{:style="counter-reset:none"}

<div class="altf8">
  <img width="100%" alt="Demostration of the main menu sliding out to show the Web Developer submenu, with WebIDE highlighted as the tenth option from top to bottom" src="../assets/webide/waterfox_classic_dev.jpeg">
  <p class="fs-2"><em>Tip: For quicker access to WebIDE, press its shortcut <kbd>Shift</kbd> + <kbd>F8</kbd> while you're in the browser.</em></p>
</div>

12. Your phone's name should appear in the right pane as the first option under USB Devices section. Click it to connect. If you don't see any, click <kbd>Remote Runtime</kbd> in the right pane, leave it as default at `localhost:6000` and press OK. If you still cannot connect your phone to WebIDE, check if you've missed any steps or whether [your phone allows DevTools]({% link devices.md %}).
{:style="counter-reset:none"}

![Screenshot of WebIDE interface with Remote Runtime pop-up shown after pressing the option in the right pane. The pop-up has 'localhost:6000' as the content of the input box, with two buttons to confirm or close.](../assets/webide/localhost_6000.png)

*If you're using other means to access WebIDE such as Firefox v59 or Pale Moon <28.6.1, you may now see a warning header about mismatched build date. You can safely ignore it as WebIDE was mainly designed to support Firefox OS device builds released alongside that Firefox/Pale Moon versions.*

### Ready to sideload apps

{:style="counter-reset:none"}
13. To sideload an app, download it (you can find lots of great apps on [BananaHackers Store](https://store.bananahackers.net) and GitHub!) and extract its ZIP content (if you see an OmniSD-packaged `application.zip` you may need to extract that too).

14. Select <kbd>Open Packaged Apps</kbd> in WebIDE's left sidebar (second option from top) and navigate to the root of the app folder you just extracted.

15. Once you've got the app loaded, press the triangle <kbd>Install and Run</kbd> in the top bar to sideload!

![Screenshot of WebIDE interface with an app selected. The triangle Install and Run button (first one left to right) is being highlighted on the top pane](../assets/webide/install_and_run.png)

> If you encounter an issue in a sideloaded app and want to debug, click the wrench to open the Developer Tools.

## Other WebIDE alternatives
* [KaiOS RunTime](https://developer.kaiostech.com/docs/02.getting-started/01.env-setup/simulator) (Linux): official developing environment for KaiOS 2.5 made by KaiOS Technologies the company. 
  - To download and set up KaiOSRT on Ubuntu, type these commands one-by-one in Terminal:

```
wget https://s3.amazonaws.com/kaicloudsimulatordl/developer-portal/simulator/Kaiosrt_ubuntu.tar.bz2
tar -axvf Kaiosrt_ubuntu.tar.bz2
cd kaiosrt-v2.5-ubuntu-20190925163557-n378
tar -axvf kaiosrt-v2.5.en-US.linux-x86_64.tar.bz2
cd kaiosrt
./kaiosrt
```
*It's also possible to get KaiOSRT to work on Windows 10 and later using Windows Subsystem for Linux (WSLg). [See this video on YouTube for action](https://youtu.be/eg2SOCTMxYU).*

* Firefox 59 (ESR 52.9): the last official Firefox version to bundle with working WebIDE and other tools for development on Firefox OS devices, before Mozilla decided to kill the project in 2016. Archives of all Firefox releases can be found [here](https://archive.mozilla.org).
* Pale Moon 28.6.1 (Windows/Linux): a popular fork of Firefox with older user interface, legacy Firefox add-on support and always running in single-process mode. Archives of all releases can be found [here]( https://www.palemoon.org/archived.shtml).
* jkelol111's [Make KaiOS Install](https://github.com/jkelol111/make-kaios-install): another command-line tool to install apps using KaiOS's remote debugging protocol.

## Setting up USB access on Linux
Dedicated to those adrenaline-fueled who want to complicate their lives.

1. Download and install `51-android.rules` by typing this long streak of command:

```
$ wget -S -O - https://raw.githubusercontent.com/cm-b2g/B2G/1230463/tools/51-android.rules | sudo tee >/dev/null /etc/udev/rules.d/51-android.rules; sudo udevadm control --reload-rules
```
2. Plug your phone to the computer using an USB cable and obtain the Vendor ID of the phone:
{:style="counter-reset:none"}

```
$ lsusb
Bus 001 Device 007: ID 05c6:f003 Qualcomm, Inc. Nokia 8110 4G
                       ^^^^
```
In our case, the Qualcomm-based 8110 4G has the Vendor ID of `05c6`.

3. Open `/etc/udev/rules.d/51-android.rules` in your preferred text editor ***as root***. Append this line, replace `05c6` with the Vendor ID you got above:
{:style="counter-reset:none"}

```
SUBSYSTEM=="usb", ATTR{idVendor}=="05c6", MODE="0664", GROUP="plugdev"
```

4. Execute this command ***as root*** to make `51-android.rules` read-only for all users on the system:
{:style="counter-reset:none"}

```
$ sudo chmod a+r /etc/udev/rules.d/51-android.rules
```

5. Now, no longer as root, create `~/.android/adb_usb.ini` in your HOME directory. Open it using your preferred text editor and put the obtained Vendor ID value in HEX: `0xABCD`, whereas `ABCD` is Vendor ID
{:style="counter-reset:none"}

6. Re-run `adb devices`.

<style>
  .w2d {
    @media (min-width:1100px) { width: 265px; float: right; padding: 0 0 30px 25px }
    margin: 0 auto; max-width: 240px;
  }
  .w2d p { margin: 0; padding: 0 }
  .altf8 { max-width: 485px; margin: 0 auto }
  .altf8 p { margin: 0; padding: 0 }
</style>