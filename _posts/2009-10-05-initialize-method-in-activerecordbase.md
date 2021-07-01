---
layout: post
title: initialize method in ActiveRecord::Base
---

I spent quite a few hours trying to figure out why User.new (where user is a model) would not use the virtual attributes defined in the model class. Virtual attributes are the ones without a corresponding column in the table. Let me explain. I have a model called user which looks like this:

[gist id=201742]

Here, i\_am\_virtual is the virtual attribute. Let us say I have a form where I accept values for all the attribtues of the User model and that includes the virtual attribute (i\_am\_virtual) as well. Now, I was under the impression that when I do something like:

[gist id=201744]

it will automatically call the i\_am\_virtual= method so when I go looking for that value I can easily get it using:

[gist id=201745]

But unfortunately it does not seem to do it. I thought it was quite strange and when you have a doubt always refer the documentation but this time I went straight into the code. Here's the code from ActiveRecord::Base's initialize method:

[gist id=201727]

and the comments itself answers my questions. Really, I feel like an idiot now having spent all that time trying to figure out what was wrong with my code. But in the end it was a good exercise TBH.