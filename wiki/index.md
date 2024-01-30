---
title: Home
layout: home
nav_order: 1
last_modified_date: 2023-12-09
---
# Welcome to KaiOS Wiki!
{:.no_toc}

This is a fork of [BananaHackers Wiki hosted on Wiki.js](https://wiki.bananahackers.net), hosted on GitHub Pages for accessibility.

You may want to:
- [check whether your KaiOS phone is debug-enabled]({% link devices.md %})
- [learn how to sideload third-party apps on your KaiOS phone]({% link sideloading/sideloading.md %})

{: .warning }
> 1. All information and resources on this website are provided on an as-is basis, free at no costs and publicly available to everyone. We currently are NOT operating any services for e.g. injecting third-party apps via KaiStore's Developer Portal (it's against their ToS) or modifying the operating system. Beware — anyone charging you for such things may be SCAM!
> 2. Tempering with system software or hardware can potentially damage your device and effectively void its warranty. Some of our guides might be forbidden by your local law. **By proceeding, you acknowledge & accept all risks associated with such actions.**
> 
> **We will NOT take any responsibility for any damage or loss that may result from modifying your phone.** It is yours to ensure that you follow all instructions carefully and take appropriate precautions to protect your phone.

Frequently Asked Questions
{: .text-delta }
- TOC
{:toc}

## WhatsApp
### Why can't I send and receive files larger than 8MB?
This is to avoid 'out of memory' errors with the nature of WhatsApp's encryption. All things sent through the app's servers – including photos and videos – are encrypted on device, and to decrypt them bit-by-bit would take huge chunks of memory, which isn't suitable for KaiOS devices, having hardware as limited as 256MB of RAM.

The only workaround is to ask the other person to send the file through a different service. Since each chat thread in WhatsApp is encrypted with unique keys, it's not possible to forward the file to another person without decrypting and re-encrypting it.

### Can I pair WhatsApp on KaiOS with WhatsApp Web?
Unlike the version of WhatsApp on Android and iOS, the KaiOS version of WhatsApp is currently NOT capable of pairing your account with the web interface or desktop applications.

