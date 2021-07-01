---
layout: post
title: IE11's javascript engine doesn't work correctly with promises
---

Yes, you read it right!

It doesn't work correctly. Specifically, if you had an array of promises, then in IE 11 (and any other version), the promises are processed synchronously, and it will go through them one by one. In Firefox and Chrome, it works as expected. The promises are resolved as and when they have finished processing and run independently of each other. Synchronous processing makes IE's performance worst of all. In some cases, it just errors out. We spent quite a while on this issue and had to resort to using callbacks, in the end, to get it working in IE.

My suggestion for anyone working with the latest HTML5 API's would be to start developing on IE. Browsers like Chrome have spoilt us developers, which makes it harder and at times, frustrating to put in workarounds for IE.
