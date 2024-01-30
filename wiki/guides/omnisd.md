---
title: OmniSD (deprecated)
parent: Sideloading and debugging
layout: default
nav_order: 4
---
# OmniSD (deprecated)
{:.no_toc}

{:.is-warning}
> Starting with KaiOS 2.5.2.2, as part of major security changes, the `navigator.mozApps.mgmt.import` Firefox OS API, on which OmniSD, Wallace Toolbox and other Gerda-related apps rely to install apps from outside sources, has been removed. **OmniSD now no longer works on those newer versions.** In other words, you cannot use OmniSD to install apps on latest KaiOS phones anymore.
> 
> As such, this and other related pages are no longer relevant and have now been put under archive for usage on older versions. For now, the only officially supporting methods to sideload third-party apps on [debug-enabled KaiOS phones]({% link devices.md %}) are [WebIDE]({% link development/webide.md %}) on KaiOS 2.5 and [appscmd](https://developer.kaiostech.com/docs/sfp-3.0/getting-started/env-setup/os-env-setup) on KaiOS 3.
>
> Luxferre, OmniSD's original developer, has been working on a second, improved version of OmniSD, but so far no progress has been announced.

OmniSD is an application installer which directly install compatible ZIP packages onto your KaiOS phone, without the need of computers. Developed by Luxferre and written in HTML, CSS and JavaScript, it leverages the `navigator.mozApps.mgmt.import` API found in Firefox OS to register your apps.

To install OmniSD, just sideload the app using WebIDE.