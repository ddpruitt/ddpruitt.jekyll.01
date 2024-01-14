---
date: '2010-10-27T20:25:00.000-07:00'
description: ''
published: true
slug: 2010-10-threading-autoresetevent-example
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Threading AutoResetEvent Example
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2010/10/threading-autoresetevent-example.html)*.

[csharp]public class Program<br />{<br />	private static System.Threading.AutoResetEvent stopFlag = new System.Threading.AutoResetEvent(false);<br />	public static void Main()<br />	{<br />		ServiceHost svh = new ServiceHost(typeof(ServiceImplementation));<br />		svh.AddServiceEndpoint(<br />			typeof(WCFSimple.Contract.IService),<br />			new NetTcpBinding(),<br />			&quot;net.tcp://localhost:8000&quot;);<br />		svh.Open();<br />		Console.WriteLine(&quot;SERVER - Running...&quot;);<br />		stopFlag.WaitOne();<br />		Console.WriteLine(&quot;SERVER - Shutting down...&quot;);<br />		svh.Close();<br />		Console.WriteLine(&quot;SERVER - Shut down!&quot;);<br />	}<br />	public static void Stop()<br />	{<br />		stopFlag.Set();<br />	}<br />}[/csharp]