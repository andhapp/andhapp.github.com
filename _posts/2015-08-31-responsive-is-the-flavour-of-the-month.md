---
layout: post
title: Responsive is the flavour of the month
---

You don't have mobile and desktop anymore.

You have devices!

Small devices equate to mobile, medium ones to tablets, large to desktops and extra-large to retinas. I understand the whole responsive thing to an extent but to learn a bit more about the tools and techniques out there, I took the [Responsive Images](<https://www.udacity.com/course/responsive-images--ud882>) course at Udacity. It was to the point, concise and free. Here are a few things I picked up:

- [SVG Optimiser](<http://petercollingridge.appspot.com/svg-optimiser>)
- [pixel density](<http://pixensity.com/>) across different phones
- [Picture](<https://developer.mozilla.org/en-US/docs/Web/HTML/Element/picture>) element and the srcset attribute to provide a list of fallback options to the browser. srcset passes the responsibility of downloading and rendering the right image for the right device.
- [calc](<https://developer.mozilla.org/en-US/docs/Web/CSS/calc>) for figuring out the margin and width dynamically.
- There's an easy way to create your responsive images via [grunt](<https://github.com/andismith/grunt-responsive-images>). I couldn't find a similar thing for webpack, as webpack works quite differently from grunt (or gulp).

All in all, I enjoyed going through the videos and doing the exercises and highly recommend it to anyone feeling a bit weak on the whole responsive thing.
