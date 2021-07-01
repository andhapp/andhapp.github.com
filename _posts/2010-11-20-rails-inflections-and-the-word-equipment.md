---
layout: post
title: Rails inflections and the word 'Equipment'
---

I was in two minds about this post's title. On one hand, I think this should be called "Why googling is not the answer to every question?" and on the other hand the current title will probably interest more people. Rails inflections is not the main focus of this post. This post is a consequence of Rails inflections and attempts to highlight some of the things that are wrong with the way developers work now a days.

Last week, I had to create a model called 'Equipment'. I know now that 'Equipment' is uncountable therefore when it comes to creating a table rails will not tabelize resulting in a table with name "equipment". But few days ago, I was surprised and straight-away [googled](<http://www.google.co.uk/search?q=equipments&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a>) the word 'equipments' and results confirmed my doubts that this is a bug in Rails. Silly me.

I went through the code and found it in the [inflections](<https://github.com/rails/rails/blob/master/activesupport/lib/active_support/inflections.rb#L54>) file and found that the 'equipment' word defined as uncountable. Now, I was even more surprised. If the word "equipments" exist (as confirmed by Google) then why on earth will Rails do otherwise. There is only one place that could resolve my dilemma, yes you got it right, Oxford dictionary. I looked it up and "Equipment" is an uncountable noun just like "information".

Now, this little research basically highlights two things:

1\. Google is just a search engine. Think about what you are doing and then take an intelligent decision.<br>

 2\. Don't assume that Rails is behaving incorrectly and leave it at that. Investigate and read the code. That will improve your understanding. I have seen several code bases where developers have actually just assumed what they are told and carried on.

Few weeks ago, John Nunemaker spoke about '[Stop Googling](<http://railstips.org/blog/archives/2010/10/14/stop-googling/>)'. If I have a bug, I will clone the code and start looking into it. In last few weeks, I have read the code bases from [rspec and cucumber](<http://www.andhapp.com/blog/2010/10/10/using-cucumber-092-and-cucumber-rails-032-with-i18n/>), [clearance](<https://github.com/thoughtbot/clearance>), [rails](<https://github.com/rails/rails>), [rvm](<https://github.com/wayneeseguin/rvm>) and [spree](<https://github.com/railsdog/spree>) and found various good and bad things in them. This also takes me one step closer to [giving something back to the open source community](<http://railscasts.com/give_back>). But will talk about it more in my next post.