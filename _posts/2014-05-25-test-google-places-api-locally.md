---
layout: post
title: Test Google Places API locally
---


Yesterday I had a chance to try out Google Places API. Quite detailed as you’d expect from Google. But, before integrating it with the code you really want to try it out.

When I say try it out, I mean just ‘curl’ an end-point in the terminal and inspect the results. With Google API’s you can create a server key (an API key) and at the time of its creation you specify the IP address for the server where requests would be made from. In order to test it locally, just find out your IP address either using whatsmyipaddress service if you don’t have a static IP address and then just use that IP address as the server address.

Now, you can use any tool (or maybe just use a GET endpoint in your browser) to see the results.

Hope it helps.
