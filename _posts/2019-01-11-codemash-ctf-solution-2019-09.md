---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Dot Nutcracker
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
Can you crack this nut? Find the right password and make the binary reveal the flag!

[cracker.exe](/content/Cracker.exe)

Hint
---
If you think you have the right password, but the binary crashes, something small is missing. Take a closer look!


Approach
---
Since this is a .net exe, I immediately opened it in [ILSpy](https://github.com/icsharpcode/ILSpy).  The main method looks like this:

``` csharp
Console.WriteLine("Yo wazzup! Give me the password! ");
int num = 3;
CryptoHelper cryptoHelper = new CryptoHelper();
while (num > 0)
{
  Console.WriteLine($"You have {num}/3 attempt(s) left.");
  Console.Write("Enter passphrase: ");
  string text = Console.ReadLine();
  string text2 = CryptoHelper.DecryptStringAES("EAAAAH5ZA4kASLVjLUsYmLK3h74KWmkS4BvBS61BuaD4lnyqdz3AO8/xfGO1atVdci0x1g==");
  if (text != null && cryptoHelper.Equals(text2, text))
  {
    Console.WriteLine(string.Format("Decrypted Flag is: {0}", CryptoHelper.DecryptStringAES("EAAAAOlDKPcRaUj/ITV1q9IHN1bAQyUWxZqVob+G1gpmyoIJIPej1O3T4TWnRUndqp4NnA==", CryptoHelper.GetHashString(text2), text, text)));
    Console.WriteLine("Press enter to quit");
    Console.ReadLine();
    Environment.Exit(1337);
  }
  num--;
  Console.WriteLine("That's wrong.");
}
Console.WriteLine("SORRY, GAME OVER");
Console.WriteLine("Press enter to quit");
Console.ReadLine();
Environment.Exit(0);
```

I saved the project using ILSpy and then started writing out the results to the console. I started by writing out `text2`, which is:

acrackeradaykeepsthedoctoraway

However, when I use that as the password, the application crashes. Upon some digging into the methods, I found that the equals call in the CryptoHelper class is tricky:

``` csharp
public bool Equals(string a, string b)
{
  if (!b.Equals(a))
  {
    return a.Equals(b + "y");
  }
  return true;
}
```
Using the password of `acrackeradaykeepsthedoctorawa`, yields our flag:

```
Decrypted Flag is: cm19-NuSS-kn4c-kker-GamE
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)