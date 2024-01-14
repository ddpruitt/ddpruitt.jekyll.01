---
date: '2009-04-02T11:55:00.000-07:00'
description: ''
published: true
slug: 2009-04-json-for-jqgrid-from-aspnet-mvc
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- asp.net-mvc
- Web Standard
- legacy-blogger
time_to_read: 5
title: Json for jqGrid from ASP.Net MVC
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2009/04/json-for-jqgrid-from-aspnet-mvc.html)*.

<a href="http://www.trirand.com/blog/" target="_blank" title="jqGrid">jqGrid</a> takes a specific format for its json (taken from jqGrid documentation):<br /><br />[js]{<br /> total: &quot;xxx&quot;,page: &quot;yyy&quot;, records: &quot;zzz&quot;,<br /> rows : [<br />   {id:&quot;1&quot;, cell:[&quot;cell11&quot;, &quot;cell12&quot;, &quot;cell13&quot;]},<br />   {id:&quot;2&quot;, cell:[&quot;cell21&quot;, &quot;cell22&quot;, &quot;cell23&quot;]},<br />    ...<br /> ]}[/js]<br /><br />The tags mean the following:<br /><br /><span style="font-weight: bold;">total </span>- Total number of Pages.<br /><span style="font-weight: bold;">page </span>- Current page Index.<br /><span style="font-weight: bold;">records </span>- Total number of records in the rows group.<br /><span style="font-weight: bold;">rows </span>- An array with the data plus an identifier.<br /><span style="font-weight: bold;">id </span>- The unique row identifier, needs to be an int from what I have found.<br /><span style="font-weight: bold;">cell </span>- An array of the data for the grid.<br /><br />The ASP.Net MVC framework has the JsonResult response type which we can use to populate the jqGrid.  As an example I created a Person model and a method to return some data:<br /><br />[csharp]<br />public class Person<br />{<br />    public int ID { get; set; }<br />    public string Name { get; set; }<br />    public DateTime Birthday { get; set; }<br />}<br /><br />public IEnumerable&lt;Person&gt; GetABunchOfPeople()<br />{<br />    yield return new Person {ID = 1, Name = &quot;Darren&quot;, Birthday = new DateTime(1970, 9, 13)};<br />    yield return new Person {ID = 2, Name = &quot;Dawn&quot;, Birthday = new DateTime(1971, 6, 1)};<br />    yield return new Person {ID = 3, Name = &quot;Thomas&quot;, Birthday = new DateTime(1995, 10, 3)};<br />    yield return new Person {ID = 4, Name = &quot;Zoey&quot;, Birthday = new DateTime(1997, 8, 15)};<br />}<br />[/csharp]<br /><br />Generating the JSON is as follows, this going into a PersonModel class:<br /><br />[csharp]<br />public JsonResult GetABunchOfPeopleAsJson()<br />{<br />    var rows = (GetABunchOfPeople()<br />        .Select(c =&gt; new<br />                         {<br />                             id = c.ID,<br />                             cell = new[]<br />                                        {<br />                                            c.ID.ToString(),<br />                                            c.Name,<br />                                            c.Birthday.ToShortDateString()<br />                                        }<br />                         })).ToArray();<br />    return new JsonResult<br />               {<br />                   Data = new<br />                              {<br />                                  page = 1,<br />                                  records = rows.Length,<br />                                  rows,<br />                                  total = 1<br />                              }<br />               };<br />}[/csharp]<br /><br /><br />The controller then would look like:<br />[csharp]<br />public class PersonController : Controller<br />{<br />    public ActionResult Index()<br />    {<br />        return View();<br />    }<br />    public JsonResult GetAllPeople()<br />    {<br />        var model = new Models.PersonModel();<br />        return model.GetABunchOfPeopleAsJson();<br />    }<br />}<br /><br />[/csharp]<br />The view doesn't need to inherit any model other than View page if all you want is for the jqGrid to show the data.  In the view, Index.aspx in this case, you add table and div for the jqGrid:<br /><br />&lt;table id="dictionary" class="scroll" cellpadding="0" cellspacing="0"&gt;&lt;/table&gt;<br />&lt;div id="pager" class="scroll" style="text-align: center;"&gt;&lt;/div&gt;<br /><br />Configuring jqGrid is:<br />[js highlight="6,8"]<br />$(document).ready(function() {<br /><br />$(&quot;#dictionary&quot;).jqGrid({<br />caption: &quot;Tank Dictionary&quot;,<br />pager: $(&quot;#pager&quot;),<br />url: '&lt;%= ResolveUrl(&quot;~/Person/GetAllPeople&quot;) %&gt;',<br />editurl: '&amp;lt;%= ResolveUrl(&quot;~/Person/Edit&quot;) %&amp;gt;',<br />datatype: 'json',<br />myType: 'GET',<br />colNames: ['ID', 'Name', 'Birthday'],<br />colModel: [<br />{ name: 'ID', index: 'ID', width: 150, resizable: true, editable: false },<br />{ name: 'Name', index: 'Name', width: 200, resizable: true, editable: true },<br />{ name: 'Birthday', index: 'Birthday', width: 300, resizable: true, editable: true }<br />],<br />sortname: 'ID',<br />sortorder: 'desc',<br />viewrecords: true,<br />height: '100%',<br />imgpath: '&lt;%= ResolveUrl(&quot;~/Scripts/jquery/jqGrid/themes/basic/images&quot;) &gt;'<br />});<br />[/js]<br />The url tag is set to call the Person controller to get the JSON results.  Note the datatype is json.<br /><br />The editurl tag will be talked about later.