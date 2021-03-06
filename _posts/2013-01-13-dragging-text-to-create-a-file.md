---
layout: post
status: publish
published: true
title: Dragging text to create a file
author: John Koerner
author_email: blog@johnkoerner.net
wordpress_id: 271
wordpress_url: http://johnkoerner.com/?p=271
date: '2013-01-13 01:45:51 -0500'
date_gmt: '2013-01-13 01:45:51 -0500'
permalink: "csharp/dragging-text-to-create-a-file/"
categories:
- csharp
tags:
- csharp
- DragDrop
---
There was a recent [question](http://stackoverflow.com/q/14293908/573218) on StackOverflow asking how to drag content from a rich text box and drop it into windows explorer to create a file. I did some digging and found that this was surprisingly easy to do. The thing to understand is that Explorer drag and drop expects the file to exist. So the solution I came up with was when the mouse leaves the RTB, if the left button is down, we save a temporary file and then setup the drag and drop.

{%highlight csharp %}
private void richTextBox1_MouseLeave(object sender, EventArgs e)
{
    // If the left mouse button is down when leaving the rtb
    if (MouseButtons == MouseButtons.Left)
    {
        // Write everything to a temp file.
        System.IO.File.WriteAllText(@"z:\Temp\helloWorld.rtf", richTextBox1.SelectedRtf);
        string[] filenames = { @"z:\Temp\helloWorld.rtf" };
        DataObject obj = new DataObject();
        // Set the drag drop data with the FileDrop format
        obj.SetData(DataFormats.FileDrop, filenames);
        // Start the drag drop effect
        DoDragDrop(obj, DragDropEffects.All);
    }
}
{% endhighlight %}
