---
layout: post
status: publish
published: true
title: Codemash CTF - 13 - Alice
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
13 - Alice
Follow the white rabbit.
```
With a hint image of:

![white rabbit](/content/challenge_13_2433.jpg)

Approach
---
Looking at the image, it is really big for a jpg. Also looking at the file in a text editor, you see mentions of other files:

![](/content/challenge13editview.png)

Looking more deeply at the file, there appears to be a zip file after all of the bytes in the JPG.  I extracted the bytes for the zip file using [BE.HexEditor](http://hexbox.sourceforge.net/) and copied them to a new file.

After extracting the zip you are given three files.

![](/content/forest.jpg)

![](/content/meadow.jpg)

![](/content/water.jpg)

Opening each of those files in a text editor finds that there is exif data giving you hints:

In forest:
```
This image has a protected secret.
```

In meadow:
```
This meadow is all dried out. Check the water first.
```

In water:
```
steghide was here. With an empty passwor
```

I used an [online steghide tool](https://futureboy.us/stegano/decinput.html) to extract the data.

Water yields the result:
```
You search the whole place but you can't find anything.


...


Now get out before you get flushed down.
```

Not much helpful in there, but Meadow yields the result:
```
So you think a mole can speak?!


...


Lucky you, this one can!

He's name is Fred and he tells you the passphrase:

The-Mad-Hatter
```

Forest appears to be password protected, so we take the password from meadow and apply it.

This yields the flag
```
Congratulations here is the flag!

cm18-xZl2-eHC5-axW3-ZkZG
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)