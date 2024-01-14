---
date: '2008-02-05T14:42:00.000-08:00'
description: ''
published: true
slug: 2008-02-value-objects-as-measurement-objects
tags:
- http://schemas.google.com/blogger/2008/kind#post
- General
- legacy-blogger
time_to_read: 5
title: Value Objects as Measurement Objects
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2008/02/value-objects-as-measurement-objects.html)*.

So I was reviewing PEAA looking to see if Fowler had come up with the idea of Measurment Objects, that horse I've been kicking around lately.&nbsp; I found that he has a couple of close patterns:&nbsp; Value Object and Money.<br /><br />Value Object:&nbsp; <span style="font-style: italic;">A small simple object, like money or a date range, whose equality isn't based on identity.</span><br /><br />Money: <span style="font-style: italic;">Represents a monetary value.</span><br /><br />According to Fowler&nbsp;Value Objects are light weight and almost primative types.&nbsp; They should also me immutable since they have no identity.&nbsp; He also suggests that in .NET structs could be used as Value Objects.<br /><br />The money pattern looks like a special case of a Measurement Object with the UnitOfMeasure being set to currency (currency being USD or Euro).<br /><br />I see the usefulness of using structs but there is the boxing issue if we implement them with interfaces.<br /><br />I will have to ponder on this.<br />