---
date: '2008-02-04T14:14:00.000-08:00'
description: ''
published: true
slug: 2008-02-measurement-objects
tags:
- http://schemas.google.com/blogger/2008/kind#post
- General
- legacy-blogger
time_to_read: 5
title: Measurement Objects
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2008/02/measurement-objects.html)*.

In my previous post I described setting up a database to track measurements.&nbsp; I ran into problems quickly with the data model and I could see that it was going to become a convoluted mess pretty quick.&nbsp; So I want to take a step back and look at it from an application point of view.<br /><br />What I want is a way to track an objects measurements.&nbsp; I need a system that is easy to understand, any one looking at an object should readily understand what each measurement property is and what units it is in.&nbsp; The system should accommodate almost any existing system of measurement but at the same time it needs to be simple.&nbsp; Brain dead simple.<br /><br /><img align="bottom" alt="Measurement Object Diagram" border="0" hspace="0" src="http://writer.zoho.com:80/ImageDisplay.im?name=344506000000008001/1202182817737_MeasurementObject.png&amp;accId=344506000000002007" vspace="0" /><br />What I am thinking is to start out with a abstract base class for our Measurement Object.&nbsp; It has an ID that can be an int, string or Guid, take your pick.&nbsp; The Text property is the string representation of the Value, Value being in an abstract class that extends MeasurementBase.<br /><br />I think that it is important to seperate the actual Value into another class of Type T.&nbsp; This allows us to create collections of MeasurementBase objects and add MeasurementBase&lt;T&gt; objects to it.&nbsp; I am still struggling with this idea as it totally blows apart expectations on what a Value is (is it an int?&nbsp; a DateTime?), but this is the reason I stuck the Text property on the MeasrumentBase.&nbsp; The Text property takes care of the conversion of the string representation to the actual Value.<br /><br />Already this is getting complicated.&nbsp; What is it I'm trying to do here?<br /><br />My ultimate goal is to have the means to convert a measurment from one system to another.&nbsp; The objects themselves should take care of the conversion.&nbsp; The way I have seen it in the past is to have conversion code scattered throughout the entire application layer, including the UI and the data access layer.<br /><br />This is one of those ideas that is on the tip of my neurons, I know it has been solved before but I haven't found it.&nbsp; And every time I start working on it I naturally want to drop into the Database thinking frame of mind.<br /><br />I need to review some of the Enterprise Patterns, see if it already exits.<br />