---
title: 'Period Matrix'
date: 2004-09-25T10:01:00.000-07:00
draft: false
url: /2004/09/period-matrix.html
tags: 
- SQL Origami
---

The Period Matrix table, Pd\_Matrix, is used in calculating accounting period formulas. These formulas include current month, quarter or years activity or balance. These formulas can also be created using standard SQL functions but not all functions are common between SQL Server and MS Access. The Period Matrix has the advantage in that it can be used in any DBMS and it also can be used in table pivoting and folding.

  
  

The table listed below is for use with the Activity table and not the Balance table. Either a separate matrix table will have to be created or an additional field would have to be added for calculating account formulas with the Balance table.

Pd\_Type

Pd\_ID

Pd\_Name

pd\_1

pd\_2

pd\_3

pd\_4

pd\_5

pd\_6

pd\_7

pd\_8

pd\_9

pd\_10

pd\_11

pd\_12

annual

1

YR

1

1

1

1

1

1

1

1

1

1

1

1

month

1

JAN

1

0

0

0

0

0

0

0

0

0

0

0

month

2

FEB

0

1

0

0

0

0

0

0

0

0

0

0

month

3

MAR

0

0

1

0

0

0

0

0

0

0

0

0

month

4

APR

0

0

0

1

0

0

0

0

0

0

0

0

month

5

MAY

0

0

0

0

1

0

0

0

0

0

0

0

month

6

JUN

0

0

0

0

0

1

0

0

0

0

0

0

month

7

JUL

0

0

0

0

0

0

1

0

0

0

0

0

month

8

AUG

0

0

0

0

0

0

0

1

0

0

0

0

month

9

SEP

0

0

0

0

0

0

0

0

1

0

0

0

month

10

OCT

0

0

0

0

0

0

0

0

0

1

0

0

month

11

NOV

0

0

0

0

0

0

0

0

0

0

1

0

month

12

DEC

0

0

0

0

0

0

0

0

0

0

0

1

quarter

1

QTR1

1

1

1

0

0

0

0

0

0

0

0

0

quarter

2

QTR2

0

0

0

1

1

1

0

0

0

0

0

0

quarter

3

QTR3

0

0

0

0

0

0

1

1

1

0

0

0

quarter

4

QTR4

0

0

0

0

0

0

0

0

0

1

1

1

semiannual

1

SA1

1

1

1

1

1

1

0

0

0

0

0

0

semiannual

2

SA2

0

0

0

0

0

0

1

1

1

1

1

1

### Pd\_Type

The Period Type is used to indicate the type of formula being used. The types listed are:

*   Month: The given months activity
    
*   Quarter: The given quarters activity
    
*   Semiannual: The given half-year activity
    
*   Annual: The entire years activity
    
*   Other types that could be created include a months or quarter ending balance.
    

### The Period ID and Name are used to identify a given time frame:

: The month number (1 thru 12) and name (January thru December)*   Quarter: The quarter number (1 thru 4) and name (QTR1 thru QTR4)
*   Semiannual: The semiannual number (1 or2) and name (SA1 and SA2)
*   Annual: The year number (1) or name (YR)

### pd\_1 thru pd\_12

The values for period 1 through 12 can only be 1 or 0. These fields are multiplied with the Activity table month fields to create the necessary formulas.

Creating Formulas
-----------------

To create a formula using the Period Matrix and the Activity table you would create a select statement where in the period fields in the Activity table were multiplied to the period fields in the Matrix table then add them all together:

( Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12)

In the WHERE clause of the select statement you would set the Period Type (Pd\_Type) and Period Name (Pd\_Name) of the Matrix table to the name of the formula. For example, if you wanted to show the monthly activity for January you would create the following select statement:

SELECT  
      Activity.AcctID  
     , Activity.DeptID  
     , Activity.Class  
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year  
     , ( Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ) As Amount  
  
FROM Activity, Pd\_Matrix  
  
WHERE  
         (Pd\_Type = 'month')  
     And (Pd\_Matrix.Pd\_Name = 'JAN')

This SQL statement could be changed to a parameterized stored procedure with variables for Pd\_Type and Pd\_Name. This would allow you to return a recordset for any of the given formulas.

Table Folding
-------------

