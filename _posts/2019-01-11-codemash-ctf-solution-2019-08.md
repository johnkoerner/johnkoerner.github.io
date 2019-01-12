---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Danger Zone
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
Can you enter the danger.zone, and find the flag?

Service listening on:

`whale.hacking-lab.com:5553`

Note: this is NOT about the web site danger.zone!

Hint
---
Find out what service is listening on the port. nmap could be helpful for this kind of fingerprinting.


Approach
---
This challenge was all about finding the right tools and getting the command line args right. As the hint suggests, we can use `nmap` to scan that port to get more information.

```
nmap -p 5553 -T4 -A -v whale.hacking-lab.com
```

Yields the output (truncated for brevity):
```
PORT     STATE SERVICE VERSION

5553/tcp open  domain  ISC BIND 9.9.5 (Debian Linux 8.0 (Jessie))

```

The command tells us that BIND (DNS) is running on that port. Now the `zone` portion of the clue makes sense, since zones are a DNS concept. We can now use `dig` to see what we can find out.  I attempted a zone transfer and got the following:

```
dig AXFR danger.zone @whale.hacking-lab.com -p5553
```

```
; <<>> DiG 9.11.3-1ubuntu1.1-Ubuntu <<>> AXFR danger.zone @whale.hacking-lab.com -p5553
;; global options: +cmd
danger.zone.            604800  IN      SOA     danger.zone. admin.danger.zone.danger.zone. 2 604800 86400 2419200 604800
danger.zone.            604800  IN      NS      ns.danger.zone.
cm19-d4ng-rwil-lrob-Insn.danger.zone. 604800 IN A 10.0.13.37
ns.danger.zone.         604800  IN      A       10.0.0.2
danger.zone.            604800  IN      SOA     danger.zone. admin.danger.zone.danger.zone. 2 604800 86400 2419200 604800
;; Query time: 161 msec
;; SERVER: 80.74.140.188#5553(80.74.140.188)
;; WHEN: Fri Jan 11 23:26:24 STD 2019
;; XFR size: 5 records (messages 1, bytes 193)
```

Here is our flag:
```
cm19-d4ng-rwil-lrob-Insn
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)