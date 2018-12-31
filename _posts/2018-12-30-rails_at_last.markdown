---
layout: post
title:      "Rails at last"
date:       2018-12-31 03:08:06 +0000
permalink:  rails_at_last
---


![Plan your crafts](https://i.imgur.com/8YU3yWB.jpg?1)

For my Rails section project, I decided to build a craft project planning app:  CraftPlanner. Besides working through the Learn curriculum, I have a full-time job, a kindergartner, and a backlog of at least ten very useful books I need to read. I also have a ton of crafty side projects I'd love to work on, including finishing a hat I'm knitting, crocheting a stuffed bear I started about a year ago (yikes) and any number of new things I stumble across on Instagram. I keep track of everything in a post-it note in Google Keep, which is fine, but it's lacking enough that a craft project organizer seemed like a great candidate for a new tool to build.

Looking back at my commit history, the CraftPlanner has taken me over three months to finish! Although each project seems to be taking a little longer than the last, this one really seemed to drag on, mainly because I had less free time to work on it, the holidays hit during this period, and  I had to do a ton more Googling and learning on my own to fulfill the requirements. I'd struggled with more than a few of the Rails labs, even when my tests passed, so I had a feeling a reckoning would be coming. And...it did.

I started work on October 24 and immediately spun my wheels on the schema. I don't remember exactly what was confusing, only that I stewed about it for awhile and lost some time. I eventually landed on including Crafts, which have many Materials through CraftMaterials, and Users, who have many Crafts through Projects. Users also have many Materials, through UserMaterials. I was originally going to call CraftMaterials Supplies, but I started to get confused by which class was an object and which class was a join. (For some reason Projects never confused me.)

![Schema sketch](https://i.imgur.com/T2ORpMx.jpg?1)

With the schema set, it was relatively easy to set up my app structure, write migrations, and get sign up, sign in, and sign out working with bcrypt. Basic craft and material views were also straightforward, but I knew the New Craft form, with nested attributes for Materials, was going to be tricky. I got the basic form working, then revisited it to add New Material fields, which was similar to the labs. The last step was getting to form to accept Quantity, an attribute only present on the join table, CraftMaterials. This turned out to very difficult! But it drove the most learning of any problem I had in this section.

Although the specific problems I had with adding a field to the join table are a little hazy now, I do remember the two concepts I needed to learn to get it working. First, I'd never really understood how nested forms worked, so I had to read blog posts like [this one](https://medium.com/@mindovermiles262/triple-nested-forms-in-rails-dedbcccb5799), documentation, and a lot of StackOverflow to wrap my head around it. It really is a bit of a nesting doll, using form helpers like `form_for` and `fields_for` to actually nest the fields. For example:

```
<%= form_for :first_item do |first| %>
  <%= first.fields_for :second_item do |second| %>
    <%= second.fields_for :third_item do |third| %>
      <%= third.some_field :field_name %>
    <% end %>
<% end %>
```

Second, when Rails form helpers can find the objects your form is referencing, it shows fields for each one that exists. If your fields are doubling unexpectedly, which happened when my forms had validation errors, you've managed to generate an extra object somewhere. And when your fields don't show up at all, which was the main problem I struggled with for weeks, you haven't built an object for Rails to generate fields on. I knew to build a new object for a `has_many` relationship, like `first_item.second_items.build` but I didn't know until I called into a Rails study group on November 13 that [it's done differently](https://stackoverflow.com/questions/783584/ruby-on-rails-how-do-i-use-the-active-record-build-method-in-a-belongs-to-rel) for a `belongs_to` relationship: `first_item.build_second_item`. Whaaat? I hadn't even suspected what to Google for that one.

After getting through the nested attributes roadblock, everything else was pretty solvable with continued searching and reading. I added another nested form for adding items to your Stash (aka UserMaterials), which interestingly required a few changes. I implemented Omniauth for Twitter. And I took a thirteen day break to enjoy Thanksgiving and read about CSS grid before trying to make my page layouts a little more presentable. 

The more I worked on the project, the more I got distracted by other improvements I wanted to make that were outside the scope of the requirements. In the interest of time, I decided to save them for future work. But in the future, I'd like to make it possible to add multiple materials when creating a new craft, add graceful fallbacks for browsers that don't support CSS grid and flexbox, style selects and nested fields when they have validation errors, and make crafts partially but not completely editable. 
