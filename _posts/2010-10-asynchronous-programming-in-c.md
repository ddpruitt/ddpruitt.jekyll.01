---
date: '2010-10-29T04:48:00.000-07:00'
description: ''
published: true
slug: 2010-10-asynchronous-programming-in-c
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Asynchronous Programming in C#
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2010/10/asynchronous-programming-in-c.html)*.

<a href="http://blogs.msdn.com/b/somasegar/archive/2010/10/28/making-asynchronous-programming-easy.aspx" target="_blank">Making Asynchronous Programming Easy</a><br /><br /><a href="http://blogs.msdn.com/b/ericlippert/archive/2010/10/29/asynchronous-programming-in-c-5-0-part-two-whence-await.aspx">Asynchronous Programming in C#</a><br /><br />[csharp]public async void AsyncIntroParallel()<br />{<br />    Task&lt;string&gt; page1 = new WebClient().DownloadStringTaskAsync(new Uri(&quot;http://www.weather.gov&quot;));<br />    Task&lt;string&gt; page2 = new WebClient().DownloadStringTaskAsync(new Uri(&quot;http://www.weather.gov/climate/&quot;));<br />    Task&lt;string&gt; page3 = new WebClient().DownloadStringTaskAsync(new Uri(&quot;http://www.weather.gov/rss/&quot;));<br /><br />    WriteLinePageTitle(await page1);<br />    WriteLinePageTitle(await page2);<br />    WriteLinePageTitle(await page3);<br />}[/csharp]<br /><br />Async CTP has been released.  Note:  This is not automatically Multi-Threading!  From the CTP:<br /><blockquote><br />Merely sticking the "Async" modifier will not make a method run on the<br />background thread. That is correct and by design. If you want to run code on a<br />background thread, use TaskEx.Run(). Please read the overview for an explanation<br />of asynchrony.<br /></blockquote>