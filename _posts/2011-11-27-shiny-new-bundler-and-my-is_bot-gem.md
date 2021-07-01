---
layout: post
title: Shiny new bundler and my is_bot gem
---

If you haven't already installed the release candidate of superfast bundler, then I feel sorry for you. It's hard to put your faith in me but here's an [article](<http://patshaughnessy.net/2011/10/14/why-bundler-1-1-will-be-much-faster>) that might change your heart. It's super simple, just do:

 ```
 gem install bundler --pre
 ```

 Last year, I released a gem called is_bot (which is just a trivial way to fool the spammers). I have been using it in several projects and keep updating it with new releases of the Rails. Few months back when [rubygems](<http://blog.rubygems.org/2011/08/31/shaving-the-yaml-yak.html>) was having trouble with Syck yaml parser, I released a version - `0.3.3` - of my is_bot gem. As a result, this version of is_bot suffered from the same issue and it gave me error messages on subsequent installs. Since then, I have released three more versions of the gem and the current version stands at `0.3.6`.

Now, the earlier version of bundler was quite forgiving and I could hack the cached gemspec file to install it. But the new version of bundler, simply rejects it. I was quite surprised to see the error message I get from bundler when I tried installing the current version - `0.3.6`. Because, it doesn't say anything about the `0.3.6` version but complains about `0.3.3` version. I thought I was going crazy. I even specified the version of the gem to `0.3.6` in my Gemfile but still it complained about `0.3.3` version. I know, I know that bundler needs to download the `Big Index` for dependency resolution but I never had this problem with the earlier versions of bundler, then why now.

Why my gem?

So, I did more investigation and ran the following command to see what exactly does bundler get back when it hits the [rubygems's endpoint](<http://guides.rubygems.org/rubygems-org-api/#misc>):

```
ruby -ropen-uri -rpp -e 'pp Marshal.load(open("https://rubygems.org/api/v1/dependencies?gems=is\_bot"))'
```

 and this returns something like this:

 ```
 [{:platform=>"ruby", :name=>"is\_bot", :dependencies=>[["rspec", ">= 0"], ["rails", "= 3.1.1"]], :number=>"0.3.6"}, {:platform=>"ruby", :name=>"is\_bot", :dependencies=>[["rspec", ">= 0"], ["rails", "= 3.1.1"]], :number=>"0.3.5"}, {:platform=>"ruby", :name=>"is\_bot", :dependencies=> [["rspec", ">= 0"], ["rails", "#<yaml::syck::defaultkey:0xbd36f20> 3.1.0.rc6"]], :number=&gt;"0.3.3"}, {:platform=&gt;"ruby", :name=&gt;"is_bot", :dependencies=&gt;[["rspec", "= 2.6.0"], ["rails", "= 3.1.0.rc5"]], :number=&gt;"0.3.2"}, {:platform=&gt;"ruby", :name=&gt;"is_bot", :dependencies=&gt;[["rspec", "= 2.6.0"], ["rails", "= 3.1.0.rc4"]], :number=&gt;"0.3.1"}, {:platform=&gt;"ruby", :name=&gt;"is_bot", :dependencies=&gt; [["sqlite3", "= 1.3.3"], ["rspec", "= 2.6.0"], ["rails", "= 3.1.0.rc4"]], :number=&gt;"0.3.0"}, {:platform=&gt;"ruby", :name=&gt;"is_bot", :dependencies=&gt; [["sqlite3", "= 1.3.3"], ["rspec", "= 2.4.0"], ["rails", "= 3.0.3"]], :number=&gt;"0.2.0"}, {:platform=&gt;"ruby", :name=&gt;"is_bot", :dependencies=&gt;[], :number=&gt;"0.1.0"}]
 ```

 And you can see `YAML::Syck::DefaultKey:0xbd36f20` bit that results in illformed gemspec error. I guess the earlier versions of Bundler had a fix for this issue, but the latest rc version loads up this information and straight-away complains about the illformed gemspec. That's all good but what's the solution for this issue.

 Simple!

 Yank the `0.3.3` version of the gem and you are good to go. Another solution would be to regenerate the gemspec for `0.3.3` again, which I hope rubygems stores uncorrupted. Phew.

