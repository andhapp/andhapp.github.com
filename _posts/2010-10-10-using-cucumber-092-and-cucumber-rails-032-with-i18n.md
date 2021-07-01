---
layout: post
title: Using cucumber-0.9.2 and cucumber-rails-0.3.2 with I18n
---

I have previously, [blogged](<http://www.andhapp.com/blog/2009/11/07/using-factory_girl-with-cucumber/>) about using factory\_girl with clearance and this post (quite similar to that one) describes the need to use messages (notice, success or failure) in your locale file with cucumber and how to go about using them. Needless to say, this pertains only to the Rails crowd but I guess anyone can set-up their gems or ruby aps to extract similar behaviour. I have been using cucumber with Rails3 and been [blogging](<http://www.andhapp.com/blog/2010/09/11/rails3-and-rspec-rails-200beta20-and-cucumber-rails-032/>) about my experiences for last couple of weeks.

Imagine, you are writing a feature and you would like to test that the correct flash message gets displayed when something goes wrong or as a notification to the user. In order to make sure, I use the same message across the board I would like to add them to my locale file and read it from there. Instead of having to copy paste them since with cucumber outward-in TDD approach one writes the feature then jumps into write controller and model specs to make the feature pass. Now, in order to achieve that all you gotta do is load the i18n library when the cucumber features are run. So, just add the following to env.rb:

<pre>require "i18n"
</pre>

But, I can't use the following snippet in my scenarios. How will I use it with cucumber?

<pre>I18n.translate :invalid, :scope =&gt; [:login, :errors, :messages]
</pre>

Simple, just use it in your step definitions. Instead of the following scenario:

<pre>Scenario: Logging in
  Given I am on sign in page
  When I press "Log in"
  Then I should see error messages
</pre>

use this scenario:

<pre>Scenario: Logging in
  Given I am on sign in page
  When I press "Log in"
  Then I should see error messages
</pre>

In your step definitions, add a new step for "I should see login failure messages" like this:

<pre>Then /^I should see login failure messages$/ do
   Then %{I should see "#{I18n.translate :invalid, :scope =&gt; [:login, :errors, :messages]}"}
end
</pre>

And that's it. It does sound like a lot of work but it took me under 15 minutes to get it working.