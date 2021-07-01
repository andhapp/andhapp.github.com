---
layout: post
title: cucumber-js, appium, WebDriverJs and Javascript Promises
---

I have mixed feelings for Appium. At times, it works beautifully, and then suddenly falls flat on it's face, leaving you frustrated. Nevertheless, once you know how it's wired up with other related tech, you feel comfortable and willing to debug the issues it throws at you. Before you ask, I had to write features to test a hybrid mobile application, currently just targeting iOS. This post just describes my experience and some gotchas. It doesn't go into details on how to set up appium with cucumber-js, because there are plenty of other blog posts on that subject.

### [cucumberjs](<https://github.com/cucumber/cucumber-js>)

Cucumber is a defacto for writing features and the good news is that's what I used. It's no different in terms of syntax to it's ruby counterpart. You need to set-it up with Appium, and WebDriverJs, but there are plenty of articles on the subject.

### [appium](<https://github.com/appium/appium/>)

Appium is a test automation framework that implements Selemium WebDriver interface using instruments for iOS, and Android. It implements the [Selenium WebDriver spec](<https://code.google.com/p/selenium/wiki/JsonWireProtocol>), so any selenium compatible client web drivers work fine with it. Appium exposes selenium-compatible API over HTTP, and selenium-webdriver communicates over the exposed end-points. Now, Appium not just implements WebDriver spec, it [also augments it in interesting ways](<https://github.com/appium/appium/blob/master/docs/gestures.md>). Appium uses [instruments](<https://developer.apple.com/library/mac/documentation/developertools/conceptual/instrumentsuserguide/Introduction/Introduction.html>) to inspect iOS code.

### [WebDriverJs](<https://code.google.com/p/selenium/wiki/WebDriverJs>)

WebDriverJs is the final piece of this puzzle. It's not much different from any other web driver. However, it does have a couple of interesting things. First, it implements a promise manager in the background which ensures that you write async code in a sync manner. For example, with promises you will write code like this:

<pre>   driver.loadWebApp().
    then(login).
    then(openUserPreferences);
</pre>

but, with WebDriverJs the promise manager, you don't have to worry about the verbosity, you can simply do:

<pre>    driver.loadWebApp();
    driver.login();
    driver.openUserPreferences();
</pre>

The promise manager ensures the order is maintained giving you the same behaviour as callbacks. Now, you would like to use the same promise manager with your own code, but the promise manager is not really exposed publicly. Well, it's exposed but I couldn't really find a way to use it with the way we have wired it up in our project. However, if you'd like to take use of it then you can do something like this:

<pre>driver.call(myFunc);
</pre>

The **call** method delegates calls to the promise manager.

### Feature testing gotchas

1\. You will see the following error intermittently, and this just means restart appium:

<pre>SessionNotCreatedError: A new session could not be created 
error: Failed to start an Appium session, err was: Error: Requested a new session but one was in progress
</pre>

2\. If you cancel running your features in the middle, and then try again, they won't run. You will have to restart appium.

3\. Finally, running features are very time-consuming, since appium fires up the emulator and evaluates the features against it.