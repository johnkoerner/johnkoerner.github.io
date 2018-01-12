---
layout: post
status: publish
published: true
title: Codemash CTF - 10 - Chest
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
10 - Chest
Can you find the flag inside of the chest?


```
[chest](/content/chest)
Approach
---

Looking at the chest, it appears to be an ELF executable.  However, opening the executalbe in a text editoring, I was able to get the entire string table and just copy and paste that out.  I replaced the spaces with newlines and opened in excel.  Sorting the file made it really easy to search.

Looking at the flags, there are plenty of red herrings in there, but they are pretty obvious.  They have pirate themed text in them:

```
cm18-mQmX-bUoC-rust-ykey // rusty key
cm18-lYmV-bUoC-vXpa-rrot // parrot
cm18-bFaL-bUgo-lden-coin // golden coin
cm18-cHbG-bUfa-ncyb-oots // fancy boots
cm18-dIiI-bUsi-lver-coin // silver coin
cm18-eOdP-bUoC-orna-ment // ornament
cm18-fLkP-bUoC-vXXb-ones // bones
cm18-gMhS-bUoC-seas-hell // sea shell
cm18-hPnR-bUoC-vXje-wels // jewels
cm18-iPnV-fanc-yban-dana // fancy bandana
cm18-jWqS-bUon-ylon-flag // nylon flag
cm18-kOlV-bbot-tleo-frum // bottle of rum
cm18-Ml2l-bUoC-vXXE-Fc8c //??? This is our flag
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)