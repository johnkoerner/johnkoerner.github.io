---
layout: post
status: publish
published: true
title: Special Folder Enum Values on Windows and Mac in .Net Core
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_email: blog@johnkoerner.net
categories:
- csharp
tags:
- csharp
- dotnetcore
- Visual Studio 2017
---
On Windows it is common to use [Environment.SpecialFolder](https://msdn.microsoft.com/en-us/library/system.environment.specialfolder(v=vs.110).aspx) to access certain folders instead of having to hard code the paths or write the appropriate lookup code for them.  Now that code is being ported to Mac using .Net core, I thought I would document the various values that appear for the special folders when running .Net Core code on the Mac.  Below is a table that contains the data for a user whose username is `john` on both the Windows Machine and the Mac OSX machine. 


| Enum Value             | Windows Value                                                                             | Mac Value                      |
|------------------------|-------------------------------------------------------------------------------------------|--------------------------------|
| AdminTools             |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Administrative Tools |                                |
| ApplicationData        |  C:\Users\john\AppData\Roaming                                                            |  /Users/john/.config           |
| CDBurning              |  C:\Users\john\AppData\Local\Microsoft\Windows\Burn\Burn                                  |                                |
| CommonAdminTools       |  C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Administrative Tools                |                                |
| CommonApplicationData  |  C:\ProgramData                                                                           |  /usr/share                    |
| CommonDesktopDirectory |  C:\Users\Public\Desktop                                                                  |                                |
| CommonDocuments        |  C:\Users\Public\Documents                                                                |                                |
| CommonMusic            |  C:\Users\Public\Music                                                                    |                                |
| CommonOemLinks         |                                                                                           |                                |
| CommonPictures         |  C:\Users\Public\Pictures                                                                 |                                |
| CommonProgramFiles     |  C:\Program Files\Common Files                                                            |                                |
| CommonProgramFilesX86  |  C:\Program Files (x86)\Common Files                                                      |                                |
| CommonPrograms         |  C:\ProgramData\Microsoft\Windows\Start Menu\Programs                                     |                                |
| CommonStartMenu        |  C:\ProgramData\Microsoft\Windows\Start Menu                                              |                                |
| CommonStartup          |  C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup                             |                                |
| CommonTemplates        |  C:\ProgramData\Microsoft\Windows\Templates                                               |                                |
| CommonVideos           |  C:\Users\Public\Videos                                                                   |                                |
| Cookies                |  C:\Users\john\AppData\Local\Microsoft\Windows\INetCookies                                |                                |
| Desktop                |  C:\Users\john\Desktop                                                                    |  /Users/john/Desktop           |
| DesktopDirectory       |  C:\Users\john\Desktop                                                                    |  /Users/john/Desktop           |
| Favorites              |  C:\Users\john\Favorites                                                                  |  /Users/john/Library/Favorites |
| Fonts                  |  C:\WINDOWS\Fonts                                                                         |  /Users/john/Library/Fonts     |
| History                |  C:\Users\john\AppData\Local\Microsoft\Windows\History                                    |                                |
| InternetCache          |  C:\Users\john\AppData\Local\Microsoft\Windows\INetCache                                  |  /Users/john/Library/Caches    |
| LocalApplicationData   |  C:\Users\john\AppData\Local                                                              |  /Users/john/.local/share      |
| LocalizedResources     |                                                                                           |                                |
| MyComputer             |                                                                                           |                                |
| MyDocuments            |  C:\Users\john\Documents                                                                  |  /Users/john                   |
| MyDocuments            |  C:\Users\john\Documents                                                                  |  /Users/john                   |
| MyMusic                |  C:\Users\john\Music                                                                      |  /Users/john/Music             |
| MyPictures             | C:\Users\john\Pictures                                                                    |  /Users/john/Pictures          |
| MyVideos               |  C:\Users\john\Videos                                                                     |                                |
| NetworkShortcuts       |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Network Shortcuts                        |                                |
| PrinterShortcuts       |                                                                                           |                                |
| ProgramFiles           |  C:\Program Files                                                                         |  /Applications                 |
| ProgramFilesX86        |  C:\Program Files (x86)                                                                   |                                |
| Programs               |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Start Menu\Programs                      |                                |
| Recent                 |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Recent                                   |                                |
| Resources              |  C:\WINDOWS\resources                                                                     |                                |
| SendTo                 |  C:\Users\john\AppData\Roaming\Microsoft\Windows\SendTo                                   |                                |
| StartMenu              |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Start Menu                               |                                |
| Startup                |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup              |                                |
| System                 |  C:\WINDOWS\system32                                                                      |  /System                       |
| SystemX86              |  C:\WINDOWS\SysWOW64                                                                      |                                |
| Templates              |  C:\Users\john\AppData\Roaming\Microsoft\Windows\Templates                                |                                |
| UserProfile            |  C:\Users\john                                                                            |  /Users/john                   |
| Windows                |  C:\WINDOWS                                                                               |                                |

The code for this is pretty straightforward. I enumerate over the possible enum values and output them to a CSV. 

``` csharp
static void Main(string[] args)
{
    StringBuilder sb = new StringBuilder();
    foreach (Environment.SpecialFolder sf in Enum.GetValues(typeof(System.Environment.SpecialFolder)))
    {
        sb.AppendLine($"{sf.ToString()}, {Environment.GetFolderPath(sf)}");
    }
    var path = System.IO.Path.GetDirectoryName(Assembly.GetExecutingAssembly().FullName);
    var fileName = GetFileName();
    var filePath = System.IO.Path.Combine(path, $"{fileName}.csv");
    System.IO.File.WriteAllText(filePath, sb.ToString());
}

static string GetFileName()
{
    if (RuntimeInformation.IsOSPlatform(OSPlatform.Windows))
        return "Win";
    else if (RuntimeInformation.IsOSPlatform(OSPlatform.OSX))
        return "OSX";

    return "Linux";
}
```
If you just want to pull the code and run it, I have a copy up on [GitHub](https://github.com/johnkoerner/NetCoreSpecialFolders/blob/master/Program.cs). As you can see, some special folders have a direct mapping to Mac OSX and others do not.  When you think about it, they all make sense.  As long as you understand the values you will get back in the various scenarios, you can use the values that are appropriate for your application.