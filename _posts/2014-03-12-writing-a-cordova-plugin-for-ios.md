---
layout: post
title: Writing a Cordova plugin for iOS
---

There are a tons of articles out there to help you in writing a plugin. [Cordova's documentation](<http://docs.phonegap.com/en/3.4.0/guide_hybrid_plugins_index.md.html#Plugin%20Development%20Guide>) is detailed and very helpful too, but it's easy for you to get buried under the documentation and go right past the nifty quirks of the framework. Here's my few tips which may come handy for you when writing a cordova plugin:

- If you know a little bit of Objective-C syntax, it will help. It depends upon the kind of plugin you writing. If your plugin is going to dip down in the native iOS world, then Objective-C knowledge is a must. However, I had to do a very trivial thing in the plugin, so I got by fine. 
- Read and learn from other cordova plugins. There are a ton of plugins and reading their code will definitely help you in creating a successful plugin yourself.
- Use Xcode to run your hybrid application. I can see people raising their eyebrows to that statement, but, the latest Xcode has command line tools and cordova leverages them heavily. That means, I could develop the application, run, test it in emulator without ever opening Xcode. But, with plugins, you want to run the application through Xcode to see errors on the native side. 
- Lastly, plugin.xml is the metadata file, similar to gemspec file in the Ruby world. plugin.xml allows one to write config that ends up getting used by Xcode, so make sure you have the correct interface name that you'd like to access from the javascript side. 

<!-- -->