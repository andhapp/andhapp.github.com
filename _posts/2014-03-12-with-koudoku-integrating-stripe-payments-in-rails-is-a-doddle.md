---
layout: post
title: With koudoku, integrating Stripe payments in Rails is a doddle
---

Most, if not all, SASS applications need some sort of payment integration to charge customers for subscriptions and repeatedly do it every month (or year or any time interval). if you are looking for one such payment-subscription solution, then Stripe is what you need. Stripe has awesome documentation, amazing dashboard, and the ability to test everything out is icing on the cake. I've not had the chance to try any other Stripe like payment integration services and I'm sure they provide similar features. Anyways, today it's about Stripe, and a lovely little gem called [koudoku](<https://github.com/andrewculver/koudoku>).

Koudoku is a Rails engine, and gives you all the subscription related stuff that you may ever need. For example: Signing-up with a particular plan, upgrading a plan for a user. It creates customers, charges cards, and updates subscriptions through Stripe's APIs. You never have to worry about all that. The gem does all that for you. It has customisable views, just like devise, which you can style the way you like. Only one drawback is the support for webhooks is a bit sparse. Only supports three events right now, but the documentation does make that fact very clear.

However, there are a few gotchas:

1\. In order to create some testing users, with subscriptions, you need to make sure they are linked to actual customers on the Stripe side, otherwise you will see the following error:

<pre>Stripe::InvalidRequestError: No such customer
</pre>

The best thing to do is create some customers on Stripe in test-mode, and use their id's when create users with subscriptions.

2\. To get the webhooks working, I had to subclass the koudoku webhooks controller, and add the following line of code:

<pre>skip_before_filter :verify_authenticity_token
</pre>

3\. Stripe will call your webhooks end-point to notify of the various events on a customer, for example, payment succeeded, charge failed and so on. You can take the appropriate action, for example, to send invoice, or email admin in response to it. I found two very nice resources to test your localhost webhook with Stripe. I presume both use reverse ssh-tunnelling, but they work out of the box, and one is even a rubygem. I used [ultrahook](<http://www.ultrahook.com/>), but also found [ngrok](<https://ngrok.com/usage>) a little later.

In all, it took me one evening to set-up and test the whole thing end-to-end. It's so easy that it should be called Stripe-asy!

Hope it helps.