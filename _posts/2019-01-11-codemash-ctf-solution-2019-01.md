---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - ASCII Art
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
I love ASCII art. What about you?
```
 ##99##  #109##  ##49### ####57#      ####  ####  #####  ####### ##   ##
#45  ## ###  97# ##  115 99#          ########## ### ### ###  ## ##   ##
105     45    ## 67   ## ###79##      ##  ##  ## ####### #####   #######
68      ##    69 ##   45 #97####      ##  ##  ## #######   ##### #######
###  49 110  ### ##  116 45#          ##  ##  ## ##   ## ##   ## ##   ##
 #72###  ##52##  #82#### ####68#      ##  ##  ## ##   ## ####### ##   ##
```
Hint
---
This one's easy, really. Look at the numbers, what could they represent?


Approach
---
Since we know the format of the flags follow the pattern cm19-XXXX-XXXX-XXXX-XXXX, we will use that to our advantage.  Looking at the numbers I see that it starts with `99` and `109` which are the ASCII code for `c` and `m` respectively. I used a text editor to get rid of the `#` symbols and then pasted the text into an [online converter](https://www.browserling.com/tools/ascii-to-text) to generate the string 

```
cm19-asci-CODE-a1nt-H4RD
```
[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)