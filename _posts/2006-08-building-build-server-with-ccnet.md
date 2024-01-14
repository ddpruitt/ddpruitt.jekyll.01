---
date: '2006-08-31T01:12:00.000-07:00'
description: ''
published: true
slug: 2006-08-building-build-server-with-ccnet
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Building a build server with CC.NET
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/08/building-build-server-with-ccnet.html)*.

<p>So I have started implementing CruiseControl.Net at work and I have to say it is pretty fun.&nbsp; I&rsquo;ve built a bunch on Nant scripts to build our SOA middle tier,&nbsp;installed CC.Net and setup the first project.</p><br /><p>What I am struggling with now is getting VSS to update the source files.&nbsp; I think I am just missing something small but for some reason I can&rsquo;t get the files to update.</p><br /><h2>Update</h2><br /><p>&nbsp;I finally had to create NAnt scripts to update the actual source.&nbsp; The VSS task in CC.Net only monitors the VSS DB for changes, it does not actually down load the latest source.&nbsp; At least as far as&nbsp;I could tell it does not.</p><br /><p>Next is to get the VSS labeled.&nbsp; CC.Net will label the source but it is not descriptive enough so it will be a trip back to the NAnt scripts.</p>