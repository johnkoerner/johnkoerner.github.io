---
layout: post
status: publish
published: true
title: Codemash CTF - 2 - Hobo Robo
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

    Hobo Robo prepared a paper chase for you.

[Start](https://codemash.hacking-lab.com/codemash/bots/bots.html)


Approach
---
The link takes you to the C3P0 wikipedia page (or so it seems).  Upon further inspection, you notice that the link actually takes you to https://codemash.hacking-lab.com/codemash/bots/bots.html, which immediately redirects you to the C3P0 wikipedia page.

I decied to curl the web page (to prevent the redirect) and saw the following:

    <html>
    <head>
            <title>Bots</title>
            <script type="text/javascript">
            eval(String.fromCharCode(105, 102, 32, 40, 33, 40, 110, 97, 118, 105, 103, 97, 116, 111, 114, 46, 117, 115, 101, 114, 65, 103, 101, 110, 116, 32, 61, 61, 61, 32, 39, 72, 111, 98, 111, 82, 111, 98, 111, 39, 41, 41, 32, 123, 32, 108, 111, 99, 97, 116, 105, 111, 110, 46, 114, 101, 112, 108, 97, 99, 101, 40, 39, 104, 116, 116, 112, 58, 47, 47, 101, 110, 46, 119, 105, 107, 105, 112, 101, 100, 105, 97, 46, 111, 114, 103, 47, 119, 105, 107, 105, 47, 67, 45, 51, 80, 79, 39, 41, 59, 125))
        </script>
    </head>
    <body style="background: white; border: 20px solid white;">
        <div style="widht: 100%; height: 100%; background: url('./robotbg.jpg') no-repeat center center fixed; -webkit-background-size: contain; -moz-background-size: contain; -o-background-size: contain; background-size: contain;">&#160;</div>
    </body>
    </html>

The obfuscated javascript is what handles the redirection, so that is not important, but the image that on the page is interesting. 

![](/content/robotbg.jpg)

A quick google search for some of the words in the image lead you to [Robot Interaction Language](http://roila.org/language-guide/vocabulary/).  Using that page to translate the image leads to the text:

   You must make word of addition two and two - This be name of page.

This takes us to https://codemash.hacking-lab.com/codemash/bots/four.html

Curling this page results in 

    <html>
    <head>
            <title>Bots</title>
            <meta name="description" content="Robots talk in ROILA language: eman egap eht esrever tsum">
        <meta name="keywords" content="secret, page, robots, fun, hacky easter, blrt, five, beep">
            <script type="text/javascript">
            eval(String.fromCharCode(105, 102, 32, 40, 33, 40, 110, 97, 118, 105, 103, 97, 116, 111, 114, 46, 117, 115, 101, 114, 65, 103, 101, 110, 116, 32, 61, 61, 61, 32, 39, 72, 111, 98, 111, 82, 111, 98, 111, 39, 41, 41, 32, 123, 32, 108, 111, 99, 97, 116, 105, 111, 110, 46, 114, 101, 112, 108, 97, 99, 101, 40, 39, 104, 116, 116, 112, 58, 47, 47, 101, 110, 46, 119, 105, 107, 105, 112, 101, 100, 105, 97, 46, 111, 114, 103, 47, 119, 105, 107, 105, 47, 67, 45, 51, 80, 79, 39, 41, 59, 125))
        </script>
    </head>
    <body style="background: white; border: 20px solid white;">
        <div style="widht: 100%; height: 100%; background: url('./robotbg2.jpg') no-repeat center center fixed; -webkit-background-size: contain; -moz-background-size: contain; -o-background-size: contain; background-size: contain;">&#160;</div>
    </body>
    </html>

The image on this page is

![](/content/robotbg2.jpg)

The image didn't provie any clues this time, but looking at the meta tag on that page `content="Robots talk in ROILA language: eman egap eht esrever tsum`. Looking at the text it says `must reverse the page name`.  

Going to https://codemash.hacking-lab.com/codemash/bots/ruof.html results in the following image, which is our flag:

![](/content/robotbg3_1337807.jpg)

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)