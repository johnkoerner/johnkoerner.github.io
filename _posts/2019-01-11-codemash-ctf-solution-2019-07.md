---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Espresso
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
Espresso. What else?

[Espresso.class](/content/Espresso.class)

Hint
---
Peek into the .class file, and find out what it is doing.


Approach
---
I took the java class file and uploaded it to an [online decompiler](http://www.javadecompilers.com).  From there I got the java code:

```
package com.hackinglab.ctf;
import java.io.PrintStream;

public class Espresso { public Espresso() {} private static String key = "Stringab";
  private static String cipher = "'>xgx47#)~Fp?8k4%IHsC9_a";
  
  public static void main(String[] paramArrayOfString) {
    if (paramArrayOfString.length != 1) {
      System.out.println("You must enter the flag.");
      System.exit(-1);
    }
    String str = paramArrayOfString[0];
    System.out.println(str);
    StringBuffer localStringBuffer = new StringBuffer();
    for (int i = 0; i < cipher.length(); i++) {
      localStringBuffer.append((char)(key.charAt(i % key.length()) - cipher.charAt(i) + 55));
    }
    if (localStringBuffer.toString().equals(str)) {
      System.out.println("Flag correct, well done!");
    } else {
      System.out.println("Dude, that's wrong!");
    }
  }
}
```

I didn't have a java dev environment handy, but I did have a C# environment, so I converted the guts of the code from JAVA to C# and got the following program, taking out the checks and just writing the output to the console:

``` csharp
public class Espresso
{
    public Espresso() { }
    private static String key = "Stringab";
    private static String cipher = "'>xgx47#)~Fp?8k4%IHsC9_a";

    public static void Main(String[] paramArrayOfString)
    {           
        StringBuilder localStringBuffer = new StringBuilder();
        for (int i = 0; i < cipher.Length; i++)
        {
            localStringBuffer.Append((char)((int)key[i % key.Length] - (int)cipher[i] + 55));
        }

        Console.WriteLine(localStringBuffer.ToString());
        Console.ReadLine();
    }
}
```

This program yields the result:
```
cm19-java-c0ff-eeba-be98
```
[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)