---
title: 'Scratching Parallel with StopWatch'
date: 2011-01-18T00:54:00.000-08:00
draft: false
url: /2011/01/scratching-parallel-with-stopwatch.html
tags: 
- .Net
---

Threw together a quick parallel stopwatch test. Not sure if the times prove anything.  
  
\[csharp highlight="28,33,39"\]  
using System;  
using System.Collections.Generic;  
using System.Diagnostics;  
using System.Linq;  
using System.Threading.Tasks;  
  
namespace Scratch.ParallelProcessing  
{  
class Program  
{  
static void Main(string\[\] args)  
{  
const int count = 10000000;  
var source1 = Enumerable.Range(0, count).ToArray();  
var source2 = Enumerable.Range(0, count).ToArray();  
var source3 = Enumerable.Range(0, count).ToArray();  
  
Stopwatch stopwatch = new Stopwatch();  
  
var parallelElapsedTimes = new List<TimeSpan>();  
var linearElapsedTimes = new List<TimeSpan>();  
var linqSelectElapsedTimes = new List<TimeSpan>();  
  
for (int i = 0; i < 10; i++)  
{  
stopwatch.Reset();  
stopwatch.Start();  
var parallelResults = Parallel.ForEach(source1, s => s %= 2);  
parallelElapsedTimes.Add(stopwatch.Elapsed);  
stopwatch.Reset();  
  
stopwatch.Start();  
LinearAction(source2, s => s %= 2);  
linearElapsedTimes.Add(stopwatch.Elapsed);  
stopwatch.Reset();  
  
stopwatch.Reset();  
stopwatch.Start();  
Array.ForEach(source3, s=>s = s%2);  
linqSelectElapsedTimes.Add(stopwatch.Elapsed);  
stopwatch.Reset();  
  
}  
  
Console.WriteLine("Elapsed Time\\t\\tMin\\t\\tMax\\t\\t\\tAvg");  
Console.WriteLine("============\\t\\t===\\t\\t===\\t\\t\\t===");  
Console.WriteLine("{0}\\t\\t{1}\\t\\t{2}\\t\\t\\t{3}", "Parallel", parallelElapsedTimes.Min(t => t.Milliseconds), parallelElapsedTimes.Max(t => t.Milliseconds), parallelElapsedTimes.Average(t => t.Milliseconds));  
Console.WriteLine("{0}\\t\\t\\t{1}\\t\\t{2}\\t\\t\\t{3}", "Linear", linearElapsedTimes.Min(t => t.Milliseconds), linearElapsedTimes.Max(t => t.Milliseconds), linearElapsedTimes.Average(t => t.Milliseconds));  
Console.WriteLine("{0}\\t\\t\\t{1}\\t\\t{2}\\t\\t\\t{3}", "Linq", linqSelectElapsedTimes.Min(t => t.Milliseconds), linqSelectElapsedTimes.Max(t => t.Milliseconds), linqSelectElapsedTimes.Average(t => t.Milliseconds));  
  
}  
  
public static void LinearAction<T>(IEnumerable<T> source, Action<T> action)  
{  
foreach (var s in source) action(s);  
}  
}  
}  
  
  
\[/csharp\]  
  
Results of the timer:  
`  
Elapsed Time Min Max Avg  
============ === === ===  
Parallel 63 191 79.5  
Linear 138 143 140.3  
Linq 54 56 54.5  
Press any key to continue . . .  
`  
  
I'm running 64 bit Vista on a Intel Core2 Duo with 4GB RAM. The Parallel seems to be inconsistent, and depends a lot on whether or not it grabs that second CPU.