The Period Matrix can also be used in table folding, where the columns of the original table are converted to rows. This is accomplished by creating a Cartesian product between the original table, in our case the Activity table, and the Period Matrix table.

A Cartesian product result set, also known as a Cross Join, is familiar to people that have created SQL statements with bad or missing joins between tables. They are recognizable because the result set will have the same row multiple tim  
es or the total row count far exceeds the tota  
l number of expected rows. In most cases this is unwanted but it comes in very handy for table folding.

The following SQL select statement will fold the Activity table's period activity columns into rows:

SELECT

       Activity.AcctID  
     , Activity.DeptID  
     , Activity.Class  
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year  
     ,    (Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ) As Amount  
  
FROM Activity, Pd\_Matrix  
   
WHERE Pd\_Type = 'month'

Note that this is identical to the SQL used to show the activity for just one month used previously, with the only exception being in the WHERE clause. Instead of indicating which month (Pd\_Name) to show, the SQL was allowed to return all the available months.

This statement works for the same reasons the previous SQL statement worked. When the Pd\_Name is JAN then pd\_1 equals one while the rest of the pd\_2 through pd\_12 equals zero. When the multiplications are carried out all the results are all zero except for January's, which is equal to the January activity. When the addition is carried out therefore only the January amount is returned.

Also, since there is no join between the two tables the result set will have twelve times the number of rows that the Activity table actually has. For each row in the Activity table there will be twelve rows generated in the result because there are twelve possible rows for the Pd\_Type of 'month'. If instead of choosing 'month' we had chosen 'quarter' for the Period Type then the results set would have four times the number of rows in the Activity table.

This method of table folding is fast and very simple to create and maintain. The most common way table folding is done though is by manually creating the final table then creating an append or update query for each column to fold. In the case of our example we would have had to create and execute thirteen queries in order to obtain the same results.

Table Folding and Pivoting Using Formulas
-----------------------------------------

Where as table folding is deals with turning columns into rows, table pivoting is turning rows into columns.

Taking the example from the table folding section lets add the requirement that our resultset show the Actual and Budget amounts in separate columns. The periods will still be shown as rows.

The SQL needed in Access would be:

SELECT  

       Activity.AcctID  
     , Activity.DeptID  
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year  
     ,Sum( IIF(Activity.Class = "Actual",  
         (Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ), 0)) As Actual  
  
     ,Sum( IIF(Activity.Class = "Budget",  
         (Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ), 0)) As Budget  
  
FROM Activity, Pd\_Matrix  
  
WHERE Pd\_Type = 'month'  
  
GROUP BY  
       Activity.AcctID  
     , Activity.DeptID  
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year

In SQL Server the CASE statement would replace the IIF( ) function:

SELECT  

       Activity.AcctID  
     , Activity.DeptID  
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year  
      
     ,Sum( CASE Activity.Class  
         WHEN "Actual"THEN  
         (Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ) ELSE 0 END) Actual  
  
     ,Sum( CASE Activity.Class  
         WHEN "Budget"THEN  
         (Activity.Jan \* Pd\_Matrix.pd\_1 + Activity.Feb \* Pd\_Matrix.pd\_2  
         + Activity.Mar \* Pd\_Matrix.pd\_3 + Activity.Apr \* Pd\_Matrix.pd\_4  
         + Activity.May \* Pd\_Matrix.pd\_5 + Activity.Jun \* Pd\_Matrix.pd\_6  
         + Activity.Jul \* Pd\_Matrix.pd\_7 + Activity.Aug \* Pd\_Matrix.pd\_8  
         + Activity.Sep \* Pd\_Matrix.pd\_9 + Activity.Oct \* Pd\_Matrix.pd\_10  
         + Activity.Nov \* Pd\_Matrix.pd\_11 + Activity.Dec \* Pd\_Matrix.pd\_12  
         ) ELSE 0 END) Budget  
  
FROM Activity, Pd\_Matrix  
  
WHERE Pd\_Type = 'month'  
   
GROUP BY  
       Activity.AcctID  
     , Activity.DeptID  
   
     , Pd\_Matrix.Pd\_Name  
     , Activity.Year  
   

Summary
-------

The Period Matrix table is a versatile tool for SQL development. It can be used in all DBMSs with little modification to the SQL statements. It can be used to replace several separate SQL statements needed to create the different formulas and it is useful in table folding and pivoting.

p>