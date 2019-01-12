---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Capture the Falg
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
This falg is easy to catch, isn't it?

```
criSdmetio1AUdW9dP3n----
```

Hint
---
```
fa
lg
```

Approach
---
Based on the characters in the text, this appears to be some sort of transposition cipher.  I loaded up my favorite [cipher tool site](http://www.dcode.fr) and eventually landed on the [caesar-box-cipher](https://www.dcode.fr/caesar-box-cipher).  Running it through will all possible sizes yields one of the strings being our flag:

```
cm19-reAd-itUP-Sid3-doWn
```


[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)