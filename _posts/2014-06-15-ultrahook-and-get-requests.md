---
layout: post
title: Ultrahook and GET requests
---

A couple of months ago, I wrote about [testing Stripe's webhooks with Ultrahook](<http://www.andhapp.com/blog/2014/03/12/with-koudoku-integrating-stripe-payments-in-rails-is-a-doddle/>).

Just this week, I found out while trying to run a GET request against Ultrahook, that it doesn't allow GET requests for security reasons. Maybe give ngrok a try for testing GET requests to your localhost. Webhook calls are POST requests and Ultrahook is as good as gold for that use-case.
