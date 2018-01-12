---
layout: post
status: publish
published: true
title: Codemash CTF - 15 - P.A.L.M. Login
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
15 - P.A.L.M. Login ™
Folks at HOBO Authentication Systems implemented a new authentication system named P.A.L.M. Login

Prove that you can break it and find a pair of username and passcode to log on.
```
[Login](https://codemash.hacking-lab.com/codemash/palm.html)


Approach
---
The login page contains a button and two inputs. When you put in text and hit the login button you get the text of `nope`.

Looking at the javascript for the button click takes us to a function that does the following:

``` javascript
function checkEntries() {
    var u = document.getElementById('puser').value;
    var p = document.getElementById('ppass').value;
    var used = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
    var ok = false;
    if (u === 'cavs') {
        if (p > 0 && p.length == 10) {
            ok = true;
            for (i = 1; i <= 10; i++) {
                var digit = p.charAt(i - 1);
                var part = p.substring(0, i);
                if (used[digit] != 0 || part % i != 0) {
                    ok = false
                }
                if (used[digit] == 0) {
                    used[digit] = 1
                }
            }
        }
    }
    if (ok) {
        document.location.href = 'palm_' + u + '_' + p + '.html'
    } else {
        alert('nope')
    }
}
```

Looking at the code, the username needs to be `cavs` and the password is a 10 digit number.

I started writing a brute force algorithm and trying to figure out the number that way, but I decided to see what I could find about the properties of the number.

It is a 10 digit number, where every digit is only used once and the first N digits must be divisible by N.

Plugging those requirements into google yield lots of results.

- [Stack Exchange Explanation](https://puzzling.stackexchange.com/questions/3017/10-digit-number-where-first-n-digits-are-divisible-by-n)
- [Explanation with Video](https://mindyourdecisions.com/blog/2016/04/10/find-the-10-digit-number-where-n-digits-are-divisible-by-n-sunday-puzzle/)

Our number is 3816547290. Put that in the form and it takes you a page named

`palm_cavs_3816547290.html`

With the text of:

```
Congrats!
cm18-zbIc-O4Zh-gmxl-r5J6
```



[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)