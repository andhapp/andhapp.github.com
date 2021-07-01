---
layout: post
title: Bundler and Rails 2.3.8
---

Life as a "Rails Developer" is a pretty smooth sailing and [Bundler](<http://github.com/carlhuda/bundler>) just makes it ever better. Rails 2.3.8 is the newest version from the Rails team. Don't get me wrong, I love to hack my way through Rails3 but time is a big constraint for the project I am working on at the moment. With Rails3, I am bound to hit some road blocks but this is just a quick project I would like to get done and over with.

I am not going to talk about how to initialise bunder and create a Gemfile. You can follow that easily from the [github](<http://github.com/carlhuda/bundler>) page. So, for the sake of this post let us assume that this is what your Gemfile looks like:

<pre>source :gemcutter

gem "rails",          "2.3.8"
gem "i18n"
gem "formtastic",     "0.9.1"

group :test do
  gem "rspec",        "1.3.0"
  gem "rspec-rails",  "1.3.2"
end

</pre>

Now, when you run the following command:

<pre>bundler install vendor
</pre>

you will get an error related to **ruby\_version\_check.rb** not found or something similar complaining about the absence of ruby\_version\_check ruby script. To fix it, just create a file named ruby\_version\_check.rb in your project's lib folder and copy the contents of this [gist](<http://gist.github.com/423851>) in it. I copied this file from the Rails master branch and changed the **min\_release** variable to 1.8.6 since 1.8.7 gave me some nasty segmentation errors on my mac. But if you have 1.8.7 installed and working correctly, change the min\_release back to 1.8.7.

Next, step is to add the following code to your environment.rb file:

<pre>require "bundler"
Bundler.setup
</pre>

and you should be good to go.

However, there are two things that I have not yet figured out a solution to:

1. Using Rails engines like [clearance](<http://github.com/thoughtbot/clearance>) since the generators have been completely revamped in Rails3 and might need a through investigation. So, for now I have added it in the old way using config.gem syntax in the environment.rb file.
2. I got some strange error on time zone which went away by commenting out config.time\_zone = 'UTC' line of code. This still needs investigation.

<!-- -->

I hope this helps anyone trying to get their head around using Bundler with Rails 2.3.8. This set up might work with pervious versions and if you will try it out for yourself.

**Update**: Just tried using rspec\_controller generator and it can't be invoked as well. So, using Bundler does not hook up the generators. Although. I would think that should not be the case since Bundler adds all the required libs to the $LOAD\_PATH so that they are found when Rails goes looking for them. Needs more investigation.