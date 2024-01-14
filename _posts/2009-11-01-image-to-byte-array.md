---
date: '2009-11-16T08:09:00.000-08:00'
description: ''
published: true
slug: 2009-11-image-to-byte-array
tags:
- .Net
- http://schemas.google.com/blogger/2008/kind#post
- legacy-blogger
time_to_read: 5
title: Image to Byte Array
---

*This was originally posted on blogger [here](https://techshorts.blogspot.com/2009/11/image-to-byte-array.html)*.

In <a href="http://team.sfi.vn/post/Some-ways-to-convert-a-byte-array-to-Bitmap.aspx" target="_blank" title="Some ways to convert a byte array to Bitmap">Some ways to convert a byte array to Bitmap</a> we see how to convert a Bitmap to and from a ByteArray.  As an alternative I use the following extension method to convert an image to a ByteArray:<br /><br />[csharp]<br /><br />using System.Drawing;<br />namespace DC.Core.Extension<br />{<br />	public static class ImageExtension<br />	{<br />		private static ImageConverter _converter;<br /><br />		public static byte[] ToByteArray(this Image image)<br />		{<br />			if (_converter==null) _converter = new ImageConverter();<br />			return (byte[])_converter.ConvertTo(image, typeof(byte[]));<br />		}<br />	}<br />}<br />[/csharp]