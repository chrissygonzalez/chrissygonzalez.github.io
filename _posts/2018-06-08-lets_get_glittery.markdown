---
layout: post
title:      "Let's Get Glittery"
date:       2018-06-08 23:45:31 +0000
permalink:  lets_get_glittery
---


For some reason, one of my programming goals has always been to create my own glitter text app, one of those sites that let you enter text and generate a ridiculous, sparkly version of it, like this: ![poop](https://i.imgur.com/8jCMfAb.gif). 

If you've never seen one, I think they're a hidden (maybe forgotten?) gem of the internet, but they're always covered in untrustworthy-looking ads and feel a little sketchy.

When I finally got to the Sinatra project, I was ready to create, read, update, and delete all the glitter text I could! But I had no idea how to do it. I decided a user would probably enter information that could turn into some sort of CSS, and I then could eventually glitterize the output when I figured out how. Modeling that data was pretty simple – I made a User with sign up credentials (username, email address, and password), and I made a glitter text, which I decided to call a Drawing. A Drawing could have any number of attributes that would make up the visual presentation, to be determined.

My first step for building my own glitter text, after modeling my data and writing the migrations, was to make some hard-coded examples and then figure out what attributes a Drawing would need based on that. I created a div, gave it a background color, text color, tried some display fonts from [Google Fonts](https://fonts.google.com/), played around with some gradients, and pretty soon, I had a delightfully garish word-image. Then I found a glittery animated gif to use as a background, and that took things to the next level. I had originally thought I would build a Drawing from a background color or gradient with a transparent animated gif on top, but a regular animated gif was much easier. Using what I'd learned from my div experiment, I built out my Drawing migration and got an instance of the class to display the colors, fonts, and backgrounds I had entered. Hooray!

I went on to build out my routes in the usual way by following previous lab assignments (Fwitter and Playlister) closely. It was a little strange to have no tests! I almost decided to try to write some, but in the interest of time, I deferred that to future work. Most of my time went into fussing with the CSS to make my app feel presentable (I am a designer, after all), and refactoring the Drawing class. I realized early on that the presentation attributes felt wrong in the Drawing class and moved them into their own class, called Theme. I started to have dreams of letting users enter their own Themes, but that also seemed a little out of scope, so I added it to my list for later.

When I was close to being done with my routes and CSS fussing, I re-read the requirements and noticed that I needed validations for user input. I had a vague memory of one lab validating for something, so I looked it up and found [validations in ActiveRecord](http://guides.rubyonrails.org/active_record_validations.html). I managed to get errors working for creating a new drawing, and then I needed a flash message to display the errors. The flash message in Playlister gave me a lot of [trouble](https://github.com/learn-co-curriculum/playlister-sinatra/issues/60), so this time I tried [sinatra-flash](https://github.com/SFEley/sinatra-flash) instead of [rack-flash](https://github.com/nakajima/rack-flash). The instructions honestly made no sense to me until I found a [helpful gist](https://gist.github.com/cmkoller/0d3b048b3c4b48ee4955), which gave a nice example I could follow to get a flash message to appear. I briefly broke my User class trying to add validations to the sign up form, but eventually that worked, too, and I added validations to every form in the app. 

Although I could keep working on this first version of Glitter Text for weeks, this feels like a pretty good first pass at exploring the possibilities. I look forward to coming back to it when I know how to build more!

![lets get glittery](https://i.imgur.com/Ss8J0NO.gif)

