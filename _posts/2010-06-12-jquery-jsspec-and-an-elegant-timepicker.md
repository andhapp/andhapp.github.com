---
layout: post
title: Jquery, JSSpec and an elegant timepicker
---

Time selection via web has always been those grey areas where one does not really find good solutions. With the advent of [Jquery](<http://www.jquery.com>), there are plethora of date selection javascripts out there. However, time selection has not received similar treatment. After much searching I found two solutions. The first one was very fancy but depended heavily on the Jquery Widget and with custom ui stuff rewritten in recent versions, it simply did not work with newest custom-ui scripts.

The second solution was simple and straight-forward but laden with bugs. However, a bit of hacking yielded a good working solution but it was still lacking something important and essential i.e. Tests. After a bit of googling, I zeroed on [JSSpec](<http://code.google.com/p/jsspec/>) as the testing framework. [QUnit](<http://docs.jquery.com/QUnit>) is at par with JSSpec but I quite like the RSpec way of testing and JSSpec emulates that for javascript.

Testing is hard. No doubts about it. But testing javascript is a completely different ball game. It is easy and quite fun, once you get the hang of it but initially it is just confusing. I had problems in setting up the test cases, ensuring the requisites are there. For example: if we are testing weather an input box slides out on a link click then we need to make sure that an input box is there. I know it sounds easy but when it comes down to writing specs, mind goes completely blank. Anyways, here's the link to [jquery-timepicker](<http://github.com/andhapp/jquery-timepicker>). Go and check it out.