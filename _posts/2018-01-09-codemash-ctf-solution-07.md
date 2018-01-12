---
layout: post
status: publish
published: true
title: Codemash CTF - 7 - Happy Eyes
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
07 - Happy Eyes
Barbara really loves to chat with all friends.

To express joy they use the characters ^^ which represent eyes of a smiling face.

Can you find this happy flag?

Hint: Offset by 2

1xT-Gcm8FV-5cYN-iBc-syHW
```

Approach
---
This one is tricky. The offset 2 indicates that there is a tool out there that takes an input. Looking at the text, it contains `c`, `m`, `1`, and `8`, so it may just be a scramble of the text.  After playing with a lot of tools online, I found a super tool that has all sorts of cipher varieties:

https://www.dcode.fr/

After that, another hint came along from the @codemashctf twitter account:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">A big dropoff in US submissions of challenge 7 answers... Just find the right tool to get the job done!  Are you on the fence?  Don&#39;t let these Europeans scare you off, they can&#39;t win any way.</p>&mdash; CodeMash CTF (@CodeMashCTF) <a href="https://twitter.com/CodeMashCTF/status/948933350311546880?ref_src=twsrc%5Etfw">January 4, 2018</a>

</blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

The hint was subtle, but the `On the fence` portion just didn't fit.  A quick search of the ciphers that contain fence, and you find the [Rail Fence](https://en.wikipedia.org/wiki/Rail_fence_cipher) cipher.  I found a tool that included the offset:

https://www.geocachingtoolbox.com/index.php?page=railFenceCipher

Setting the offset to 2 results in:

    cm18-FxVs-T5yc-YHNG-WicB

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)
