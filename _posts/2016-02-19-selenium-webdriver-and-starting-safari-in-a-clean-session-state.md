---
layout: post
title: Selenium WebDriver and starting Safari in a clean session state
---

I first used selenium on a java project a while back. Since then selenium has grown by leaps and bounds. With continued support and a myriad of bindings, it's a tool to go to for automated testing. However, it does sometimes stumps you with nuances you've not seen in the past. One such quirk I came across this week was starting safari in a clean session state. Unlike Chrome and Firefox, it's impossible to start safari in a clean session state. A clean session state means devoid of any hangovers, cookies, for instance is a good example.

The project I was working on was set up with cucumber features using capybara that in turn uses selenium webdriver's ruby bindings for communicating with the browser. Like any astute developer, I googled for solutions.

Beware! Google search for 'safari in clean session state' may throw you off into a completely different direction. Here are some of those solutions that won't work.

1. Pass `clean_session` state as `true` as an additional option when a new capybara driver is registered for Safari. However, this will not work. Because, there's a comment in [selenium webdriver's code pointing](<https://github.com/SeleniumHQ/selenium/blob/master/rb/lib/selenium/webdriver/safari/bridge.rb#L34>) out the fact that it's still outstanding.

2. Open Safari with different flags like `-n -b -F`. This doesn't work either. Even if it did, you will have to delve deep in selenium webdriver land to pass that option in and monkey patch a solution for this. Thankfully, it doesn't work because monkey-patching is never a reliable way to fix bugs.

So, what's the solution?

Well, the only way to fix it is by deleting the cookies before a feature run. Typically, add some code to delete cookies in a before hook for capybara to run before each feature.

It took a lot of trying, experimentation and patience to find this solution and sincerely hope it helps someone.
