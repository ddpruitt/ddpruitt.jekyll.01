---
date: '2009-03-13T10:56:00.000-07:00'
description: ''
published: true
slug: 2009-03-datatable-finding-differences-in-column
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: 'DataTable: Finding Differences in Column Values'
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2009/03/datatable-finding-differences-in-column.html)*.

I have two tables in a typed DataSet and I want to compare one column in each table to see if TableA has values that are not in TableB.<br /><br /><div><pre style="margin: 0px;"><span style="color: rgb(43, 145, 175);">IEnumerable</span>&lt;<span style="color: blue;">string</span>&gt; valuesInA = typedDataSet.TableA.AsEnumerable().Select(row =&gt; row.AField);</pre><pre style="margin: 0px;"><span style="color: rgb(43, 145, 175);">IEnumerable</span>&lt;<span style="color: blue;">string</span>&gt; valuesInB = typedDataSet.TableB.AsEnumerable().Select(row =&gt; row.BField);</pre><pre style="margin: 0px;">&nbsp;</pre><pre style="margin: 0px;"><span style="color: blue;">foreach</span> (<span style="color: blue;">var</span> notInB <span style="color: blue;">in</span> valuesInA.Except(valuesInB))</pre><pre style="margin: 0px;">&nbsp;&nbsp;&nbsp; <span style="color: rgb(43, 145, 175);">Debug</span>.WriteLine(<span style="color: blue;">string</span>.Format(<span style="color: rgb(163, 21, 21);">&quot;Value not in TableB.BField: {0}&quot;</span>, notInB));</pre></div><br />This is assuming that both AField and BField are the same type.<br />