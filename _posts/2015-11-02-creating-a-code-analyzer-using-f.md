---
layout: post
status: publish
published: true
title: Creating a Code Analyzer using F#
author:
  display_name: John Koerner
  login: admin
  email: blog@johnkoerner.net
  url: ''
author_login: admin
author_email: blog@johnkoerner.net
wordpress_id: 1458
wordpress_url: https://johnkoerner.com/?p=1458
date: '2015-11-02 04:39:05 -0500'
date_gmt: '2015-11-02 04:39:05 -0500'
categories:
- Code Analysis
tags:
- C#
- Code Analysis
- roslyn
- Visual Studio 2015
- F#
---
**Note**: This article covers creating a C#/VB code analyzer using F#. At this time there is no Roslyn support for analyzing F# code.

In the past we have covered creating code analyzers using [C#](https://johnkoerner.com/csharp/creating-your-first-code-analyzer/) and [VB](https://johnkoerner.com/code-analysis/creating-your-first-vb-analyzer/). Creating an analyzer in F# is just as easy. I have just started the process of learning F# and figured an analyzer would be a great test project to learn on. There aren't official templates for F# analyzers, but you can take the C# templates and use those as a starting point for F#.

To start, make sure you have the latest version of the [.Net Compiler Platform SDK](https://visualstudiogallery.msdn.microsoft.com/2ddb7240-5249-4c8c-969e-5d05823bcb89) installed.

Next, you'll want to create an "Analyzer with Code Fix (NuGet + VSIX)" project under the Visual C#->Extensibility group in the project templates.

![New Project Dialog](https://johnkoerner.com/wp-content/uploads/2015/06/newproject.png)

Once you have the project created, add a new F# library project to the solution. With the new project added to the solution, you'll next want to modify the VSIX project to deploy the F# project instead of the C# project. To do this, modify the source.extension.vsixmanifest file and go to the Assets tab. Switch the project on both the `Analyzer` and `MefComponent` to be the new F# library.

![VsixManifest](https://johnkoerner.com/wp-content/uploads/2015/11/VsixManifest.png)

Now you can remove the C# analyzer and test project form the solution.

You solution is now set, but the F# project needs the appropriate references in order to work with analyzers. Add the `Microsoft.CodeAnalysis` NuGet package to the F# project.

Now we can start coding the analyzer. We'll implement the same basic analyzer that comes with the C# samples, where it raises a diagnostic whenever there are lowercase characters in type names.

We'll start creating our analyzer by importing some namespaces we'll need later in the code.

    namespace FSharpFirstAnalyzer
    open Microsoft.CodeAnalysis
    open Microsoft.CodeAnalysis.Diagnostics
    open System.Collections.Immutable
    open System.Linq
    open System

Next we'll declare our analyzer and inherit from the DiagnosticAnalyzer base class. Notice that we are registering our analyzer as a C# only analyzer.

    [<DiagnosticAnalyzer(Microsoft.CodeAnalysis.LanguageNames.CSharp)>]
    type public MyFirstFSAnalyzer() = 
        inherit DiagnosticAnalyzer()

Now we can create a descriptor for our diagnostic and override the `SupportedDiagnostics` property to return our diagnostics.

    let descriptor = DiagnosticDescriptor("FSharpIsLowerCase", 
                                "Types cannot contain lowercase letters", 
                                "{0} contains lowercase letters" , 
                                "Naming", 
                                DiagnosticSeverity.Warning, 
                                true, 
                                "User declared types should not contain lowercase letters.", 
                                null)

    override x.SupportedDiagnostics with get() = ImmutableArray.Create(descriptor)

Finally, we can do our work in the `Initialize` override. We'll create a symbol analysis function and check if the symbol has any lowercase characters. To do this, we'll perform a match on the `Symbol.Name`. Finally we'll register that function with the context passed into the Initialize method.

        override x.Initialize (context: AnalysisContext) =
            let isLower = System.Func<_,_>(fun l -> Char.IsLower(l))
            let analyze (ctx: SymbolAnalysisContext) = 
                match ctx.Symbol with
                    | z when z.Name.ToCharArray().Any(isLower) -> 
                        let d = Diagnostic.Create(descriptor, z.Locations.First(), z.Name)
                        ctx.ReportDiagnostic(d)
                    | _->()

            context.RegisterSymbolAction(analyze, SymbolKind.NamedType)

At this point, we can run the analyzer solution and a new Visual Studio instance will appear. This is referred to as the experimental instance and has completely isolated settings from the instance in which you do your main development. Create a simple C# console application and open the `Program.cs`. You should get a diagnostic on the `Program` class indicating it contains lowercase letters.

![lowercaseLetters](https://johnkoerner.com/wp-content/uploads/2015/11/lowercaseLetters.png)

The full code for our F# analyzer is:

    namespace FSharpFirstAnalyzer
    open Microsoft.CodeAnalysis
    open Microsoft.CodeAnalysis.Diagnostics
    open System.Collections.Immutable
    open System.Linq
    open System

    [<DiagnosticAnalyzer(Microsoft.CodeAnalysis.LanguageNames.CSharp)>]
    type public MyFirstFSAnalyzer() = 
        inherit DiagnosticAnalyzer()
        let descriptor = DiagnosticDescriptor("FSharpIsLowerCase", 
                                "Types cannot contain lowercase letters", 
                                "{0} contains lowercase letters" , 
                                "Naming", 
                                DiagnosticSeverity.Warning, 
                                true, 
                                "User declared types should not contain lowercase letters.", 
                                null)

        override x.SupportedDiagnostics with get() = ImmutableArray.Create(descriptor)

        override x.Initialize (context: AnalysisContext) =
            let isLower = System.Func<_,_>(fun l -> Char.IsLower(l))
            let analyze (ctx: SymbolAnalysisContext) = 
                match ctx.Symbol with
                    | z when z.Name.ToCharArray().Any(isLower) -> 
                        let d = Diagnostic.Create(descriptor, z.Locations.First(), z.Name)
                        ctx.ReportDiagnostic(d)
                    | _->()

            context.RegisterSymbolAction(analyze, SymbolKind.NamedType)

As you can see, creating an analyzer in F# is possible, and once you have the tooling setup, the development flow is not much different than that of a C# or VB analyzer. Overall, I think matching functionality in F# provides interesting possibilities when creating analyzers for Roslyn.