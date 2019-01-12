---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Mrs. Robot
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
Mrs. Robot has hidden a flag for you.

Connect to: http://whale.hacking-lab.com:4280

Hint
---
How can you tell search engines, not to scan your files?


Approach
---
The page that you hit gives you a textbox where you can enter text. Javascript then appears to MD5 the text and take you the `{MD5}.html` page.   The hint gives us a big clue that we should look at the `robots.txt` file on that server.  The contents of that file were:

```
User-agent: *
Disallow: /481065fd79b253104aeab5ca5c717cd5.html
```

Browsing to that page gives us the clue:
```
fatatu = pataje
```

Since I did last years CTF, I remember ROILA (but a google search also returns it as the first hit), so I look those words up and it yields `word = winter`.  Typing winter into the textbox takes us to `f6432274349b5cb93433f8ed886a3f37.html` which contains our flag:
```
cm19-bOTs-haVe-brai-nZ33
```
[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)