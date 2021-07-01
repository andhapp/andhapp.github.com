---
layout: post
title: Extend Paperclip 2.3.1.1 to retrieve attachment's dimensions in Rails 2.3.8
---

In my [previous](<http://www.andhapp.com/blog/2010/07/07/paperclip-and-validate-the-attachment-dimension/>) post, I mentioned a way of validating the size of the attachment and I did **warn** readers that it is a monkey-patch and it needs serious refactoring.

Big refactoring is a result of several small ones and that's exactly what I have done here. I have extracted the code out and it looks much neater now. As a result, I have reduced my technical debt and in the process gained a better understanding of Paperclip.

**Objective:**<br>

 1\. Make code reusable, probably extract it out and then use Ruby's magic to add it straight to Paperclip. So, that next time I can just use it without doing all the extra work.<br>

 2\. Make the existing code neat.<br>

 3\. To retrieve the width and height of the attachment.

This is where we left the code last time:

<pre>class Dummy &lt; ActiveRecord::Base
   has_attached_file :photo
   def validate
     temp_file = photo.queued_for_write[:original] #get the file that is being uploaded
     dimensions = Paperclip::Geometry.from_file(temp_file)
     if (dimensions.width &gt; desired_width) || (dimensions.height &gt; desired_height)
        errors.add("photo_size", "must be image size #{desired_width}x#{desired_height}.")
     end
   end
   def desired_height
      # retrieve it from a different model
   end
   def desired_width
     # retrieve it from a different model
   end
</pre>

Above, I have used @queued\_for\_write to retrieve the attachment object but if this code changes in Paperclip and I am using it in, let us say 5 different places, I will have to fix it in all those places. I just don't want to come back and change the code every time Paperclip changes anything. Therefore, this is plain wrong. Similarly, if the Paperclip::Geometry's API changes, I will have to endure the same painful process yet again. Therefore, it becomes essential to extract this code out into its own module and then it's all in one place. Right, so I created a module, as below:

<pre>module Paperclip
  module Dimension
    
    # calculates width using processor
    def width_of name
      return 0 unless path(name)
      Geometry.from_file(path(name)).width.to_i
    end

    # calculates height using processor
    def height_of name
      return 0 unless path(name)
      Geometry.from_file(path(name)).height.to_i
    end
    
    #path to the attachment
    def path name
      attachment_for(name).queued_for_write[:original]
    end
    
  end
end
</pre>

I am instead using a method [attachment\_for](<http://github.com/thoughtbot/paperclip/blob/master/lib/paperclip.rb#L372>) within Paperclip. For example, if you have code like:

<pre>has_attached_file :photo
</pre>

then, you can do something like:

<pre>attachment_for :photo
</pre>

to get hold of the attachment object. But bear in mind, has\_attached\_file is a class method where as attachment\_for is an instance method (I can't really explain the difference here but the fact is they can't be used in a similar way). This allows me to change the code in my model to something like this:

<pre>class Dummy &lt; ActiveRecord::Base
   has_attached_file :photo
   def validate
     if width_of(:photo) &gt; desired_width || height_of(:photo) &gt; desired_height
        errors.add("photo_size", "must be image size #{desired_width}x#{desired_height}.")
     end
   end
   def desired_height
      # retrieve it from a different model
   end
   def desired_width
     # retrieve it from a different model
   end
</pre>

Wow! That is clean and has the same syntax as has\_attached\_file. I don't need to indulge in Paperclip's nitty gritty. It's in a different module. But you can't run this code just yet. Because, it's not hooked into my application yet. If you do run it, you should see NoMethodError on width\_of. In order to hook this code up into our application, add the module to a file, let us name it, paperclip.rb and put it inside app\_root/config/initializers/.

So, when the app starts up it will load this file but this module is nothing without the support of actual Paperclip. Therefore, to hook it into Paperclip, we will add the following line at the bottom and the module in it's final state would look something like this:

<pre>module Paperclip
  module Dimension
    
    # calculates width using processor
    def width_of name
      return 0 unless path(name)
      Geometry.from_file(path(name)).width.to_i
    end

    # calculates height using processor
    def height_of name
      return 0 unless path(name)
      Geometry.from_file(path(name)).height.to_i
    end
    
    #path to the attachment
    def path name
      attachment_for(name).queued_for_write[:original]
    end
    
  end
end

Paperclip::InstanceMethods.send(:include, Paperclip::Dimension)
</pre>

I am including our custom module inside Paperclip::InstanceMethods, which gets called when has\_attached\_file is [invoked](<http://github.com/thoughtbot/paperclip/blob/master/lib/paperclip.rb#L259>) from within the model class and ensures all the instance methods are available to our model class.

Now, if you run it. It will work like a charm. By just adding this code to your initializers you can simply retrieve the width and height of the attachment. Here's the [gist](<http://gist.github.com/466691>) of the file, if you need it.

I hope it helps and for anyone interested, please go ahead and create a validator for dimensions just like we have one for size.