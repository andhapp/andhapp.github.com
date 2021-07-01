---
layout: post
title: Getting Clearance test suite to green
---

The title could be slightly misleading but I am not talking about installing clearance in your Rails application. This post is just a small note to myself since I had considerable difficulties in getting the clearance gem's test suite working in my local environment. It's a very trivial detail that I missed or rather overlooked whilst trying to get them working. For readers who don't know, [Clearance](<https://github.com/thoughtbot/clearance/>) is a Rails authentication engine and is developed by ThoughtBot and let me tell you that they love Cucumber. For testing the engine, Clearance uses [Aruba](<https://github.com/aslakhellesoy/aruba>), i.e. CLI steps for Cucumber.

The background story is that I have been quite interested in Clearance for quite a while now and am quite active in the ML and do chime in with my opinions and I just updated my local fork after a while and ran the specs and features. My preferred approach when bug fixing or adding any features or just code browsing any library is to install the dependencies in the vendor directory via bundler. I could use rvm gemsets and install the dependencies there but I usually don't go for that approach.

So, I did exactly the same for clearance and installed the dependencies to vendor directory and ran the specs and features. Specs ran without any issues but with features I got a weird **"bundler can't be found"** error. I was stumbled because I do have bundler installed on my machine. Anyways, after hours of debugging I figured the root of the cause. Below is the cucumber feature that does the background work in testing the engine(\*taken from [Clearance repository](<https://github.com/thoughtbot/clearance/blob/master/features/integration.feature>)):

<pre>When I successfully run "rails new testapp"
    And I cd to "testapp"
    And I remove the file "public/index.html"
    And I remove the file "app/views/layouts/application.html.erb"
    And I configure ActionMailer to use "localhost" as a host
    And I configure a root route
    And I add the "cucumber-rails" gem
    And I add the "capybara" gem
    And I add the "rspec-rails" gem
    And I add the "factory_girl_rails" gem
    And I add the "dynamic_form" gem
    And I add the "database_cleaner" gem
    And I add the "clearance" gem from this project
    And I add the "diesel" gem
    And I run "bundle install --local"
    And I successfully run "rails generate cucumber:install"
    And I disable Capybara Javascript emulation
    And I successfully run "rails generate clearance:features"
</pre>

and you can see it creates a new rails app and installs the dependencies as part of the feature.

To run the test suite I used the following command:

<pre>bundle exec rake cucumber
</pre>

because I installed all my dependencies in vendor and for them to be in the LOAD\_PATH ran rake scoped via bundler. Now, when it came to running the CLI steps it complained about bundler's absence because it was not installed to vendor as it was not in the Gemfile.

I did not use:

<pre>rake cucumber
</pre>

because then bundler path would not kick in and the features would fail straight-away. So, how can we get this to work. Simple. Just create a new gemset for all the clearance development dependencies and get bundler to install it to the gemset as opposed to vendor and then run the features using:

<pre>rake cucumber
</pre>

And they will be green. Phew. It took me a while to figure this out but I am so relieved I did.