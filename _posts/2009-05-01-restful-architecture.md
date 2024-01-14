---
date: '2009-05-21T11:48:00.000-07:00'
description: ''
published: true
slug: 2009-05-restful-architecture
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- asp.net-mvc
- legacy-blogger
time_to_read: 5
title: RESTful Architecture
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2009/05/restful-architecture.html)*.

Found the following in the article <a href="http://blog.wekeroad.com/2007/12/06/aspnet-mvc-using-restful-architecture/">ASP.NET MVC: Using RESTful Architecture</a> and thought it worth noting.  It describes what the MVC command actions should be, no more than this is needed:<br /><blockquote style="font-style: italic;">The endpoint needs to be something meaningful, and Rails uses a nice convention that divides the endpoints into 7 main bits:<br /><ul><br />	<li> <span style="font-weight: bold;"> Index </span>- the main â€œlandingâ€ page. This is also the default endpoint.</li><br />	<li> <span style="font-weight: bold;"> List </span>- a list of whatever â€œthingâ€ youâ€™re showing them - like a list of Products.</li><br />	<li> <span style="font-weight: bold;"> Show </span>- a particular item of whatever â€œthingâ€ youâ€™re showing them (like a Product)</li><br />	<li> <span style="font-weight: bold;"> Edit </span>- an edit page for the â€œthingâ€</li><br />	<li> <span style="font-weight: bold;"> New </span>- a create page for the â€œthingâ€</li><br />	<li> <span style="font-weight: bold;"> Create </span>- creates a new â€œthingâ€ (and saves it if youâ€™re using a DB)</li><br />	<li> <span style="font-weight: bold;"> Update </span>- updates the â€œthingâ€</li><br />	<li> <span style="font-weight: bold;"> Delete </span>- deletes the â€œthingâ€</li><br /></ul><br />Normally the last 3 are â€œaction only â€ and donâ€™t have a view associated with them. So if you â€œcreateâ€ a Product (from the New view, using Create as the action on the form), youâ€™d just redirect then to the List or Edit views. Likewise if you Update a Product from the Edit page (using Update as the action on the form) you might want to go back to the Edit view and show a status update.</blockquote><br />I don't agree that this should be the ONLY command results you can have but I think it is a good guideline to follow.  Now I have to go update my MVC commands.