---
layout: post
title:      "Getting Javascripty"
date:       2019-09-24 18:56:55 +0000
permalink:  getting_javascripty
---


The Rails-Javascript project was refreshingly small after coming from the Rails section. Instead of having to build an entire CRUD app with many requirements, Rails-JS only asked for new front-end functionality using Rails as an API. Exciting!

Because I work for a company that uses React, and I've been trying to make it known that I'm interested in working on front end development, I had taken a quick React detour after finishing the Rails project. I worked through all of the React labs and most of Redux, then used what I learned to work on a small CSS change for another team at my job. (Seeing React in a production code base gave me an appreciation for how complex React can get.) I was going to try to finish the final project before the Rails-JS section, but I realized it's not meant to work that way and had to get back into Rails again.

Returning to Rails was a little painful, but I eventually remembered how it worked. It wasn't until I got to the project, though, that I understood why there were so many API lessons. It hadn't clicked that Rails can be used as a backend API until I was actively trying to meet the project requirements. Now, I get it! 

My biggest challenge turned out to be figuring out how to use vanilla Javascript with Rails. We no longer use jQuery at work, so I didn't want to rely on (or learn more about) jQuery in my project, but I immediately missed the `$(document).ready()` function. I changed my initial function call to happen after `DOMContentLoaded`, but I continued to have a few strange errors about variables, and later classes, being declared multiple times. In diagnosing this problem, I learned about Turbolinks.

Had I read the links on the project requirements page, I would have known that Turbolinks, a library that tries to make navigating your web application faster, has its own set of events that supersede the regular DOM events. I wasn't sure if the events were causing my problem or if it was something related to the Rails stance that [Javascript should be kept in a single file](https://stackoverflow.com/questions/26192826/confused-about-how-to-use-vanilla-javascript-with-ruby-on-rails), rather than the page-specific files that I was using. I ended up turning Turbolinks off and keeping my page-specific files, and eventually my errors resolved themselves, so perhaps it was a Turbolinks issue.

Other things that were tricky included getting my has-many relationships to show up correctly, until I found [a well-explained blog post]([https://www.thegreatcodeadventure.com/building-a-super-simple-rails-api-json-api-edition-2/](https://www.thegreatcodeadventure.com/building-a-super-simple-rails-api-json-api-edition-2/)) by Sophie DeBenedetto, and learning how to send a POST request using AJAX but not using jQuery. For the form, I ended up using` XMLHttpRequest.send()` and a `FormData` object, but there was a brief moment when I thought I'd have to manually serialize my form data to be able to display it on screen (`FormData` [cannot be stringified](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest/Using_XMLHttpRequest#Submitting_forms_and_uploading_files)).

Now that this project is complete, I'm excited to get back to React and review how it all works!
