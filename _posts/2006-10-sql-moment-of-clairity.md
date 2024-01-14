---
date: '2006-10-17T12:16:00.000-07:00'
description: ''
published: true
slug: 2006-10-sql-moment-of-clairity
tags:
- http://schemas.google.com/blogger/2008/kind#post
- SQL Origami
- legacy-blogger
time_to_read: 5
title: SQL Moment of Clairity
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/10/sql-moment-of-clairity.html)*.

I was working on a stored procedure the other day, not one that I wrote originally but one that was causing performance issues in out system.  The procedure was taking any where from 40 to 60 seconds to run, which is unacceptable in a web service.  This in fact was causing the web service to time out.<br /><br />An inspection of the execution plan showed that one part of the procedure was doing an index scan and that it was this that was taking up over 85% of the execution time.  I was totally baffled, it was hitting the index so why wasn’t it faster?<br /><br />Then I learned three things all at once:<br /><ul><br />	<li>Implicit Conversion</li><br />	<li>non-sargable kills performance</li><br />	<li>Index Seek is preferred of Index Scan</li><br /></ul><br /><strong>Implicit Conversion</strong><br /><br />In the stored proc a variable was defined as an NVARCHAR(20) but the field in the table it was being compared to was a CHAR(10).  This lead to an implicit conversion of the variable to a CHAR(10), which lead into the next issue:<br /><br /><strong>Non-Sargable Kills Performance</strong><br /><br />Sargable refers to the pseudo-acronym “SARG� – Search ARGument and refers to a WHERE clause that compares a constant value  to a column value.  The implicit conversion was causing a non-SARGable condition which means the WHERE clause cannot use an index.<br /><br /><strong>Index Scan</strong><br /><br />Because of the non-sargable condition an Index Scan was being performed.  An Index Scan is just as bad as a Table Scan in the SQL realm and should be avoided at all costs.<br /><br />The solution was simple:  Change the variable to a CHAR(10).  After doing that the Index Scan became an Index Seek and the whole stored procedure returned in less than a second.  Any time I see an order of magnitude improvement like that from one simple change it just boggles my mind.