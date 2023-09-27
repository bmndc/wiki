---
title: W2D KaiOS Jailbreak
layout: minimal
nav_order: 7
---
# W2D KaiOS Jailbreak

Web To Development script that invokes the developer menu hidden from the Settings app.

Just click the button below from the browser of your KaiOS device.

*Credits to Luxferre, tbrrss and Cyan.*

<button class="btn js-launch-dev-menu">Launch Developer menu</button>

<script>
const launchDevmenu = document.querySelector('.js-launch-dev-menu');

jtd.addEvent(launchDevmenu, 'click', function(){
  if(window.MozActivity) {
    var act = new MozActivity({
      name: "configure",
      data: {
        target: "device",
        section: "developer",
      },
    });
    act.onerror = function (e) {
      console.error(act, e);
      window.alert("Error:", JSON.stringify(act), e);
    };
  } else if (window.WebActivity) {
    var act = new WebActivity("configure", {
      target: "device",
      section: "developer",
    });
    act.start().catch(function (e) {
      console.error(e, act);
      window.alert("Error: " + e);
    });
  } else {
    window.alert('Please open the page from the device itself!')
  }
});
</script>