No reasons have been officially stated on this, but [the description of WhatsApp about the feature](https://blog.whatsapp.com/whats-app-web) highly suggests that this is due to KaiOS devices' limitations on background processes and battery life, which prevents the feature from syncing decryption keys and mirroring messages & calls from your phone.

On a related note, you cannot sign into another device, pair with those interfaces and then sign into the KaiOS version of WhatsApp. Attempting to do so will result in the renewal of the decryption keys and all other devices being forced to log off automatically.

## Apps and games
### Is the X app available on KaiOS?
- *Facebook, WhatsApp*: Both are available to download from KaiStore on KaiOS 2.5, and NOT available on KaiOS 3. However, with Facebook, you can use the browser to access the mobile version of the service.
  - **Why are apps like WhatsApp available on v2.5 but not v3?** v3 isn't made available in India where WhatsApp plays a crucial role in small and medium business, ever since Jio, a major network carrier in the country, dropped KaiOS in favor of Android Go; while JioPhones with v2.5 were more successful and an oppotunity for Facebook/Meta to bring their services to the masses.
  - v3 devices are currently only sold in the US where Apple's iMessage service and SMS are dominating, and 'it makes little sense to introduce [WhatsApp] solely for there' ([source](https://reddit.com/r/KaiOS/comments/13m6l0h/_/jkwr0sy/?context=1))
  - v3 also features a huge overall redesign, with support for new APIs and hardware interactions, meaning that apps have to be reworked to support the new version. As WhatsApp relies heavily on device APIs, that would create an enormous work for the WhatsApp team to figure out.
  - For KaiOS apps in general, while devices running v3 are sold in the US, it is not available elsewhere for international developers, who made up most parts of KaiStore, to port their apps on. They can only rely on KaiOS's emulators which is missing many of the APIs and functionalities that physical devices have. Physical devices, even then, are essentially locked down by OEMs & developers can only test apps via Submission Portal and hope for the best.
- *Spotify*: NOT available on KaiOS, due to the OS not capable of processing Widevine DRM to decode and play songs from the service. Not to mention term violations and copyright infringements with third-party implementations, on which the company is really strict.
- *Uber*: Mobile web version can be accessed on KaiOS 3, and NOT available on KaiOS 2.5. If you live in the US, the service recently allows you to call to book.
- *Instagram*: Mobile web version can be accessed on KaiOS 3, and NOT available on KaiOS 2.5. Facebook/Meta doesn't open any public APIs to make third-party implementations possible, and restricts such actions via their Terms of Services.
- *Google Duo*: Available to download from KaiStore on selected KaiOS 2.5 devices, such as Nokia 8110 4G and Energizer E241s; others can access by visiting this address in the browser and select Options > Pin to Apps Menu for quicker access, or sideload from BananaHackers Store.

For other apps, look for them in KaiStore and BananaHackers Store. If they're not there, they're not available on KaiOS, either due to ToS violations or developers not being aware of them.

### Can I run Java apps and games on KaiOS?
NO, at least not natively. KaiOS, as it's based on web technologies, can only runs apps made in HTML5, CSS and JavaScript, and does not have the APIs to run apps made with Java 2 Micro Edition (J2ME) technologies.

However, same as on Android, you can run them in emulators. There are 2 ways to emulating J2ME apps on KaiOS devices: Luxferre's abandoned [Project KAVA](https://gitlab.com/suborg/project-kava/), and openGiraffes' reworked [Mozilla PluotSorbet](https://github.com/openGiraffes/pluotsorbet-kaios-template). They don't run very well, have many issues and barely work if you're trying to run a graphic-intensive game or an app that heavily relies on real device APIs.

By clicking the links, you'll be taken to their respective GitLab/GitHub repositories where you can find more information and instructions on running them.

### Opening KaiStore stucks at 25%/69%, or results in "Connection error"
- 25%? KaiStore is having a hard time setting up the connections to its servers. Double-check your Internet connection and try again.
- 69%? KaiStore can connect to the servers, but it might have been unable to retrieve the categories and list of apps, most likely due to cache problems. Just like your brain's short-term memory, caches can be misconstrued, so why not give it a fresh new state. Open Settings, then under the Privacy & Security tab, choose Browsing privacy, and Clear Cache and Saved Data. Note that this will log you out of some apps.
- 'Connection error'? In most cases, the servers for KaiStore are currently going down at the moment. KaiOS team should be looking into that immediately, and try to get it back up and running in a few hours or so. Have a cup of coffee and enjoy the rest of the day.

## General availability
### Has any KaiOS 3 devices come to markets outside the US yet?
NO. But you can import one unlocked, such as the Nokia 2780 Flip, on Amazon or eBay and it'll work with European LTE bands, with full call, message and data support, as confirmed by u/JoTheShmo, u/canegiallodoppiacoda and u/FarCaptain7820.

Do note that the phone is specifically tailored to the US market, so you'll have to live with the limited display and T9 predictive languages of English (US) and Español (Spanish – US).

There's also been some news from the Japanese publishing company ASCII, who got in contact with Orbic's EVP Global Strategy and Operations Danny Adamopoulos at CES 2023, that Orbic will bring their Verizon's Journey V to Japan with KaiOS 3.1 instead of AOSP.

If you have more information, please notify me and I'll update this ASAP.

### Can I update my KaiOS 2.5 phone to KaiOS 3, or any newer versions of KaiOS? If so, when can I expect an update?
NO. While it's technically possible to port some of the latest features in later KaiOS versions to older ones, some new stuff in each version need older phone hardware to be reworked to adapt (i.e. v3 updated and completely redesigned its Android 10 Gonk layer, changing how the phone hardware can interact with the operating system).

Adapting to any of these changes means some maintenance costs and efforts for OEMs, which is not economical considering how little KaiOS phones cost.

> There's test & validation cost on the OEM side, then support cost (because some updates fail), sometimes indeed some carrier cost. (...) That [update to KaiOS 3] requires chipset vendors and OEM development and QA, [all of which are] very hard to justify on low margin products.
> — Fabrice Desré, Chief Architect of KaiOS Technologies ([source](https://discord.com/channels/472006912846594048/472006912846594050/906408683339124756))

### What has changed in KaiOS 3 over KaiOS 2.5?
Here's a great summary from u/canyouswim73 (taken from this post):

> v3.x is a generational difference from v2.x. it is a complete rewrite of the OS to support a newer underlying infrastructure. Specifically, v2.x and earlier of the OS are based on Firefox v48, which is very old. this is why it is slow (mostly), and why there are other limitations in what the OS can do, specifically when browsing the web. Going to v3.x they have changed the underlaying version of Firefox to v84, which is much more recent and adds many of the new web features we have come to expect (but still no DRM, so no Spotify or similar).
> 
> so, with that out of the way, there are a few other key differences you'll notice:
> 
> - v3.x phones have a bit faster processor on them, and the underlaying OS is itself faster, so the overall experience is faster
> - all apps from the appstore need to be upgraded by their developer to move from v2.x to v3.x compatibility. for this reason the v3 appstore is much less populated (for now) than the v2.x appstore. May of the core apps are there, however, at this point
> - regarding apps, though - no whatsapp for v3.x yet
> - the v3.x OS has addressed a handful of common complaints from earlier versions, including the issue with group texting, some improvements to the custom predictive text dictionary, and some other small odds and ends

If you want to learn more about the update, here are a few bookmarks:
- [Help Center: Key updates on KaiOS 3.0](https://www.kaiostech.com/help-center/key-updates-on-kaios-3-0/)
- [Help Center: Apps on KaiOS 3.0](https://www.kaiostech.com/help-center/apps-on-kaios-3-0/)
- [Developer Portal: KaiOS 3 Overview](https://developer.kaiostech.com/docs/sfp-3.0/introduction/overview)