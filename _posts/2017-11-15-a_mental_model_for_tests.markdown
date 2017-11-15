---
layout: post
title:      "A mental model for tests"
date:       2017-11-15 15:38:11 +0000
permalink:  a_mental_model_for_tests
---


I've decided I'm going to use these blog posts to focus on things I've learned that have surprised me, or things that I figured out that changed my whole way of thinking about a concept. Once I figure a problem out, I usually realize that the thing I was stuck on wasn't actually that complicated, it's the picture of how it worked in my head that was leading me down the wrong path. This was recently the case for me in the Music Library CLI lab, so I thought I'd share my wrong understanding in the hope it sets your right.

The Music Library lab has a few classes (Song, Artist, Genre, and a few more) that all relate to each in multiple ways (I believe these are 'collaborating' classes) and a series of 12 test files that you're recommended to do in order. This leads you to build up a base level of functionality for each class, then go back and add some of the more complex interdependencies later. At that point, the tests can check for some fun concepts across classes like: if you create a new Song, are you also able to return that Song instance from the Artist's list of songs? 

I started to have trouble in the middle of this phase, in a way I recognize as a 'not returning the right thing from a method' problem. It was confusing, so I think I might have gamed the system a little and forced a method to return the type of thing the test was asking for (in this case, I think it was an array). No big deal, really, because it didn't impact much else. Until it did. Towards test 10 or 11, things got pretty weird. A test expected an instance of Song to be equal to an array that contained an instance of Song, again and again. Why? Why would you ever want that array? The test was so stupid for wanting that array.

In troubleshooting, I employed both of my resources, which are 1) Pry bindings, and 2) reading the rspec test. I read the test many times and was angry with it for expecting a strange result. I progressively placed bindings in every method in every class that the test touched, looking at what the data equaled in every step along the way. I'm a pretty visual thinker, as many of us are, and at some point I realized I was thinking of my code as a pipe, or more specifically (don't judge, I have a preschooler who likes craft projects) as a toilet paper tube. I was putting something into the tube, and the test was on the other side, expecting something out of the tube, and they should be the same but were not. Why? What did the test know that I didn't?

Guess what? At some point, a binding in the right place finally revealed that THE TEST IS ME (actually, I thought something more like 'the array is calling from inside the house!'). *I* was creating the array and instance of the Song. *My code* produced both the thing that went into the tube and *also* the thing that came out of the tube. The mistake in my understanding of the process was thinking that the test was programmed to know what it would get at the end. If the two things weren't equal, it was just because I had done something wrong -- specifically that weird array adjustment I'd made earlier. The test itself just knew what two places to touch that should be the same.

TL;DR: sometimes tests are comparing your code's input against your code's output, rather than your code's output against  predetermined data. If they expect something weird, that's a great indication that you've got something to fix. 
