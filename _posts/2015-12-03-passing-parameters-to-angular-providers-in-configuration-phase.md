---
layout: post
title: Passing parameters to Angular providers in configuration phase
---

Providers are probably the most significant concept in `Angular 1`. Services and factories use providers underneath, which makes it even more powerful. Anyways, `Angular 1` has two phases in it's lifecycle - configuration phase and run phase. Providers are initialised in the configuration phase. In this phase none of other angular services, like, `$http`, `$location` and so on are available to use. I had to pass some values to a custom provider and the only way you can do it is through the config defined on the module.

I never knew you could do that and this tiny post is just a note to self as a reminder.
