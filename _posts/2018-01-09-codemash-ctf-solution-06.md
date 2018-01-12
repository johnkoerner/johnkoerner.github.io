---
layout: post
status: publish
published: true
title: Codemash CTF - 6 - Witchcraft
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
06 - Witchcraft
I was just messing around with my magic wand trying out some new spells and all of a sudden the flag was gone.

All I was left with is the following:

    363336643331333832643438363537373432326436383530
    333137323264346337393738333932643635373035343465

Can you undo my spell and get the flag?
```

Approach
---
The first thing that jumped out to me on this one is the number of `3`s in the text. Obviously this is some sort of encoded string. Taking the first few bytes `36 33` as hex numbers and convert them to a string `63`. `63` is the ascii code for `c` and since I knew all of the flags started with cm, I definitely had a lead.  

I wrote a small script to process through the entire string:

``` csharp
static void Main(string[] args)
{
    var input = "363336643331333832643438363537373432326436383530333137323264346337393738333932643635373035343465";
    Console.WriteLine(HexToString(input));
    Console.WriteLine(HexToString(HexToString(input)));
    Console.ReadLine();
}

static string HexToString(string source)
{
    StringBuilder sb = new StringBuilder();
    for(int i=0; i<source.Length; i+=2)
    {
            sb.Append(Convert.ToChar(int.Parse( source.Substring(i, 2), System.Globalization.NumberStyles.HexNumber)));
    }           return sb.ToString();
}
```

This yields the output:

```
636d31382d486577422d685031722d4c7978392d6570544e
cm18-HewB-hP1r-Lyx9-epTN
```

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)
