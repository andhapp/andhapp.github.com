---
layout: post
title: Using factory_girl with cucumber
---

I have moved away from fixtures and there is only one reason for it. factory\_girl is an awesome piece of functionality the gives one the flexibility to easily define the data to use in tests and for populating the database with dummy data. However, I must add that I am also using [Populator](<http://github.com/ryanb/populator/>) and [Faker](<http://github.com/yyyc514/faker/>) gems along with [factory\_girl](<http://github.com/thoughtbot/factory_girl>) to populate the database with dummy data but I will discuss it some other day.

Now, [cucumber](<http://github.com/aslakhellesoy/cucumber/>) is the [BDD](<http://en.wikipedia.org/wiki/Behavior_Driven_Development>) library that allows one to write the features first. The features are in plain English and any client-manager can understand them. However, there was quite a [debate](<http://www.rubyinside.com/coulda-a-cucumber-like-dsl-for-bdd-2461.html>) few weeks ago over this whole issue of - "Who lets their client managers write stories?". Follow the [link](<http://www.rubyinside.com/coulda-a-cucumber-like-dsl-for-bdd-2461.html>) if you are interested and read the comments. Anyways, I have been trying this out recently and I must say after an initial steep learning curve I can see the benefits. You just define the functionality from a user's perspective and it makes the development a tad longer yet easier.

Now, using factory\_girl from within rspec is easy but how can I make sure that the data is there before I run my cucumber features. Because in order to test a feature like a "admin should be able to delete a user" there must be a user in the system otherwise how could it be tested? Well, here's the solution to it.

Problem: Create test data before the cucumber features.

In order to create an instance of a model object we can use one of the following depending on the situation:

<pre>Factory(:model_factory)
Factory.build(:model_factory)
</pre>

Now, to make sure we create all the factories that we have defined already we need to get a list of all the defined factories somehow. And we need this list before we run the cucumber features. So, we simply add the following code to env.rb (cucumber's config file) and voila!

<pre>Before do
  require 'factory_girl'
  Dir.glob(File.join(File.dirname(__FILE__), '../../spec/factories/*.rb')).each {|f| require f }  
  Factory.factories.keys.each {|factory| Factory(factory) }
end
</pre>

You would ask why does this work? Well, let us see what does the define method do. The same method that we use to define a factory. Here's the code inside the define method\*:

<pre># File 'lib/factory_girl/factory.rb', line 48

def self.define (name, options = {})
  instance = Factory.new(name, options)
  yield(instance)
  if parent = options.delete(:parent)
    instance.inherit_from(Factory.factory_by_name(parent))
  end    
  self.factories[instance.factory_name] = instance
end
</pre>

The last line in the method is basically adding the name of the created factory to the factories class variable and that's the variable I use to get hold of these defined factories.

\* - Code taken directly from the latest [rdocs](<http://rdoc.info/projects/thoughtbot/factory_girl>)

**Update(10 October, 2010):**<br>

 I think factory\_girl has since changed its internal code. I am assuming it has since I tried using this code with Rails3 and cucumber-0.9.2 and cucumber-rails-0.3.2, but the features did not run at all. So, now if you wish to use factory\_girl with cucumber add this in env.rb file instead:

<pre>Before do
  require 'factory_girl'
  Dir.glob(File.join(File.dirname(__FILE__), '../../spec/factories/*.rb')).each {|f| require f }  
end
</pre>

So, what I am simply doing now is building the factories but not actually creating them and now you can create all your factories in the step\_definition files. I think this is a better way of using factory\_girl with cucumber.