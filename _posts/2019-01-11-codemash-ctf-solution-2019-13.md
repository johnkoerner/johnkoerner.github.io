---
layout: post
status: publish
published: true
title: Codemash CTF 2019 - Ghost Text
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
Ghost text is ... invisible!

[ghost_text.txt](/content/ghost_text.txt)

Hint
---
`AA_AAA_ = 01001`

Approach
---
The hint on this particular one is really required to figure out the problem.  I opened the text file in a hex editor and found that there were extra non-printable characters in the file.  My interpretation of the hint is that all non-printable characters were a 1 and for all `n` consecutive characters, we would have `n-1` 0s.

So I wrote a little C# script to do this for me:

``` csharp
StringBuilder sb = new StringBuilder();
var bytes = System.IO.File.ReadAllBytes(@"C:\Users\passp\Downloads\ghost_text.txt");

var consecutive = 0;
for (int i = 3; i < bytes.Length; i++)
{
    if (bytes[i] == 0xE2)
    {
        if (consecutive>1)
        {
            sb.Append('0', consecutive - 1);
        }
        consecutive = 0;
        sb.Append('1');
        if (bytes[i] == 0xE2)
            i += 2;
    }
    else
    {
        consecutive++;
    }
}

for (int i = 1; i < sb.Length+1; i++)
{

    Console.Write(sb[i-1]);
}

Console.ReadLine();  
```

This yields the output:
<div style="overflow:wrap; word-break: break-all;">
```
011000110110110100110001001110010010110101110010001100110011010001100100001011010110001001110100011101110110111000101101011101000110100001100101010000110010110101001000010000010101001001010011
```
</div>

Pasting that into an [online binary to text converter](https://www.rapidtables.com/convert/number/binary-to-ascii.html), yields our flag:

`cm19-r34d-btwn-theC-HARS`

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown-2019/)