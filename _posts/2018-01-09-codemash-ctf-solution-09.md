---
layout: post
status: publish
published: true
title: Codemash CTF - 9 - Meow
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
```
09 - Meow!
Can you lure the cat out of the hiding place?


```
[meow.pdf](/content/meow.pdf)
Approach
---
Opening the PDF in a hex editor and searching for the string `image` you see that there appears to be multiple images in the PDF.

There are plenty of online tools to extract the images from the PDF: http://www.pdfaid.com/ExtractImages.aspx

One of the images from the PDF is our flag.

![](/content/meowflag.png)


[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)