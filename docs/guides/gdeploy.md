---
title: gdeploy
parent: Sideloading and debugging
layout: default
nav_order: 2
---

`gdeploy` is a small cross-platform command-line utility developed by Luxferre as an alternative to the graphical WebIDE, and can even be used as NodeJS module/library. According to Luxferre, 'it uses the same `firefox-client` backend but has much simpler architecture for application management'.

For Windows 10 version 1709 and later, type these commands one by one into Command Prompt, with [DIR_PATH] replaced by the extracted folder directory of the app you want to install (see step 8 above):

```console
winget install Git.Git
winget install OpenJS.NodeJS.LTS
cd /d "%USERPROFILE%\Desktop"
git clone https://gitlab.com/suborg/gdeploy.git
curl -Lo platform-tools.zip https://dl.google.com/android/repository/platform-tools-latest-windows.zip
tar -xf platform-tools.zip
cd platform-tools\
adb devices
adb forward tcp:6000 localfilesystem:/data/local/debugger-socket
cd ..\gdeploy\
npm i && npm link
gdeploy install [DIR_PATH]
```

For macOS and Linux, if you have Homebrew installed as a package manager:

```console
brew install git node android-platform-tools
cd ~/Desktop
git clone https://gitlab.com/suborg/gdeploy.git
adb devices
adb forward tcp:6000 localfilesystem:/data/local/debugger-socket
cd gdeploy
npm i && npm link
gdeploy install [DIR_PATH]
```
