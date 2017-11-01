---
layout: post
title:      "Key, value, or pair? A small hash mystery solved"
date:       2017-11-01 21:23:24 +0000
permalink:  key_value_or_pair_a_small_hash_mystery_solved
---

https://imgur.com/a/cFhf9

My first introduction to coding was trying to manipulate Flash sites with ActionScript (and then later, JavaScript), so when I started Learn I knew `for` loops and `var i` cold. I'd also taken some introductory Ruby classes on a site called [Skillcrush](https://skillcrush.com/), so I was getting through labs pretty easily and feeling more and more confident. Then I got to Hashes.

`Each` had been giving me a little trouble (where's my friend `var i`?), but by following the pattern, it was starting to make sense. The iterator is actually convenient and straightforward when you get used to it, even if the syntax is a little weird. Hashes were also new to me, although they have a nice analog in Javascript objects, so the concept wasn't really new. But iterating through multilevel Hashes made me realize how much I really didn't understand what was going on. How many words was `each` looking for, one or two? There were examples of both in the lessons, but I couldn't really figure out what the difference was. By following the pattern in the lesson example and strategic placement of Pry bindings, I did manage to get my tests to pass, but I did it with...an array. I could get the value of a Hash pair by doing something like `Hash.each { |entry| entry[1] }` but why did it work? 

After some fruitless Googling, I asked my husband (a software engineer) what was going on. His theory was that the single iterator probably represented the key-value pair, and the two iterators represented the key and value, respectively. And the pair was probably stored as an array somewhere, so addressable as `entry[1]`. I tested it out, and it worked as expected! This was a complete revelation to me, and it made Hashes much less intimidating.

Later, I spent some time with the Hash class documentation (http://ruby-doc.org/core-2.4.2/Hash.html) and learned that there are actually other / better iterators available in the Hash class, like `each_key`, `each_pair,` and `each_value`. So if you're lucky and start with one of those, you may never encounter the `each` confusion I had. But if you're not, I hope my small hash iterator mystery can help you figure out your hash iteration troubles.
