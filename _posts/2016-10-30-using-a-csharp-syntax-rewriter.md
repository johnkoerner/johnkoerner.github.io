---
layout: post
status: publish
published: true
title: Using a CSharp Syntax Rewriter
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
- Code-Analysis
- roslyn
- Visual Studio 2015
---
One interesting feature of the roslyn engine is the `CSharpSyntaxRewriter`.  This is a base class which you can extend that implements the [visitor pattern](https://en.wikipedia.org/wiki/Visitor_pattern).  You simply override the `Visit` method that is appropriate for your use case and you can rewrite any portion of a syntax tree.

Consider the following code:

``` csharp
public class Foo
{
    public string _bar = "baz";
}
```

Now, let's say we want to change `"baz"` to something else.  To do this, we simply implement a new `CSharpSyntaxRewriter` that overrides the `VisitLiteralExpression` so that our code is only executed on `LiteralExpression` syntax nodes.  We then check to see if it is a `StringLiteralExpression` and if it is, then we create a new node.

``` csharp
class LiteralRewriter : CSharpSyntaxRewriter
{
    public override SyntaxNode VisitLiteralExpression(LiteralExpressionSyntax node)
    {
        if (!node.IsKind(SyntaxKind.StringLiteralExpression))
        {
            return base.VisitLiteralExpression(node);
        }

        var retVal = SyntaxFactory.LiteralExpression(SyntaxKind.StringLiteralExpression, 
                                                      SyntaxFactory.Literal("NotBaz"));
        return retVal;
    }
}
```

The rewriter can be passed any `SyntaxNode` and it will run on that node and its descendants.  So, to use this, I can get a `SyntaxTree` from a `SemanticModel` that I get from a `CSharpCompilation`. Here is a full working sample:

``` csharp
var tree = CSharpSyntaxTree.ParseText(@"
  public class Foo
  {
      public string _bar = ""baz"";
  }");
var Mscorlib = MetadataReference.CreateFromFile(typeof(object).Assembly.Location);
var compilation = CSharpCompilation.Create("MyCompilation",
    syntaxTrees: new[] { tree }, references: new[] { Mscorlib });
var model = compilation.GetSemanticModel(tree);
var root = model.SyntaxTree.GetRoot();

var rw = new LiteralRewriter();
var newRoot = rw.Visit(root);

Console.WriteLine(newRoot.GetText());
Console.ReadLine();
```

As you can see, a rewriter is a quick and easy way to manipulate a syntax node that you have access to.  It's a great tool to use when you have some simple changes you need to make to a syntax tree.

If you have come up with a good use for syntax rewriters, leave a comment below.