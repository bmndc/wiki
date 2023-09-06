---
title: Devices
layout: default
nav_order: 2
has_children: true
has_toc: false
---
# Devices

{: .note }
> - ✅ = debug-enabled out-of-the-box: open the phone's Browser, go to https://w2d.bananahackers.net and select *Launch Developer menu, Debugger, ADB and DevTools*
> - ⚠️ = needs additional work for debugging to work, see the phone's dedicated page for more information
> - 🔒 = currently debug-locked
> - ❓ = unknown (contribute by making a pull request, posting on Reddit or BananaHackers' Google Groups)

| Model name | KaiOS version | Debugging status | Note |
|:--|:--|:-:|:--|
| Nokia 8110 4G | 2.5.1 | ✅ |  |
| Nokia 2720 Flip | 2.5.2.2 | ⚠️ | Debug-enabled on 2.5.2, requires permanent root via boot partition modifying on 2.5.2.2 |
| Nokia 800 Tough | 2.5.2.2 | ⚠️ | Debug-enabled on 2.5.2, requires permanent root via boot partition modifying on 2.5.2.2 |
| Nokia 8000 4G | 2.5.4 | ✅ | No engmode-extension apps, requires boot partition patching to root |
| Nokia 6300 4G | 2.5.4 | ✅ | No engmode-extension apps, requires boot partition patching to root<br>(excl. TA-1324 not rootable due to different PK_HASH ⇒ no substitute loader) |
| Nokia 2720 V Flip | 2.5.4 | 🔒 | Rooting procedures should be the same as 8000 4G/6300 4G, but phone rejects patched boot image |
| Nokia 2760 Flip | 3.1 | 🔒 | ADB reports as unauthorized |
| Nokia 2780 Flip | 3.1 | ⚠️ | Custom firmware & manual injection to sideload, no debugging. ADB reports as unauthorized |
| CAT B35 | 2.5.1 | ⚠️ | Requires extracting using EDL and editing ADB hex on data partition |
| Energizer E241s | 2.5.1.2 | ✅ |  |
| Energizer E242s | 2.5.3.2 | 🔒 | Credits to u/CaramelSpoonful on Reddit for confirming |
| Energizer E280s | 2.5.3.2 | ✅ | Credits to u/gogolplex-pt on Reddit for confirming |
| Energizer E282sc | 2.5.3.2 | 🔒 | Credits to u/nicalejo on Reddit for confirming |
| Alcatel Go Flip 1/2 (4044v) | 1.0 | ✅ | After turning on debugging mode, dial ##3424# to enable serial port |
| Alcatel Go Flip 3 | 2.5.2 | 🔒 |  |
| Alcatel Go Flip 4 (4056W) | 3.0 | 🔒 | ADB reports as unauthorized.<br>Credits to u/tbrrss on Reddit for confirming |
| Alcatel MyFlip 2 (A406DL) | 2.5.4 | ✅ | No engmode-extension apps, no rooting |
| Alcatel 3088 | 2.5.1.1 | ✅ | W2D for debug mode |
| AT&T Cingular Flip IV (U102AA) | 2.5.3.1 | ✅ | No rooting (confirmed on 2.5.3) |
| AT&T Cingular Flex | 2.5.4 | ✅ | No engmode-extension apps, no rooting |
| AT&T Cingular Flex 2/<br>Cricket Debut Flex | 3.1 | 🔒 | ADB reports as unauthorized.<br>Credits to u/canyouswim73 on Reddit for confirming |
| TCL Flip Pro | 3.0 | 🔒 | ADB fails to detect device |
| myPhone Up Smart 3G | 2.5.1.1 | ❓ |  |
| myPhone Up Smart LTE | 2.5.3.1 | 🔒 | ADB reports as unauthorized |
| Crosscall Core-S4 | 2.5.3.2 | ✅ | No engmode-extension apps |
| Maxcom MK281 | 2.5.1.1 | ✅ |  |
| Jazz Digit 4G | 2.5.3.1 | ❓ |  |
| MTN Smart Feature Phone | 2.5.1.2 | ❓ |  |
| Multilaser/ObaPhone ZAPP | 2.5.1.1 | ✅ |  |
| Viettel V6504 | 2.5.3.2 | ⚠️ | Press and hold 2 on boot to enter KaiOS Recovery for injecting apps |