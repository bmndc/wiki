---
title: Change SMS and alarm tones
parent: Customization
layout: default
---
# Change SMS and alarm tones
{:.no_toc}

{:.is-info}
> This page is not complete.

1. Turn on debugging mode on your phone.

2. Enable temporary root access

3. Pull

```
adb pull /system/b2g/webapps/sms.gaiamobile.org
```

4. Extract
{:style="counter-reset:none"}

5. Replace
{:style="counter-reset:none"}

6. Push
{:style="counter-reset:none"}

```
adb push sms.gaiamobile.org /data/local/webapps
```

7. Pull
{:style="counter-reset:none"}

```
adb pull /data/local/webapps/webapps.json
```

8. Edit `basePath`
{:style="counter-reset:none"}

```diff
- "basePath": "/system/b2g/webapps"
+ "basePath": "/data/local/webapps"
```

9. Push
{:style="counter-reset:none"}

```
adb push webapps.json /data/local/webapps
```

10. Restart