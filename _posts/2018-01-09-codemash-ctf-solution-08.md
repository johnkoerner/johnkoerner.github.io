---
layout: post
status: publish
published: true
title: Codemash CTF - 8 - Happy Eyes
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
08 - Lock
The key for that lock got lost.

If you are good at lock picking you will find the flag.

Lock.class
```

Approach
---
A .class file is a java compiled file, so I simply uploaded the file to an online decompiler and got the following code:

```
package com.hackinglab.ctf;
import java.io.PrintStream;

public class Lock { public Lock() {} private static String key = "lockpickingisfun";
  private static String cipher = "?8hiyKT5fw*W^J~art3t.47i";
  
  public static void main(String[] args) {
    if (args.length != 1) {
      System.out.println("Provide codeword to open the lock!");
      System.exit(-1);
    }
    String input = args[0];
    StringBuffer codeword = new StringBuffer();
    for (int i = 0; i < cipher.length(); i++) {
      codeword.append((char)(key.charAt(i % key.length()) - cipher.charAt(i) + 54));
    }
    if (codeword.toString().equals(input)) {
      System.out.println("Correct codeword! The Lock is open!");
    } else {
      System.out.println("Wrong codeword!");
    }
  }
}
```

I took the guts of the code and re-worked it into a small C# app to give me the correct output.

```
private static String key = "lockpickingisfun";
private static String cipher = "?8hiyKT5fw*W^J~art3t.47i";

public static void Main(String[] args)
{
    String input = key; ;
    StringBuilder codeword = new StringBuilder();
    for (int i = 0; i < cipher.Length; i++)
    {
        codeword.Append((char)(key[(i % key.Length)] - cipher[i] + 54));
    }
    Console.WriteLine(codeword.ToString());
    Console.ReadLine();
}
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)