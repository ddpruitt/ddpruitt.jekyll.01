---
date: '2011-01-10T07:04:00.000-08:00'
description: ''
published: true
slug: 2011-01-simple-mapreduce
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Simple MapReduce
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2011/01/simple-mapreduce.html)*.

Open file, read in lines, return individual words, get length of each word, Order by the length of the words, count each word of specific length.<br /><br />[csharp]<br /><br />static void Main()<br />{<br />	<br />	var counts = OpenFileReturnWords(@&quot;LoremIpsumDolor.txt&quot;)<br />		.AsParallel().Select(w=&gt;w.Length)<br />		.AsParallel().ToLookup(k =&gt; k)<br />		.Select(c =&gt; new { Number = c.Key, CountOfNumber = c.Count() })<br />		.OrderBy(c=&gt;c.Number);<br /><br />	foreach (var count in counts)<br />		Console.WriteLine(&quot;Count of {0:0000}: {1}&quot;, count.Number, count.CountOfNumber);<br /><br />	Console.WriteLine(&quot;Total Count: {0}&quot;, counts.Sum(c=&gt;c.CountOfNumber));<br />}<br /><br />public static IEnumerable&lt;string&gt; OpenFileReturnWords(string fileName)<br />{<br />	using (var reader = new StreamReader(fileName))<br />	{<br />		string line;<br />		while ((line = reader.ReadLine()) != null)<br />		{<br />			var wordsInLine = line.Split(new[] {' ', '.'})<br />				.Where(word =&gt; !string.IsNullOrEmpty(word));<br /><br />			foreach (var word in wordsInLine) <br />				yield return word;<br />		}<br />	}<br />	yield break;<br />}<br /><br />[/csharp]