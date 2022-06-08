---
layout: post
title:  "Link_to and Link_to_unless"
date:   2022-01-18 12:12:46 +0000
categories: Rails
permalink: "/link_to-and-link_to_unless_current/"
---

Building a navigation bar in Rails is pretty easy. You simply write up something like:

    <nav class="hidden md:flex space-x-10">
        <%= link_to "Demo", "/demo", class: "text-with-padding" %>
        <%= link_to "Docs", "/documentation", class: "text-with-padding" %>
        <%= link_to "Pricing", "/pricing", class: "text-with-padding" %>
    </nav>
 
 And you get a set of urls for your link that look like this:
 
 ![Links](/img/hieroglyph links Screenshot 2022-01-18 085621.png)
 
 However if you are on the "Docs" page already then you dont't really need the "Docs" link to be a link. It could just be text. Simple enough, use `link_to_unless_current` instead of `link_to`.
 
    <nav class="hidden md:flex space-x-10">
        <%= link_to_unless_current "Demo", "/demo", class: "text-with-padding" %>
        <%= link_to_unless_current "Docs", "/documentation", class: "text-with-padding" %>
        <%= link_to_unless_current "Pricing", "/pricing", class: "text-with-padding" %>
    </nav>

The problem is that when you end up on the "Docs" page it looks like this:

![Links borked](/img/hieroglyph links Screenshot borked docs link 2022-01-18.png)

What happened? Well, the "Docs" line was rendered as plain text instead of a normal `<a>` tag link. This means that line also didn't render it's `text-with-padding` class and no CSS was applied to it. Without the CSS the padding was lost and "Docs" went and cozied up to the "Demo".

We can fix this by moving the class to a wrapping div and get the best of both worlds: styling and `link_to_unless_current`.

    <nav class="hidden md:flex space-x-10">
        <div class="text-with-padding">
            <%= link_to_unless_current "Demo", "/demo" %>
        </div>
        <div class="text-with-padding">
            <%= link_to_unless_current "Docs", "/documentation" %>
        </div>
        <div class="text-with-padding">
            <%= link_to_unless_current "Pricing", "/pricing" %>
        </div>
    </nav>

This is more lines of code but that is the trade-off. Have fun and choose your own adventure!

**Screenshots taken from *[Hieroglyph Screenshots](https://www.hieroglyphscreenshots.com)*.**
  
  
