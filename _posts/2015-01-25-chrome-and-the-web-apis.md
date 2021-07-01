---
layout: post
title: Chrome and the Web APIs
---

Browser is becoming better by the day and Chrome is at the forefront of this movement. There are a plethora of interesting [Web APIs](https://developer.mozilla.org/en-US/docs/Web/API) that will redefine the browser in the near future. It won't be far wrong if we extended the Javascript prophecy to the browsers - 'anything that can be done in a browser will be done in the browser in the future', and it's true to a large extent even now, i.e., [Chromebook](https://www.google.co.uk/chrome/devices/).

I recently came across Bluetooth API that landed in Chrome canary recently. It doesn't do much right now, but, it's a start. To see it in action:

1. I enabled the *Enable experimental web platform features* in `chrome://flags` for my local Chrome canary installation<br>

2. Restarted the browser<br>

3. Connected the phone to the mac via bluetooth<br>

4. Opened Chrome developer tools and ran the following command:

```
navigator.bluetooth.requestDevice().then(
  function(d) {
   console.log('Found a device', d); 
  },
  function(e) {
  console.log('Exception', e); 
  }
);
```

It returned straight-away with the following output:

```
Found a device BluetoothDevice {instanceId: "E0:CB:EE:84:F7:C2"}
```

`requestDevice()` returns a promise and you can attach the appropriate `resolve` and `reject` callbacks with it.

**That's well and good, but what can I really do with this?**

Just off the top of my head:

- take a phone call on your computer
- transfer data
- transfer audio
- ...and lots more, in the future

