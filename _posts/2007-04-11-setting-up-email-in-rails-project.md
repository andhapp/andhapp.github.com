---
layout: post
title: Setting up email in Rails project
---

I spent last whole week trying to figure out what was wrong with the e-mail code I wrote in Ruby on Rails because I followed he book closely and was expecting to run it without any issues...but anyways... here are few things you must know before you embark on this task:

1\. Ask your host how the server has been configured...after several days and exchange of several emails I discovered that [mine](<http://www.gazzin.com/>) has been set up as **"POP before SMTP"** due to which I was getting a bizarre error.<br>

 2\. If it is SMTP then I guess it is straight forward (as in the book or tutorials on the web or whatever reference you are following) but if it is **"POP before SMTP"** then go [here](<http://wiki.rubyonrails.org/rails/pages/PopBeforeSMTPForActionMailer>). As you will see the link will take you to another page which has two separate code snippets ...the first one need to go in the environment.rb and the second one need to go in the ActionMailer's base.rb class.

Since you will be amending the rails code base I will suggest to perform a [freeze](<http://www.andhapp.com/blog/post/Rails-Input-output-error-on-linux-/35>) and then do it on the rails code local to the project. You can find the base.rb class at the following location:

**rails\_project\_directory/vendor/rails/actionmailer/lib/action\_mailer/base.rb **

I hope it will resolve the issues for you.