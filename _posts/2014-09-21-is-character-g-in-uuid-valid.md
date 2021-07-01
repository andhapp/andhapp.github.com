---
layout: post
title: Is character 'g' in UUID valid?
---

Did you know [UUID has a very detailed specification](<https://pretty-rfc.herokuapp.com/RFC4122>)? Well, if you did, good for you, if you didn't, it's okay, you can read it now.

For some reason, I always thought UUID (or GUID) is a random collection of numbers and characters and randomness guarantees uniqueness. I was pretty sure about the randomness but wasn't sure that presence of character 'g' makes it invalid.

Let's look at UUID's definition. UUID is in fact a random **128 bit number** and it's represented using hexadecimal numbers for the sake of readability. Now, let me ask you the same question again:

**Is character 'g' in UUID valid?**

Ofcourse, it's not valid!

**Why?**

Because hexadecimal digits don't include 'g'. Therefore, a valid UUID should always match:

<pre>/[0-9a-f]{8}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{4}-[0-9a-f]{12}/i
</pre>

So, presence of 'g' in UUID means that UUID specification has not been implemented correctly in the programming language.