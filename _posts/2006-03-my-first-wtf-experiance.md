---
date: '2006-03-15T09:18:00.000-08:00'
description: ''
published: true
slug: 2006-03-my-first-wtf-experiance
tags:
- http://schemas.google.com/blogger/2008/kind#post
- Rant
- General
- legacy-blogger
time_to_read: 5
title: My First WTF Experiance
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/03/my-first-wtf-experiance.html)*.

<p>OK, so I have seen bad code in the past.&nbsp; Hell, I&rsquo;ve written some pretty bad code in the past, present and will in the future.&nbsp; But what I am looking at right now just blows my freaking mind.</p><p>A stored procedure that generates dynamic SQL to parse an XML document stored in a table which then somehow drives a cursor to fetch one row from something the dynamic sql calls that then drives another cursor that uses OPENXML to get data from another xml document.</p><p>I can&rsquo;t figure it out!&nbsp; Why?&nbsp; Who was the clever SOB that thought this could even remotely be a good idea?</p><p>WTF?!!?</p>