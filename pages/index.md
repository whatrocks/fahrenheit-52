---
title: Fahrenheit 52
---

> "The best hygiene for beginning writers or intermediate writers is to write a hell of a lot of short stories. If you can write one short story a week—it doesn’t matter what the quality is to start, but at least you’re practicing, and at the end of the year you have 52 short stories, and I defy you to write 52 bad ones. Can’t be done. At the end of 30 weeks or 40 weeks or at the end of the year, all of a sudden a story will come that’s just wonderful." - Ray Bradbury

*I guess we'll find out!*

Fahrenheit 52 was a weekly writing challenge that I did in 2022. At the end of the week, I (or a guest!) read that week's story aloud and released it as an episode in the [Fahrenheit 52 podcast feed](/podcast.xml). If audio's not your thing, you can subscribe to the [blog RSS feed](/rss.xml) instead. 

My goal for this project was to have fun and practice writing. And it worked! Thanks for checking it out!

**Read the stories:**

<ul>
<% for (const num of Array(53).keys()) { _%>
<% var match = pages.find(p => p.week === num); %>
<% if(match){ %>
<li><a href=<%=pathTo(match) %>><%=match.title %></a></li>
<% } else{ %>  
<li>Week <%=num %></li>
<% } %>
<% } _%>
</ul>

**Listen to the stories:**

<div class="podcasts">

[![Podcasts](podcasts.svg)](https://podcasts.apple.com/us/podcast/fahrenheit-52/id1600947555)

[![Overcast](overcast.svg)](https://overcast.fm/itunes1600947555)

[![Spotify](spotify.png)](https://open.spotify.com/show/0CatFy1udJkcp8OkwwXp4b)
</div>