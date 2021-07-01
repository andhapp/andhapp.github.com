---
layout: post
title: Paperclip 2.3.1.1 and validate attachment's dimension
---

[Paperclip](<http://wiki.github.com/thoughtbot/paperclip/>) is an easy-to-use file upload gem released by [Thoughtbot](<http://thoughtbot.com/>). It provides several validations out of the box like validation on size (as in file size) of the attachment, if the attachment is present or not and so on. However, it does not have any validations on the dimensions of the file because sometimes you have to ensure the file is the correct dimension to avoid any design disasters.

To validate dimensions, one needs two things, namely:

1) Dimension of the file that is being uploaded and<br>

 2) Dimensions to validate against or the desired dimensions

One [tutorial](<http://roberto.peakhut.com/2010/01/14/paperclip_recipes/>), I found particular useful in my quest is by Roberto Soares. It doesn't exactly touch on the topic I am talking about here but it does point me in the right direction. He gives code to calculate the dimension of the file being uploaded, in case you would like to save the height and width of the file in the model.

**How is my problem different from Roberto's?**<br>

 1) I do not want to save the height and width of the file in the database.<br>

 2) My desired dimensions are already stored in a different model, i.e. I do not need to define it explicitly like other validations, such as validates\_length\_of :name, :within => 2..10

So, it is a particular sort of situation. Without any more discussions, here's the code:

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

Key thing to note, is the @queued\_for\_write attribute that is defined on Attachment class within Paperclip. This keeps hold of the original file that is being uploaded, which I then retrieve to get the dimensions. I simply compare the height and width in the validate method that gets called before save. This does work but it's a dirty hack and is impossible to reuse. Therefore, I am going to try and extract it out and make it more reusable. Stay tuned for it.

**Please Note:** This is just a monkey-patch and will increase your technical debt. Use it carefully, with an intention to refactor it as soon as possible.