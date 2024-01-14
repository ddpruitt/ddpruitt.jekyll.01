---
date: '2010-10-27T20:25:00.001-07:00'
description: ''
published: true
slug: 2010-10-uow-filehelpers
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- uow
- utility
- legacy-blogger
time_to_read: 5
title: 'UOW: FileHelpers'
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2010/10/uow-filehelpers.html)*.

The utility of the week is <a href="http://filehelpers.sourceforge.net/">FileHelpers</a>, a .Net library that works with delimited and fixed length files. It helps to import and export data from files, strings or streams.<br /><br />I found this recently as I needed to process several CSV files but I did not want to write by hand a parser. Been there, done that way too many times so I did a search and what do you know- someone smarter than me already did it.<br /><br />What I like about it is the wizard that comes with the library that helps to build plain old c# classes to work with the data rows. In about twenty minutes I had a working CSV processing engine complete with intellisense.<br /><br />The library is<a href="http://sourceforge.net/softwaremap/trove_list.php?form_cat=187" style="font-weight: bold; color: #330000;">BSD License</a><span style="font-weight: bold; color: #330000;">, </span><a href="http://sourceforge.net/softwaremap/trove_list.php?form_cat=16" style="font-weight: bold; color: #330000;">GNU Library or Lesser General Public License (LGPL)</a>