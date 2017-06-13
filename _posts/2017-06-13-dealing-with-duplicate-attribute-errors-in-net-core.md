---
layout: post
status: publish
published: true
title: Dealing with Duplicate Assembly Attributes in .Net Core
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
When migrating a project from .Net Framework to .Net Standard, you may run into issues where you get duplicate assembly attributes. An example you might see is something like this:

    Severity	Code	Description	Project	File	Line	Suppression State
    Error	CS0579	Duplicate 'System.Reflection.AssemblyTitleAttribute' attribute MyProject
    D:\Dev\MyProject\obj\Debug\netstandard2.0\MyProject.AssemblyInfo.cs	20	N/A

I ran into this because I have an AssemblyInfo.cs with an `AssemblyTitleAttribute` and the .Net Standard project is also generating the `AssemblyTitleAttribute`. After reading through some [GitHub issues](https://github.com/dotnet/cli/issues/4710), it appears there are two ways around this issue.

First, I could remove the `AssemblyInfo.cs` that I already had in my project and add the appropriate attributes to the `csproj` file. Since I am converting a .Net Framework project in place with a new solution and csproj file, this will not work for me. I am left with the secon option.

Add settings to the `csproj` file to indicate that the various attributes should not be generated. Here is an example `csproj` file with a few of the attributes disabled:

    <Project Sdk="Microsoft.NET.Sdk">
        <PropertyGroup>
            <TargetFramework>netstandard2.0</TargetFramework>
            <GenerateAssemblyConfigurationAttribute>false</GenerateAssemblyConfigurationAttribute>
            <GenerateAssemblyDescriptionAttribute>false</GenerateAssemblyDescriptionAttribute>
            <GenerateAssemblyProductAttribute>false</GenerateAssemblyProductAttribute>
            <GenerateAssemblyTitleAttribute>false</GenerateAssemblyTitleAttribute>
        </PropertyGroup>    
    </Project>

Once those settings are added to the `csproj` file, everything compiles and there are no duplicate attribute errors.

