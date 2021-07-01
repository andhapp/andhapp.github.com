---
layout: post
title: Python2 not found error on installing emscripten on Mac OS X (Yosemite)
---

On the weekend, I needed to use a `C library` and decided to give `node.js` a try as I have been spending more time in the JavaScript ecosystem. Google revealed few ways to connect to a C library from node, namely, [node-ffi](<https://github.com/node-ffi/node-ffi>), [emscripten](<http://kripken.github.io/emscripten-site/docs/getting_started/downloads.html>) and so on. `Node-ffi` is similar to `ruby-ffi` and is a wrapper around `libffi`.

Given that I have used `ruby-ffi` in the past, I decided to give emscripten a try this time around. The installation guides are spot on and work like a charm except for one minor thing. For some reason, on running the `emscripten` (using `./emcc` command) it complained about not finding `python2`. Not sure why it's looking for `python2` in the `PATH`, but I created a symlink to the installation of python in `/usr/bin` and called it `python2` instead.

Hope this simple fix doesn't cause any more issues later on.
