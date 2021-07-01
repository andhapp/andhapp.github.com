---
layout: post
title: Rails3 and rspec-rails-2.0.0.beta20 and cucumber-rails-0.3.2
---

Last week, I started a Rails3 project and considering I am sucker for TDD. I added the current stable versions of rspec-rails and cucumber-rails to the Gemfile. Now, this is a simple project (and honestly speaking I could have just used Sinatra) for the same, but I wanted to get a Rails3 app up and running.

When I say simple, I mean no "ActiveRecord". Some might say I am better off using Sinatra with so little codebase to load but like I said it was just to get some hands on experience with Rails3. Developers mostly use rspec-rails and cucumber-rails with activerecord and since I wasn't going to use activerecord, I hit a few road blocks.

**Rspec-rails**<br>

 First, let's have a look at changes one needs to do use rspec-rails with activerecord. I am assuming that you have installed rspec in your rails app using the new rails3 generators and you have a spec\_helper.rb in your spec folder. Just comment out the following lines to make it work with activerecord:

<pre>  config.fixture_path = "#{::Rails.root}/spec/fixtures"
  config.use_transactional_fixtures = true
</pre>

spec\_helper.rb file does have directions to remove these files in the absence of activerecord.

**Cucumber-rails**<br>

 Similarly, cucumber-rails actually relies on the fact that activerecord is always used. When you run **rake:cucumber**, you will probably see the following errors:

<pre>** Invoke cucumber:all (first_time)
** Invoke cucumber:ok (first_time)
rake aborted!
Don't know how to build task 'db:test:prepare'
</pre>

Reason, because cucumber depends upon the db:test:prepare task to run. But in the absence of activerecord this causes issues since there is no db. I added a patch for the same which checks for the presence of database.yml and takes action accordingly. Here's the lighthouse [ticket](<https://rspec.lighthouseapp.com/projects/16211-cucumber/tickets/656-error-on-running-rake-cucumber-in-rails3-app-without-activerecord-dependency>) and [patch](<http://s3.amazonaws.com/activereload-lighthouse/assets/19755635e6c54f8ebe0124170007ce20e8b184c8/patch_to_fix_template_in_absence_of_activerecord.diff?AWSAccessKeyId=1AJ9W2TX1B2Z7C2KYB82&Expires=1284207850&Signature=E0kjgnJaJvTIiYG%2FE8YoX4UaDHc%3D>). You can monkey patch it in your app by modifying the rake task in lib/tasks/cucumber.rake.

In the end it was a good experience and taught me a bit more about cucumber and rspec.