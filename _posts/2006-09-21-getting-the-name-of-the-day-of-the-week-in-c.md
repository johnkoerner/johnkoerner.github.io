---
layout: post
status: publish
published: true
title: Getting the name of the day of the week in C#
author: John Koerner
author_email: blog@johnkoerner.net
wordpress_id: 181
wordpress_url: http://johnkoerner.com/?p=181
date: '2006-09-21 23:43:49 -0400'
date_gmt: '2006-09-21 23:43:49 -0400'
categories:
- csharp
tags: []
---
Getting the current day of week in C# is pretty easy if all you need is the English version of the day, for example:

{%highlight csharp %}
MessageBox.Show(System.DateTime.Now.DayOfWeek.ToString());
{% endhighlight %}

But if you want to get the Day of Week for the current language the computer is setup for, the above code will not work. You need to access the `DayNames` property on the `DateTimeFormatInfo` class and get the day of week from there. The snippet of code below, demonstrates how to do it:

{%highlight csharp %}
MessageBox.Show(System.Globalization.CultureInfo.CurrentCulture.DateTimeFormat.DayNames[(int) System.DateTime.Now.DayOfWeek]);
{% endhighlight %}
