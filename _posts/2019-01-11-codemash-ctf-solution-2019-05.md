---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Busted File
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
Mommy told you not to store your important files on those old diskettes. Can you repair the file?

[busted.zip](/content/busted.zip)

Hint
---
Have you heard of magic numbers?


Approach
---
Any time I get a file from a CTF, the first thing I do is open it in a hex editor.  When opening this file I see that the first four bytes are [`DE AD BE EF`](https://en.wikipedia.org/wiki/Magic_number_(programming)#Magic_debug_values), which is a classic magic number.  Since I have worked with zip files in the past, I knew they started with `PK` and then a version number. A quick google search got me the [right values](https://en.wikipedia.org/wiki/Zip_(file_format)).  So I replaced the `DE AD BE EF` bytes with `50 4B 03 04` and was able to open the file.

This got us a smiling horse:

![horseWithFlag](/content/busted-contents.jpg)

I opened this file with a hex editor and a search for the string `cm`, yields our flag:

```
cm19-disk-3tte-N0st-algy
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)