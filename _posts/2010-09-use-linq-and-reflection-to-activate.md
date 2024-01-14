---
date: '2010-09-05T07:58:00.000-07:00'
description: ''
published: true
slug: 2010-09-use-linq-and-reflection-to-activate
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Use Linq and Reflection to Activate Interface and Execute a Method.
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2010/09/use-linq-and-reflection-to-activate.html)*.

I created a simple ICommand interface similar to the one in System.Windows.Input:<br />[csharp]interface ICommand<br />{<br />	string Description { get; }<br />	bool CanExecute(object parameter);<br />	void Execute();<br />}[/csharp]<br />In my project I created a bunch of classes that implement my ICommand interface and I wanted to find and execute them all.  I came up with two ways to do this, using a List&lt;ICommand&gt; and reflection.<br /><h2>List&lt;ICommand&gt;</h2><br />This is very direct and easy but as I added new commands the list began to grow. Also I had to remember to add my commands to the list as I created them.<br />[csharp]<br />string separator = new string('=', 100);<br />var commandsToExec = new List&lt;ICommand&gt;<br />						{<br />							new Commands.TestEntityConnectionStringBuilderCommand(),<br />							new Commands.BenchmarkingExampleCommand(),<br />							new Commands.FastTokenizerBenchmarkCommand(),<br />							new Commands.LinqToXmlTest01()<br />						};<br />foreach (var cmd in commandsToExec)<br />	if (cmd.CanExecute(null))<br />	{<br />		Console.WriteLine(&quot;{0}{1}{2}{1}{0}{1}&quot;, separator, Environment.NewLine, cmd.Description);<br />		cmd.Execute();<br />		Console.WriteLine(&quot;{1}{0}{1}{1}&quot;, separator, Environment.NewLine);<br />	}<br />[/csharp]<br /><h2>Reflection</h2><br />Using linq I find all the types in my Assembly that implements the ICommand interface.  I then loop through the results, create an instance of the object and cast it as a ICommand and then call the execute method.<br />[csharp]<br />var commandClasses = from type in Assembly.GetExecutingAssembly().GetTypes()<br />						where type.GetInterfaces().Contains(typeof(ICommand))<br />						select type;<br />foreach (var commnadType in commandClasses)<br />{<br />	var cmd = Activator.CreateInstance(commnadType) as ICommand;<br />	if (cmd.CanExecute(null))<br />	{<br />		Console.WriteLine(&quot;{0}{1}{2}{1}{0}{1}&quot;, separator, Environment.NewLine, cmd.Description);<br />		cmd.Execute();<br />		Console.WriteLine(&quot;{1}{0}{1}{1}&quot;, separator, Environment.NewLine);<br />	}<br />}<br />[/csharp]