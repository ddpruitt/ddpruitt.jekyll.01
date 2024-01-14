---
date: '2009-02-25T07:35:00.000-08:00'
description: ''
published: true
slug: 2009-02-dataset-more-reasons-to-not-like-it
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- Rant
- legacy-blogger
time_to_read: 5
title: 'DataSet: More reasons to not like it'
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2009/02/dataset-more-reasons-to-not-like-it.html)*.

So I am still living in the world of DataSets, when will I ever learn?<br /><br />The task was simple, take the contents of DataSetA and merge it into DataSetB.  Sure, just use:<br /><div style="margin-left: 40px;"><br />DataSetA.Merge(DataSetB, true)<br /></div><br />and life will be good.  But wait!  Why is it when I try to save the merged data from DataSetB to the database it doesn't show up?<br /><br />Because the RowState of all the rows in all the tables are set to Unchanged!  And a merge operation does not change the RowState.  So if I want all the data from B to be saved to A I have to change all the row states of all the tables to Added.  Sure, I should be able to loop thorough it all and set the row's state as such:<br /><br /><div style="margin-left: 40px;">row.RowState = DataRowState.Added;<br /></div><br />Not so fast grasshopper!  row.RowState does not have a setter!  Isn't that Asinine!  You have to use:<br /><br /><div style="margin-left: 40px;">row.SetAdded();<br /></div><br />What ever, I say setter, you say method.  Long story short I created an extension method that works.<br /><br />public static DataSet MergerAllDataAsNew(this DataSet target, DataSet source)<br />{<br />    foreach (DataTable table in source.Tables)<br />        foreach (DataRow row in table.Rows)<br />            row.SetAdded();<br /><br />    target.Merge(source, true);<br /><br />    return target;<br />}<br /><br />Brute Force works.