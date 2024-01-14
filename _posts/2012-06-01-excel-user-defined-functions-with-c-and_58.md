---
date: '2012-06-13T05:35:00.002-07:00'
description: ''
published: true
slug: 2012-06-excel-user-defined-functions-with-c-and_58
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- MS Excel
- legacy-blogger
time_to_read: 5
title: Excel User Defined Functions with C# and ExcelDna
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2012/06/excel-user-defined-functions-with-c-and_58.html)*.

Adding user defined functions to Excel can be laborious, either you use VBA or COM. Why can't Microsoft make it easier to use Visual Studio and .NET within Excel?<br /><br />Enter <a href="http://exceldna.codeplex.com/" target="_blank" title="ExcelDna on CodePlex">ExcelDna</a>.<br /><br /><a name="more"></a><br /><br />This example creates a static function in C# using Visual Studio. There is documentation that already describes this, what I am adding is:<br /> <ul><br /> <li>Use Visual Studio to create project<br /> <li>Post Build Events to help create the final XLL file.<br /></li></ul><br /><br /><strong>NOTE:</strong> <em>I hate Post Build Events.</em> The ONLY exception is in this case where I am modifying the output of the final build. Post Build Events are Evil especially when used in a large development team. A better solutions is to create actual Build Scripts that do what I am about to do. You have been warned.<br /><br />First, create a new Class Library project. Use NuGet to add a reference to the Excel-DNA package. NuGet will also add ExcelDna.dna and ExcelDna.xll to your project. Rename them both to the name that you want your final output xll to be. In my case I renamed them to Scratch-ExcelDna.dna and Scratch-ExcelDna.xll. Also for both files change to properties for <strong>Build Action</strong> to "Content" and <strong>Copy to Output Directory</strong> to "Copy Always".<br /><br />Within the packages folder created by NuGet is the ExcelDnaPack utility, in the tools folder. This will package your project into one xll file. For it to work you need to update the .dna file:<br /><br /><pre class="brush:xml" name="code">&lt;DnaLibrary RuntimeVersion="v4.0"&gt;
     &lt;ExternalLibrary Path="DC.Scratch.ExcelDna.dll" Pack="true" /&gt;
&lt;/DnaLibrary&gt;
</pre><br /><br />Note that I am using .Net 4.<br /><br />To get the pack utility to work, add a Pre-build event to delete the existing xll:<br /><br />del "$(TargetDir)Scratch-ExcelDna-packed.xll"<br /><br />Then add a Post-build event to recreate it:<br /><br />"$(SolutionDir)packages\Excel-DNA.0.29\tools\ExcelDnaPack.exe" "$(TargetDir)Scratch-ExcelDna.dna"<br /><br />While you are in the Project Properties messing with the evil build events set the Debug options so you can test your code. Set the External Program to you MS Excel and add a Command Line argument with a path to your final xll file.<br /><br />Now, add a class TestFunctions:<br />[csharp]<br />using ExcelDna.Integration;<br /><br />namespace DC.Scratch.ExcelDna<br />{<br />public class TestFunctions<br />{<br />[ExcelFunction(Description = "Product of two numbers", Category = "DNA Test")]<br />public static double TheProductOf(double x, double y)<br />{<br />return x*y;<br />}<br />}<br />}<br />[/csharp]<br /><br />Hit F5 and see if Excel Starts. If it does, add some numbers to the Excel spreadsheet and see if the TheProduct() function works.<br /><br />Download sample project here: <a href="https://dl.dropboxusercontent.com/u/480457/techshorts/2012/06/DC.Scratch.ExcelDna.zip">DC.Scratch.ExcelDna</a><br /><br />Microsoft should really look at buying Excel-DNA and incorporating it into Visual Studio. You Guys Listening!?!