---
title: Fahrenheit 52
---
# Fahrenheit 52

"Write a short story every week. It's not possible to write 52 bad short stories in a row" - Ray Bradbury

I guess we'll find out!

The Stories:
<% for (const page of pages) { _%>
* [<%= page.title || pathTo(page) %>](<%= pathTo(page) %>)
<% } _%>