---
layout: post
status: publish
published: true
title: Codemash CTF - 1 - Do you like my Style?
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_email: blog@johnkoerner.net
categories:
- codemash
tags:
- codemash
- fun
---
Hint
---
    01 - Do you like my Style?
    Every one is talking about styles. Sometimes its about what you wear and sometimes its about what you do.

    All I know is that the flag you want definitely has Style.

It also included the following image:

<img src="/content/challenge_01_7093.jpg" width="250">

Approach
---
This CTF is a very obvious hint that wants us to look in the stylesheet for the site to find the flag.  I opened up the developer tools in my web browser and browsed through the style.css file. At the bottom, I found the flag.

![solution-image](/content/ctf-solution1.png) 

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)