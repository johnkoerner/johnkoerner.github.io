---
layout: post
status: publish
published: true
title: Codemash CTF - 14 - Security Regulations
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
14 - Security Regulations
Due to some new privacy regulations this flag had to be shred. The classification will be secret or topsecret depending on the content.

____-____-____-____-____
```

[Left over shred inside the paper shredder](https://codemash.hacking-lab.com/codemash/secret_challenge_shred1.html)


Approach
---
Following the link gives you shred text:

```
Shred 1: 
Note: the other shreds are classified as «topsecret»!

cm18
```

Since the URL has a number in it, maybe we could change the 1 to a 2.  Doing that results in shred text of:

```
Shred 2: 
Note: the contents on this shred were sanitized!

XXXX-XXXX
```

The URL also contains the word `secret` and there was mention in the clue of `secret` and `topsecret`, so if we change the URL to topsecret_challenge_shred2.html, we get the following text:

```
Shred 2

bWh0-VIkC
```

Uupdate the URL for #3 and we get the text:

```
Shred 3

cMf4-72jY
```

Combine them together for the flag of 

```
cm18-bWh0-VIkC-cMf4-72jY
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)