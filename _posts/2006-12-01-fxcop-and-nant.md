---
date: '2006-12-06T08:41:00.000-08:00'
description: ''
published: true
slug: 2006-12-fxcop-and-nant
tags:
- http://schemas.google.com/blogger/2008/kind#post
- General
- legacy-blogger
time_to_read: 5
title: FxCop and NAnt
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2006/12/fxcop-and-nant.html)*.

<p>I am working on automating our build process and one of the things I am trying to do now is to add FxCop to the mix.&nbsp; There are a couple of ways to run the process, one using an exec task to call the executable directly, the other is through a Contrib task &lt;fxcop&gt;.</p> <p>I tried the first method with no success.&nbsp; For some reason I couldn't get the output file name to be recognized by the executable.&nbsp; I eventually had to switch to the &lt;fxcop&gt; task but I had to set a system envitonment variable to the executable first.&nbsp; It eventually looked like this:</p> <p>&nbsp;</p> <pre>&lt;target name="analyze.fxcop" description="Runs FxCop on build output"&gt;<br /><br />   &lt;setenv name="PATH" value="${tools.dir}\fxcop;%PATH%" /&gt;<br /><br />   &lt;mkdir dir="${build.dir}\\fxcop" /&gt;<br /><br />   &lt;fxcop directOutputToConsole="false" analysisReportFilename="${build.dir}\\fxcop\\fxcop.xml" failonerror="false"&gt;<br />      &lt;targets&gt;<br />         &lt;include name="${build.dir}\\release\\bin\\*.dll" /&gt;<br />      &lt;/targets&gt;<br />      &lt;dependencyDirectories refid="referenceComponents" /&gt;<br />   &lt;/fxcop&gt;<br /><br />&lt;/target&gt;</pre><br /><p>A lot of work was involved just to find this out.&nbsp; Oh well, I got it working so now I share my results.</p>