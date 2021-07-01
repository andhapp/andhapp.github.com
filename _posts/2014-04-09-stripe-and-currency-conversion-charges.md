---
layout: post
title: Stripe and Currency conversion charges
---

Stripe is pretty awesome.

The integration is simple. Documentation is ample.

It just works!

### But, do you know how Stripe works out currency conversion charges?

Being a SAAS company means anyone can pay for your service and although you don't really need to know how the charges work, but it'd be nice if you know how many customers you really need before you make any profit. For you to calculate that number, you need to know how much are you making from one customer every month.

Whilst thinking about it, I came up with a few scenarios. I also made an assumption that in order to attract more customers, you preferred to create your plans in USD:

1\. Your Stripe account is set up in GBP. User pays for a plan (in USD) with their local currency which is also USD. How many times does Stripe charge currency conversion fee? Once - to convert the USD's to GBP's for you to withdraw, right?

2\. Your Stripe account is set up in GBP. User pays for a plan (in USD) with their local currency which not USD (could be any currency). How many times does Stripe charge currency conversion fee now? Twice - to convert the non USD's to USD's and then those to GBP's for you to withdraw, right?

Confusing, isn't it?

Well, Stripe is very reasonable. It never does what they call a 'double dip' when it comes to currency conversion charges. It only charges you currency conversion once when it converts the USD's (which is what your plans are set up in) to GBP's (what's your account in set up as).

### How can you save some of money on currency conversion?

Well, if you know where bulk of your customer segment is (I know I said SAAS kind of means you are open for business with anyone in the world), but let's say for instance you did have that information you can always set up your plans in that currency. The saving won't be huge, but something is better than nothing, right?

Hope it helps.