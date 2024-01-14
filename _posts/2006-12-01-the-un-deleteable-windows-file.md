---
date: '2006-12-21T02:33:00.000-08:00'
description: ''
published: true
slug: 2006-12-the-un-deleteable-windows-file
tags:
- http://schemas.google.com/blogger/2008/kind#post
- General
- legacy-blogger
time_to_read: 5
title: The Un-Deleteable Windows File
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/12/the-un-deleteable-windows-file.html)*.

<p>I have several Open Source projects I am following and to facilitate downloading the code I created a simple NAnt script.&nbsp; The script worked great until the other day one of the projects started failing to update.</p> <p>Most of the projects I'm tracking are in Subversion.&nbsp; All I'm doing is checking out the trunk then about once or twice a week doing an update.&nbsp; So when the project started failing to update I figured it would be a simple matter of deleting the project folder and just checking it out again.</p> <p>Wasn't going to happen.&nbsp; One of the directories would no delete, no matter what I tried.&nbsp; I tracked it down to a couple of file in hidden _svn folders.&nbsp; I could delete every other file in this folder except for these.&nbsp; Nothing seemed to work.</p> <p>I finally dropped to a command window and attempted to DEL the file, that is when I got the first real clue what the problem was:&nbsp; the file name&nbsp; was too long.&nbsp; The root folder of all the projects I was updating was on my Desktop so the path was already super long: C:\Documents and blah blah buried deep in the bowls of the hard drive long\Desktop.</p> <p>So I moved the root folder to my c:\ and sure enough I was able to delete the folders.</p> <p>Funny how that works.</p>