---
date: '2011-09-28T02:40:00.002-07:00'
description: ''
published: true
slug: 2011-09-running-totals-in-excel_39
tags:
- MS Office
- http://schemas.google.com/blogger/2008/kind#post
- MS Excel
- legacy-blogger
time_to_read: 5
title: Running Totals in Excel
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2011/09/running-totals-in-excel_39.html)*.

Excel does not have a running total feature or function built in.  All the examples I found on the web to do running totals included VBA code. Not that I have anything against VBA but I thought there should be a way to do running totals with built in worksheet functions.<br /><br />Enter our one of our favorite functions: OFFSET().  But first, what is a running total?<br /><br /><img alt="Running Total Example" class="alignright" height="243" src="https://dl.dropboxusercontent.com/u/480457/techshorts/2013/07/RunningTotalExample01.png" width="292" /><br /><br />A running total is when you have a list of Values and you want to total of the current Value with the Previous values.  <a href="http://en.wikipedia.org/wiki/Running_total" target="_blank" title="Running Total">Wikipedia</a> states that a running total is "summation of a sequence of numbers which is updated each time a new number is added to the sequence, simply by adding the value of the new number to the running total."<br /><br />The key to getting the SUM() correct is getting the Range correct.  For a given Range of Values, start with the First number and SUM() until you get to the current row.  You can do this by using the OFFSET() function and taking advantage of Excel's table features to get the column range.<br /><br />[vb] OFFSET ( cell reference, rows, columns, [ height ], [ width ] ) [/vb]<br /><br />In the above case the Running Total column's formula becomes:<br /><br />[vb] =SUM( OFFSET( [Values], 0, 0, ROW() - ROW([Values]) + 1, 1 ) ) [/vb]<br /><br />[Values] is the Column we want the running total for.<br /><br />rows = 0 and columns = 0 because we want to start at the very first cell of [Values]<br /><br />[width] = 1 because we want only the [Values] column<br /><br />[height] = ROW() - ROW([Values]) + 1, this is the magic line.<br /><br />To get the height we have to figure out our current Row number, subtract off the starting Row of [Values] then add 1.  ROW([Values]) gives us the starting row of the column and ROW() gives us the current row.  For example, if the Table starts on row 3 (headers are on row 3) then the column [Values] starts on row 4.  The height of the very first cell in [Values] is:<br /><br />[vb] ROW() - ROW([Values]) + 1 = 4 - 4 + 1 = 1 [/vb]<br /><br />The height of the 3rd cell in the [Values] column is:<br /><br />[vb]ROW() - ROW([Values]) + 1 = 6 - 4 + 1 = 3 [/vb]<br /><br /><a href="http://www.navigatorpf.com/tutorials/offset-function-excel" target="_blank">Offset Function in Excel</a><br /><br /><a href="http://en.wikipedia.org/wiki/Running_total" target="_blank">Running Total</a>