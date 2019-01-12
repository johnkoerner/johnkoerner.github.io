---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - On Site Challenge
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

Clue
---
Games are played all night.
This one online, but there, board.
Code is history

Hint
---
There is a code hidden somewhere in the Kalahari.


Approach
---
This clue pointed us to the game room in the Kalahari.  There was a QR code on the walls that takes you to Bill Sempf's [User Talk page](https://www.owasp.org/index.php/User_talk:Bill_Sempf) on the OWASP website. One thing that stood out was that the page was recently modified. Looking at the history, there is a string that was removed:

`Y20xOS1rNGxhLWhhOWktYzAwbC1wbzBM`

The string stood out as a base64 encoded string. Decoding that string yields our flag:
```
cm19-k4la-ha9i-c00l-po0L
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)