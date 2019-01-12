---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - The Parrot
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
Can you find the hidden parrot?

[parrot.pdf](/content/parrot.pdf)

Hint
---
Opening the file with a tool other than a PDF viewer, could be helpful.


Approach
---
This is a password protected PDF, so we need to crack that first. I downloaded `pdfcrack` on my kali VM and ran the following command (using one of the wordlists on the machine):

```
pdfcrack ./parrot.pdf -w /usr/share/wordlists/sqlmap.txt
```

This yields us the password `cracker`.  From there you open the PDF and just see a parrot, so maybe something is hidden behind it. I found an [online image extractor](https://www.pdf-online.com/osa/extract.aspx?o=img) that supports passwords, which yielded me the flag:

![flag](/content/cracker.png)



[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)