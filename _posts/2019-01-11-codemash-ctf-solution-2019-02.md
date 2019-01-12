---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Esoteric Stuff
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
It's getting a bit esoteric now. **Ookay**?!

```
....................!?.?...?....
...?...............?............
........?.?.?.?.!!?!.?.?.?.?!!!.
....................!.?.?.......
................................
!.................!.!!!!!!!!!!!!
!!!!!!!!!!!!!..?.?!!!!!!!!!!!!!!
!!!.............................
!.?.?.......!..?.?!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!!!!!.?.?.!!!!!!!.
.?.?........................!.!!
!!!!!!!!!!!!!!!!!!!!!...!.?.....
..!.?.!..?.?....................
........!.!!!!!!!!!!!!!!!!!!!!!!
!!!!!...........................
....!.?...........!.?.!..?.?!!!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!.?.?.......!..?.?..!...!.?.?.!!
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!.
```

Hint
---
Have you heard of esoteric programming languages?
Look at the challenge description closely, too.


Approach
---
The title indicates that this probably related to a programing language and the `Ookay` in the clue helps us find out that this is related to the `Ook` programming language.  A quick search finds us an [online interpreter](https://www.dcode.fr/ook-language) for Ook. Pasting our text into that yields our flag. 

```
cm19-es0c-odeI-sfuN-c0de 
```


[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)