---
layout: post
title:      "Building a piano with Javascript"
date:       2019-12-04 21:30:26 -0500
permalink:  building_a_piano_with_javascript
---


I started the Flatiron School's online program before there was an upper limit on how long you could stay in the program, which was great because it made it livable as a working parent, but as time dragged on, I started feeling desperate to just be done with it already. At the beginning of the React section, I decided my only time goal was just to please please manage to graduate in less than two and a half years. I'm proud to say that (fingers crossed that I pass the final assessment) I'll be just squeaking in under the line at two years, five months. Yay, me.

For each of the five portfolio projects, I aimed to built something useful to my life at the time. For this final portfolio project, I decided I'd like a tool to compose simple songs (as a way to encourage my daughter to practice the guitar) that incorporated some sort of external library, and I got closer than I ever have to building something like the initial idea. I wasn't able to include all the features I wanted to, of course, but I'm pretty happy to be finishing Flatiron with this as a starting point.

![Screenshot of Tone Piano](https://i.imgur.com/1z0goUh.png)

This project, Tone Piano, uses Ruby on Rails as a backend API and React as a frontend (as specified in the requirements), and incorporates the [Tone.js](https://tonejs.github.io/) library for the piano sounds. My general process was to first pull together a Tone.js proof of concept, so I could be sure I could actually get it to work, then slowly turn a hardcoded song composer into one that connected to React, then Redux, then the database, and then gradually separate things into components and refactor out the mess.

For the most part, this project went according to plan and I followed the process I'd outlined. I did run into a few problems, though. First, I had a difficult time understanding how to construct a song using Tone.js. It's pretty straightforward to make a single sound, but to save a series of them to be played back later turned out to be a little mysterious. I'm not familiar with music software or electronic music terminology at all (or the Web Audio API that Tone.js wraps), so it was hard to know where to focus my Googling. After much tutorial reading, the key to being able to make anything work at all turned out to be [this GuitarLand site](https://www.guitarland.com/MusicTheoryWithToneJS/PlayRhythms.html)  by Mike Sult. His examples saved me! He put everything in the source to be viewable, and copying and trial and error finally yielded a playable song. I will admit that I don't fully understand *how* it's working right now, but I plan to come back to it now that I have a first version built.

Another major problem I encountered was getting a song to save to the database. I used the same technique from the Rails-JS project – constructing an object from my form data and using `fetch` to send a `POST` request – but it just wouldn't work. A contributing factor was that I was [missing a pair of brackets](http://billpatrianakos.me/blog/2013/09/29/rails-tricky-error-no-implicit-conversion-from-symbol-to-integer/) (a giant thank you to  [Bill Patrianakos](http://billpatrianakos.me/) for that blog post). However, the main issue turned out to be that I had forgotten to include the `headers` object, and it turns out...it's necessary. In past Rails work, `headers` also contained a X-CSRF-Token for session security, but I had stripped out the whole object because I wasn't going to have Users, and I'd forgotten to add Content-Type back in. 

    fetch('/api/songs', {
       method:  'POST',
       headers: {
          'Content-Type':  'application/json'
       },
       body:  JSON.stringify(songObject)
       }) 

Finally, the biggest problem I had was figuring out how to render a Song show page. I could get React Router to give me different views, but I couldn't figure out how to pass the song `:id` parameter to the view that needed it. I find the React Router documentation to be a little hard to parse, so it took an annoying amount of Googling to finally get it. I'm not sure where I found the example that ultimately worked for me, but I found [this post](https://tylermcginnis.com/react-router-pass-props-to-components/) by Tyler McGinnis and [this post](https://learnwithparam.com/blog/dynamic-pages-in-react-router/) by Paramanantham Harrison to be particularly helpful. Besides not understanding how to pass and receive parameters in the route, I realized hadn't wrapped my head around using the Route to pass information at all, and it took some time to adjust my mental model from the old Rails route way of thinking.

    <Route  exact  path="/songs/:id"  render={(routerProps) =>  <SongView  {...routerProps}  newSong={false}/>}  redirectToList={false}  />

Actually, I suppose the final *final* difficulty I had was in keeping my components organized. I sort of discovered what I was going to build as I went, because I kept finding things I hadn't anticipated or understood before I got to them. There were many different versions of this component being connected to the Redux store then disconnected, or that component moving from class to functional component before I was able to settle on a structure that worked. Then I had to refactor everything to remove outdated bits and make everything clear. This is the first thing I've built that had this much revision, and although it was terrifying, it really was worth it. I went from feeling like I was moving pieces of a mess around to finally being able to picture (and draw) the way my components relate to each other. 

![React component architecture](https://i.imgur.com/aRm62dB.jpg)

For now, Tone Piano is in a state that meets this specific project's requirements, but in the future, I'd like to continue to add features and make improvements. Specifically, I'm hoping to: 

 - Improve the animation that shows when a song is playing
 - Allow songs to be edited and deleted
 - Figure out how to include rests and notes other than quarter notes
 - Rethink the way the notes and staff are rendered to include a treble clef on every row, and potentially a time signature and bars between measures
 - Add a funky sound or voice option for playback
 - Animate the intro piano graphic
 - Add print styles for printing sheet music
 - Redraw notes to be more correctly proportioned

And so much more! Stay tuned...

