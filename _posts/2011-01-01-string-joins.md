---
date: '2011-01-04T08:27:00.000-08:00'
description: ''
published: true
slug: 2011-01-string-joins
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: String Joins
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2011/01/string-joins.html)*.

I've seen a lot of code to generate SQL statements.  Invariable the programmer has an array of strings that they loop through (for example to put into an IN clause) and they always have a check to see of the current item is the first or last in the list.  The typical usage is to have a <strong>StringBuilder </strong>and an <strong>if </strong>statement which determines if an extra comma (or plus sign or whatever) is added or left out.<br /><br />I say: <strong>Stop Doing That!</strong><br /><br />Use the string.Join().<br /><br />[csharp]<br /><br />var strings = new[] {  &quot;Darren&quot;, &quot;Dawn&quot;, &quot;Thomas&quot;, &quot;Zoey&quot; };<br /><br />var results = string.Format(&quot;Replace \&quot;{0}\&quot; with {1} Question Marks: ({2})&quot;,<br />	string.Join(&quot;,&quot;, strings), strings.Length,<br />	string.Join(&quot;,&quot;, Enumerable.Repeat(&quot;?&quot;, strings.Length))<br />	);<br /><br />Console.WriteLine(results);<br /><br />[/csharp]<br /><br />The resulting output is:  <br /><br /><code>Replace "Darren,Dawn,Thomas,Zoey" with 4 Question Marks: (?,?,?,?)</code>