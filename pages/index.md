---
title: Fahrenheit 52
---

> "The best hygiene for beginning writers or intermediate writers is to write a hell of a lot of short stories. If you can write one short story a week—it doesn’t matter what the quality is to start, but at least you’re practicing, and at the end of the year you have 52 short stories, and I defy you to write 52 bad ones. Can’t be done. At the end of 30 weeks or 40 weeks or at the end of the year, all of a sudden a story will come that’s just wonderful." - Ray Bradbury

*I guess we'll find out!*

The Stories:

<% for (const num of Array(53).keys()) { _%>
<% for (const page of pages.filter(p => p.title !== 'Fahrenheit 52')) { _%>
<% if(num===page.week){ %>
   * [<%= page.title || pathTo(page) %>](<%= pathTo(page) %>)
 <% } else{ %>  
   * <%= num %>
<% } %>
<% } _%>
<% } _%>
