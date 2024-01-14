---
date: '2004-09-25T10:01:00.000-07:00'
description: ''
published: true
slug: 2004-09-period-matrix
tags:
- http://schemas.google.com/blogger/2008/kind#post
- SQL Origami
- legacy-blogger
time_to_read: 5
title: Period Matrix
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2004/09/period-matrix.html)*.

<p>The Period Matrix table, Pd_Matrix, is used in calculating accounting period formulas. These formulas include current month, quarter or years activity or balance. These formulas can also be created using standard SQL functions but not all functions are common between SQL Server and MS Access. The Period Matrix has the advantage in that it can be used in any DBMS and it also can be used in table pivoting and folding. </p><br /><a name="more"></a><br /><p>The table listed below is for use with the Activity table and not the Balance table. Either a separate matrix table will have to be created or an additional field would have to be added for calculating account formulas with the Balance table.</p><table border="1" cellpadding="1" cellspacing="1" style="BACKGROUND: #fff;"><thead><tr style="BORDER-RIGHT: black solid; BORDER-TOP: black solid; BACKGROUND: silver; BORDER-LEFT: black solid; BORDER-BOTTOM: black solid;"><td>Pd_Type</td><td>Pd_ID</td><td>Pd_Name</td><td>pd_1</td><td>pd_2</td><td>pd_3</td><td>pd_4</td><td>pd_5</td><td>pd_6</td><td>pd_7</td><td>pd_8</td><td>pd_9</td><td>pd_10</td><td>pd_11</td><td>pd_12</td></tr></thead><tbody><tr valign="top"><td>annual </td><td>1 </td><td>YR </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td></tr><tr valign="top"><td>month </td><td>1 </td><td>JAN </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>2 </td><td>FEB </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>3 </td><td>MAR </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>4 </td><td>APR </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>5 </td><td>MAY </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>6 </td><td>JUN </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>7 </td><td>JUL </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>8 </td><td>AUG </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>9 </td><td>SEP </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>10 </td><td>OCT </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>11 </td><td>NOV </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>0 </td></tr><tr valign="top"><td>month </td><td>12 </td><td>DEC </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td></tr><tr valign="top"><td>quarter </td><td>1 </td><td>QTR1 </td><td>1 </td><td>1 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>quarter </td><td>2 </td><td>QTR2 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>1 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>quarter </td><td>3 </td><td>QTR3 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>1 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>quarter </td><td>4 </td><td>QTR4 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>1 </td><td>1 </td></tr><tr valign="top"><td>semiannual </td><td>1 </td><td>SA1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td></tr><tr valign="top"><td>semiannual </td><td>2 </td><td>SA2 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>0 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td><td>1 </td></tr></tbody></table><h3>Pd_Type</h3><p>The Period Type is used to indicate the type of formula being used. The types listed are:</p><ul><li><p>Month: The given months activity</p><li><p>Quarter: The given quarters activity</p><li><p>Semiannual: The given half-year activity</p><li><p>Annual: The entire years activity</p><li><p>Other types that could be created include a months or quarter ending balance.</p></li></li></li></li></li></ul><h3>The Period ID and Name are used to identify a given time frame:</h3><ul>:&nbsp;The month number (1 thru 12) and name (January thru December)<li>Quarter:&nbsp;The quarter number (1 thru 4) and name (QTR1 thru QTR4)</li><li>Semiannual:&nbsp;The semiannual number (1 or2) and name (SA1 and SA2)</li><li>Annual:&nbsp;The year number (1) or name (YR)</li></ul><h3>pd_1 thru pd_12</h3><p>The values for period 1 through 12 can only be 1 or 0. These fields are multiplied with the Activity table month fields to create the necessary formulas.</p><h2>Creating Formulas</h2><p>To create a formula using the Period Matrix and the Activity table you would create a select statement where in the period fields in the Activity table were multiplied to the period fields in the Matrix table then add them all together:</p><p>( Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12)</p><p>In the WHERE clause of the select statement you would set the Period Type (Pd_Type) and Period Name (Pd_Name) of the Matrix table to the name of the formula. For example, if you wanted to show the monthly activity for January you would create the following select statement:</p><p>SELECT<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Class<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year<br />&nbsp;&nbsp;&nbsp;&nbsp; , ( Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ) As Amount<br /><br />FROM Activity, Pd_Matrix<br /><br />WHERE<br />&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; (Pd_Type = 'month')<br />&nbsp;&nbsp;&nbsp;&nbsp; And (Pd_Matrix.Pd_Name = 'JAN')</p><p>This SQL statement could be changed to a parameterized stored procedure with variables for Pd_Type and Pd_Name. This would allow you to return a recordset for any of the given formulas.</p><h2>Table Folding</h2><p>The Period Matrix can also be used in table folding, where the columns of the original table are converted to rows. This is accomplished by creating a Cartesian product between the original table, in our case the Activity table, and the Period Matrix table.</p><p>A Cartesian product result set, also known as a Cross Join, is familiar to people that have created SQL statements with bad or missing joins between tables. They are recognizable because the result set will have the same row multiple tim<br />es or the total row count far exceeds the tota<br />l number of expected rows. In most cases this is unwanted but it comes in very handy for table folding.</p><p>The following SQL select statement will fold the Activity table's period activity columns into rows:</p><p>SELECT</p><p>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Class<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year<br />&nbsp;&nbsp;&nbsp;&nbsp; ,&nbsp;&nbsp;&nbsp; (Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ) As Amount<br /><br />FROM Activity, Pd_Matrix<br />&nbsp;<br />WHERE Pd_Type = 'month'</p><p>Note that this is identical to the SQL used to show the activity for just one month used previously, with the only exception being in the WHERE clause. Instead of indicating which month (Pd_Name) to show, the SQL was allowed to return all the available months.</p><p>This statement works for the same reasons the previous SQL statement worked. When the Pd_Name is JAN then pd_1 equals one while the rest of the pd_2 through pd_12 equals zero. When the multiplications are carried out all the results are all zero except for January's, which is equal to the January activity. When the addition is carried out therefore only the January amount is returned.</p><p>Also, since there is no join between the two tables the result set will have twelve times the number of rows that the Activity table actually has. For each row in the Activity table there will be twelve rows generated in the result because there are twelve possible rows for the Pd_Type of 'month'. If instead of choosing 'month' we had chosen 'quarter' for the Period Type then the results set would have four times the number of rows in the Activity table.</p><p>This method of table folding is fast and very simple to create and maintain. The most common way table folding is done though is by manually creating the final table then creating an append or update query for each column to fold. In the case of our example we would have had to create and execute thirteen queries in order to obtain the same results.</p><h2>Table Folding and Pivoting Using Formulas</h2><p>Where as table folding is deals with turning columns into rows, table pivoting is turning rows into columns.</p><p>Taking the example from the table folding section lets add the requirement that our resultset show the Actual and Budget amounts in separate columns. The periods will still be shown as rows.</p><p>The SQL needed in Access would be:</p><p>SELECT<br /><p>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year<br />&nbsp;&nbsp;&nbsp;&nbsp; ,Sum( IIF(Activity.Class = "Actual",<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ), 0)) As Actual<br /><br />&nbsp;&nbsp;&nbsp;&nbsp; ,Sum( IIF(Activity.Class = "Budget",<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ), 0)) As Budget<br /><br />FROM Activity, Pd_Matrix<br /><br />WHERE Pd_Type = 'month'<br /><br />GROUP BY<br />&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year</p><p>In SQL Server the CASE statement would replace the IIF( ) function:</p><p>SELECT<br /><p>&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year<br />&nbsp;&nbsp;&nbsp;&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp; ,Sum( CASE Activity.Class<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; WHEN "Actual"THEN<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ) ELSE 0 END) Actual<br /><br />&nbsp;&nbsp;&nbsp;&nbsp; ,Sum( CASE Activity.Class<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; WHEN "Budget"THEN<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; (Activity.Jan * Pd_Matrix.pd_1 + Activity.Feb * Pd_Matrix.pd_2<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Mar * Pd_Matrix.pd_3 + Activity.Apr * Pd_Matrix.pd_4<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.May * Pd_Matrix.pd_5 + Activity.Jun * Pd_Matrix.pd_6<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Jul * Pd_Matrix.pd_7 + Activity.Aug * Pd_Matrix.pd_8<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Sep * Pd_Matrix.pd_9 + Activity.Oct * Pd_Matrix.pd_10<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; + Activity.Nov * Pd_Matrix.pd_11 + Activity.Dec * Pd_Matrix.pd_12<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ) ELSE 0 END) Budget<br /><br />FROM Activity, Pd_Matrix<br /><br />WHERE Pd_Type = 'month'<br />&nbsp;<br />GROUP BY<br />&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; Activity.AcctID<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.DeptID<br />&nbsp;<br />&nbsp;&nbsp;&nbsp;&nbsp; , Pd_Matrix.Pd_Name<br />&nbsp;&nbsp;&nbsp;&nbsp; , Activity.Year<br />&nbsp;<br /><h2>Summary</h2><p>The Period Matrix table is a versatile tool for SQL development. It can be used in all DBMSs with little modification to the SQL statements. It can be used to replace several separate SQL statements needed to create the different formulas and it is useful in table folding and pivoting.</p><br />p></p></p>