---
layout: post
status: publish
published: true
title: Codemash CTF - 11 - Bacon!
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
11 - Bacon!
Get the bacon!

```
[1000.zip](/content/1000.zip)

Approach
---
This is a zip file that contains a git repository. Which contains a zip file, which contains a git repository, and so on and so forth. Looking at the git repository, it looks like there is a deleted file, so if we reset the repository, the file is restored.

Since there is a pattern to the names, it should be pretty easy to script.

```
Param([int]$startId)

Add-Type -assembly "system.io.compression.filesystem"
$currId = $startId;

do 
{
    $next = ($currId-1).ToString().PadLeft(4,"0")  
    $currStr = $currId.ToString().PadLeft(4,"0")
    [io.compression.zipfile]::ExtractToDirectory("D:\temp\cmgit\$currStr\$next.zip", "D:\temp\cmgit")
    cd "D:\temp\cmgit\$next"
    git reset --hard
    $currId = $currId -1;
    
} While( $currId -gt 0)
```
Then I can invoke the script using 

`.\1000.ps1 1000`

This worked for the first 100 entries and then the format changed. For number `901`, it skipped `900` and went to `0899.zip`. I renamed folder `0901` to `0900` and continued on.

`.\1000.ps1 900`

This worked until `0613` where the zip file simply contained an image named trunk.jpg:

![](/content/trunk.jpg)

After a bit of playing and seeing that there were multiple commits on the branch, I reset to 2 commits back (`git checkout HEAD~2`) and the zip file followed our pattern again. 

`.\1000.ps1 0613`

This worked until `278` which had an image named `scooter.jpg` and a zip file:

![](/content/scooter.jpg)

Checking the branches, there is a new branch called `blaster`:
```
λ  git branch -l
  blaster
* master
```

Switch to that branch and continue on:
`.\1000.ps1 278`

That worked until 0044, which wasn't a valid git repository.  I went back to the 0045 directory and tried to extract the zip file and was prompted for a passowrd. The original file name offered a hint on where to look:

![](/content/44hint.png)

Doing a `git log` on the 0045 folder yields:
commit b364135b78a640c2889dc1fc44e5e1c3326b8cd2 (HEAD -> master)
Author: Gorilla <gorilla@codemash.org>
Date:   Thu Dec 7 09:42:54 2017 -0500

    Commit committed. Pass is fluffy99

Reset the git repo again and continue on.

`.\1000.ps1 0044`

This leads us to folder `0001`, which has a flag image inside it:

![](/content/11flag.jpg)

[Return to the full breakdown of the Codemash CTF](/codemash/codemash-ctf-breakdown/)