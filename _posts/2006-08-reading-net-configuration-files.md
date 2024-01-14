---
date: '2006-08-09T08:20:00.000-07:00'
description: ''
published: true
slug: 2006-08-reading-net-configuration-files
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Reading .NET Configuration Files
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/08/reading-net-configuration-files.html)*.

<p>I am currently working on a small app that will scan our environment and verify that all the configuration settings are correct.&nbsp; One thing I found was that you can&rsquo;t open&nbsp;just any&nbsp;.config file using System.Configuration, it has to be named the same as the calling assembly.</p><p>What a pain.</p>