---
layout: post
status: publish
published: true
title: Codemash CTF - 3 - The Riddler
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
    03 - 1337 Riddler
    1337 r1ddler h4s a puzzl3 f0r u 2 solve!

    H3 1s l1st3n1ng 0n th3 <i>BEST</i> p0r7 on this s3rv3r!

Approach
---
The clue in this puzzle to get your started is that you need to connect to an open port on the server. 

Using telnet, I connected to the server on port 8357 (BEST in l33t 5p34k):

    telnet> o codemash.hacking-lab.com 8357
    Trying 80.74.140.117...
    Connected to codemash.hacking-lab.com.
    Escape character is '^]'.
    Make an educated guess, dude:
    1
    I need 20 digits, dude!
    Connection closed by foreign host.

20 digits??!? This is going to take a while to do by hand.  Let's put in 20 digits and see what happens:

    Make an educated guess, dude:
    11111111111111111111
    0<

As I was working this out, the @codemashctf account sent out a hint.
<blockquote class="twitter-tweet" data-lang="en"><p lang="en" dir="ltr">For challenge 3: The advice I am going to give at the precompiler: The first # is 7. Try once with 20 9&#39;s then a 2nd time with 20 7&#39;s and see the difference in what is returned.  the # and symbol that is returned does mean something. 1234567890, How to try, is up to you though.</p>&mdash; CodeMash CTF (@CodeMashCTF) <a href="https://twitter.com/CodeMashCTF/status/947474146992246784?ref_src=twsrc%5Etfw">December 31, 2017</a>

</blockquote>
<script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

So, I tried a 7 followed by all 1s:

    Make an educated guess, dude:
    71111111111111111111
    1<

And then a 9 followed by all 1s:

    Make an educated guess, dude:
    91111111111111111111
    0>

Based on the few things I have tried, it appears that the number is the number of characters that are correct and the `<` and `>` indicate if the next number is larger or smaller than the number you input.

We could manually walk through the logic and eventually solve this, but, it could also be scripted. Here is a quick C# console app I put together to do this:

``` csharp
static void Main(string[] args)
{
    int knownCount = 1;
    string known = "7";
    while (true)
    {
        bool found = false;
        foreach (var guess in GetGuesses(known))
        {
            TcpClient client = new TcpClient("codemash.hacking-lab.com", 8357);
            var s = client.GetStream();

            ReadHeader(s);
            Console.Write(guess + " - ");

            s.Write(Encoding.ASCII.GetBytes(guess + "\r\n"), 0, 22);
            byte[] result = new byte[3];
            while (true)
            {
                var cnt = s.Read(result, 0, 3);
                Console.WriteLine(Encoding.ASCII.GetString(result).Trim());
                string number = Encoding.ASCII.GetString(result).Trim().TrimEnd(new[] {'>','<'});
                
                if (int.Parse(number) > knownCount)
                {
                    known += guess[knownCount];
                    knownCount++;
                    found = true;
                }
                if (cnt <= 0) break;
            }
            if (found) break;
        }
    }
}

static string[] GetGuesses(string known)
{
    var result = new List<string>();
    for (int i=0; i<10; i++)
    {
        var x = known + i.ToString();
        x=x.PadRight(20, '5');
        result.Add(x);
    }
    return result.ToArray();
}

static void ReadHeader(Stream s)
{
    byte[] result = new byte[1];
    while (s.Read(result, 0, 1) >0)                
        if (result[0] == Encoding.ASCII.GetBytes("\n")[0])  break;
}
```
Running this code eventually gives us the value `78025928232920712967`. Popping that into a telnet session gives you:

    Make an educated guess, dude:
    78025928232920712967

    Congrats! Here's your flag:
    cm18-Glz3-yM2k-h9i9-wntS


[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)