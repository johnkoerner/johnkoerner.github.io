---
layout: post
status: publish
published: true
title: Minified Javascript not Deploying With .Net Core Projects Created in Visual Studio 2017
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_email: blog@johnkoerner.net
categories:
- csharp
tags:
- csharp
- Jenkins
- Visual Studio 2017
---
I was working on a very [simple site](https://cartpadding.com) that I created using the new .Net Core project templates in Visual Studio 2017.  Everything worked great on my machine, but, when I deployed to Azure, none of my custom javascript or CSS were working properly.  What gives?

After doing some digging, I found that the deployed site was trying to use the `site.min.js` and the `site.min.css`, but those files weren't deployed to Azure.  After googling a bit, I found that it was probably an issue with my bundling and when I opened the `bundleconfig.json`, Visual Studio tried to be helpful:

![Extensions are available...](/content/extensionsavailable.png)

Of course, I ignored the extension warning and comment at first, but the extension that is missing solves the exact problem I was having.  The [link](https://go.microsoft.com/fwlink/?LinkId=808241) in the comments has an article on how to enable and configure bundling in ASP.NET Core.

So, while the Visual Studio team could work on making this a better experience, I have to remember to read the warnings and comments that are left in the generated code.  They are there for a reason.

