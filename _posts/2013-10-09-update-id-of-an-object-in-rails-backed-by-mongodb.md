---
layout: post
title: 'Update id of an object in Rails backed by MongoDB '
---

I'm not a big fan of developers getting swayed by NoSQL hype and using mongoDB with Rails. Unless there's a good enough reason, stick to relational databases.

Anyways, I found myself trying to update id of an object in Rails. Tried it in rails console first and it didn't work as the id is a read-only field. Next stop, mongo console. Don't ask my why I'm updating the id, because I have to, unfortunately.

Here are the steps:

1\. Start mongo console by running 'mongo' on the command line (terminal, iterm)

2\. Run following commands in order:

 ```
 show dbs;
 use <your-database_name>;
 doc = db.<collection>.findOne({_id: ObjectId('required-id')});
 doc._id = ObjectId('new-id');
 db.<collection_name>.insert(doc);
 ```

 If you want you can delete the old document, but apparently you can't update the id. You will have to clone the doc and give it a new id, and then insert into collection, which is what we've done.
Took me a little while to get this working, essentially due to my lack of understanding of mongoDB in general.

**Update:**

In the commands above, I forgot to commit the insertion to the disk. Please don't forget to run this at the end:

```
db.<collection_name>.commit;
```
