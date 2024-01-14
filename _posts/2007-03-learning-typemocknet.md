---
date: '2007-03-31T15:26:00.000-07:00'
description: ''
published: true
slug: 2007-03-learning-typemocknet
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Learning TypeMock.Net
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2007/03/learning-typemocknet.html)*.

We need to implement a better unit testing strategy at work but unfortunately we have code that is not written to be unit tested.  Our unit test rely on the state of our database and this has caused so many issues that I'm hesitant to even run them.<br /><br />To fix the issue I have started working with <a href="http://www.typemock.com/" target="_blank" title="TypeMock.Net">TypeMock.Net</a> an AOP mocking tool.  TypeMock will intercept calls to objects that are called by the code you are testing without actually creating or executing the object.  I'm still fuzzy on the details but I plan on using this tool to help me test some pretty untestable code.