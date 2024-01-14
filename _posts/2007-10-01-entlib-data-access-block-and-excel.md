---
date: '2007-10-10T04:39:00.001-07:00'
description: ''
published: true
slug: 2007-10-entlib-data-access-block-and-excel
tags:
- http://schemas.google.com/blogger/2008/kind#post
- General
- legacy-blogger
time_to_read: 5
title: EntLib Data Access Block and Excel
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2007/10/entlib-data-access-block-and-excel.html)*.

I need to be able to open an Excel workbook and grab the data from one of the worksheets.  I don't want to use any Office InterOperability (as that sucks) and I know I can do it using ADO.Net.  But since 1.) I hate writing all of that DataAdapter / Connection code because 2.) I am lazy I decided to see how hard it would be to use the EntLib DAB.<br /><br />Turned out it was pretty easy.<br /><br />Create your configuration as such:<br /><br />Then call your code as such:<br /><br />[csharp]<br />public static DataSet GetWorksheet()<br />{<br />string sql = "SELECT * FROM [Sheet1$]";<br />string connectionName = "Book1";<br /><br />return DatabaseFactory.CreateDatabase(connectionName)<br />.ExecuteDataSet(CommandType.Text, sql);<br />}<br />[/csharp]<br />And that is that.  One DataSet ready to go.