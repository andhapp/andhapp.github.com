---
layout: post
title: rspec stub V should_receive
---

I have been pondering over the difference between the two aforesaid methods in rspec but it did not become apparent to me at first. Yesterday, whilst reading the [RSpec Bible](<http://www.amazon.co.uk/RSpec-Book-Behaviour-Development-Cucumber/dp/1934356379>) it all became crystal clear. I know some people might say "Oh...come on this is so easy" but I like to work these things out for myself because it is better in the longer run. Well let us have a look at the example from the RSpec book. Imagine you have a MessagesController and below is tiny bit of code from its spec:

<pre>before do 
   Message.stub(:new).and_return(message)
end

it "saves the message" do 
  message.should_receive(:save) 
  post :create
end
</pre>

What is the intent of this method?<br>

 It is to test if the message is getting **saved** or not when a HTTP POST is performed.

Therefore, we concentrate on the "save" bit and any other calls which are part of that action(create in this example) and are required to achieve save, in this case, are just stubbed i.e. new. However, in the code snippet below we do not need to stub anything because we do not need to do call any methods prior to new:

<pre>it "creates a new message" do 
  Message.should_receive(:new).
  with("text" =&gt; "a quick brown fox").
  and_return(message)

  post :create, :message =&gt; { "text" =&gt; "a quick brown fox" }
end
</pre>

Therefore, the spec methods basically ensure that one is testing just what the intent of the test is. Well...I could be absolutely wrong about all this but it is makes a bit more sense to me now. I will get it in the end hopefully.

\* Please note that all the code sinppets are taken from Chapter 24, Rails Controller, [The RSpec Book](<http://www.amazon.co.uk/RSpec-Book-Behaviour-Development-Cucumber/dp/1934356379>).

\* Updated on 18.02.14 - Replaced broken gist links with code snippets.