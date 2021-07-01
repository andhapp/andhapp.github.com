---
layout: post
title: ActiveModel API and Parameter Object design pattern
---

About 3 months ago, I was working on this piece of code which had some "virtual models". Virtual models are the entities that are well defined models except they are never persisted to the database. They are just kept in memory and discarded. You could by all means persist them but I didn't have to do it at the time.

The application had a search interface (that allowed users to search across the application). We all know any user interaction needs robust validations and it was same for this application as well. The interface allowed users to select 4 (or 5) different filters to search across. So. the task was to capture the user supplied search filters and validate them and if valid search the and display the results based on it. There are several ways to solve this problem but I think with ActiveModel API the task at hand becomes really really easy.

ActiveModel API makes a [ruby object feel like activerecord](<http://yehudakatz.com/2010/01/10/activemodel-make-any-ruby-object-feel-like-activerecord/>). This essentially means creating one "Search" virtual model (object) and use ActiveModel API and add validations to it. And all the search filters are defined on the Search model itself which is in line with [Martin Fowler's Parameter Object design pattern](<http://www.refactoring.com/catalog/introduceParameterObject.html>). Well, better designed code promotes better practices.

Sorry, for absence of any code in this post as I did this ages ago and was for a client project. Please leave comments if you need any clarifications.