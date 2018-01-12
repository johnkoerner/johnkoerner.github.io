---
layout: post
status: publish
published: true
title: Codemash CTF - 5 - Bools for Fools
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
05 - Bools for fools
Calculate this!

((not(a) and b) or c) xor d

```
[boolsforfools_fixed.zip](/content/boolsforfools_fixed.zip)

Approach
---
The hint is pretty obvious that you need to do some boolean operations on the attached files.  To start, I load the text and get rid of all of the whitespace, so I am just dealing with the 1s and 0s.  I then wrote functions for each of the operatoins (not, and, or, and xor)

Here is the `not` implementation as an example.  See the full source [on GitHub](https://github.com/johnkoerner/2018CodeMashCTF)
``` csharp
public static string Not(string input)
{
    var result = new StringBuilder();
    foreach (var s in input)
    {
        Validate(s);
        if (s == '1')
        {
            result.Append("0");
        }
        else if (s == '0')
        {
            result.Append("1");
        }
        else
        {
            throw new Exception();
        }
    }

    return result.ToString();
}
```

Once I had all of that wired up, I ended up with the result of:

```
1111111000100110001111111
1000001011100011001000001
1011101010000010101011101
1011101001001010001011101
1011101011101100101011101
1000001010101101001000001
1111111010101010101111111
0000000010110011100000000
1101001100011100001110110
0111110011011000111101001
0000101010011100110101001
0011010111111101110111010
1101011000110101111101010
0100100101010100111001011
1001001010010110100010101
0100010011010110000101001
1111111100101101111110101
0000000010001010100010101
1111111011111111101011111
1000001001001010100010110
1011101001001110111110010
1011101010110101000110000
1011101000101111000011001
1000001011011100010100000
1111111010100001100000111
```

I tried various encodings and translations on this data, until we got a hint from CodeMashCTF:

<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">Challenge 5 is all that QR&#39;d. (pun intended)) After you finish your calculations for challenge 5 - you may notice a picture forming in the matrix. It may help to mark all cells with a 1, black, and all cells with a 0, white...</p>&mdash; CodeMash CTF (@CodeMashCTF) <a href="https://twitter.com/CodeMashCTF/status/948215403729301504?ref_src=twsrc%5Etfw">January 2, 2018</a>

</blockquote>

<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

Now it is obvious that this represents a QR code.  I wrote a little code to write data to an image:

``` csharp
public static string Format(string input)
{
    var bmp = new System.Drawing.Bitmap(25, 25);
    var g = System.Drawing.Graphics.FromImage(bmp);
    var whitepen = new Pen(Brushes.White);
    var blackpen = new Pen(Brushes.Black);
    var row = 0;
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < input.Length; i++)
    {
        if (i % 25 == 0 && i != 0)
        {
            row++;
            sb.Append("\r\n");
        }
        sb.Append(input[i] == '1' ? "1" : "0");
        var pen = input[i] == '1' ? blackpen : whitepen;
        g.DrawRectangle(pen, i % 25, row, 1, 1);
    }
    bmp.Save("D:\\temp\\cm\\qr.bmp");
    g.Dispose();
    bmp.Dispose();
    return sb.ToString();
}
```

The output image looks like this:

<img src ="/content/qr.bmp" width="75" />


[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)
