---
layout: post
status: publish
published: true
title: Simple Interprocess Communication in .Net Core using Protobuf
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
- Jenkins
- Visual Studio 2017
- dotnetcore
---
In the past, I have used WCF to handle inter-process communication (IPC) between various separate components of my client applications. Since .Net Core [doesn't yet support](https://github.com/dotnet/wcf/issues/1200) WCF server side code, I had to look into alternatives.  The two main approaches to this that I have found are `TCPServer` and `NamedPipeServerStream`. [Other's](http://www.c-sharpcorner.com/article/building-a-tcp-server-in-net-core-on-ubuntu/) have covered the TCP approach, so I wanted to see what could be done with the `NamedPipeServerStream`.  

I started reading the [MSDN documentation](https://msdn.microsoft.com/en-us/library/bb546085(v=vs.110).aspx) on the basics of IPC with named pipes and found that it worked with .Net Core 2.0 with no changes. This is the true benefit of .Net Core.  An older article about IPC is still completely relevant even though the code is now running on a Mac instead of a Windows Machine.  One thing I didn't like too much about that article was the `StreamString` class and I wanted to see what I could due with plain old C# objects.

I decided to start try out [Protobuf](https://github.com/mgravell/protobuf-net). I had heard about it in the past and figured this would be a good foray into learning more about it.  Since I was developing a client and a server, I decided I would start with the API and put that into a shared class project. So I created a `Common` project and defined a `Person` class in there:

	[ProtoContract]
    public class Person
    {
		[ProtoMember(1)]
		public string FirstName { get; set; }

		[ProtoMember(2)]
		public string LastName { get; set; }
    }

Decorating the class with the protobuf attributes was all I had to do.  Now that it is defined in the common class, I could write a server to serve up the data and a client to consume the data, each referencing the `Common` library. Next up, I created the server.  Following the linked example above, I defined the server console application as:

    static void Main(string[] args)
    {
        Console.WriteLine("Starting Server");

        var pipe = new NamedPipeServerStream("MyTest.Pipe", PipeDirection.InOut);
        Console.WriteLine("Waiting for connection....");
        pipe.WaitForConnection();

        Console.WriteLine("Connected");

        Serializer.Serialize(pipe, new Person() { FirstName="Janey", LastName = "McJaneFace" });
        pipe.Disconnect();
    }

I am simply defining the `NamedPipeServerStream` to listen on a pipe named "MyTest.Pipe". For now, the code immediately returns an object to the connection, that can be read from the client side. This is achieved using protobuf's `Serializer.Serialize` method.  To define the client, I need to use a `NamedPipeClientStream` to connect to the same pipe.

    static void Main(string[] args)
    {
        Console.WriteLine("Client");
        var pipe = new NamedPipeClientStream(".", "MyTest.Pipe", PipeDirection.InOut, PipeOptions.None);
        Console.WriteLine("Connecting");
        pipe.Connect();
        var person = Serializer.Deserialize<Person>(pipe);
        Console.WriteLine($"Person: {person.FirstName} {person.LastName}");
        Console.WriteLine("Done");
    }

Once I connect, I then use protobuf's `Serializer.Deserialize` method to read from the stream and deserialize the person object.  That's it.  I am passing data from one process to another in .Net core.  If you are using .Net Core 1.x, you will need to explicitly add a reference to the `System.IO.Pipes` nuget package.  And for both 1.x and 2.0 .net core, you need to add a nuget reference to protobuf. 

A fully working solution for this can be found as a sample GitHub [project](https://github.com/johnkoerner/SimpleIPCDotNetCore). There appear to be other .Net Core/Standard projects([1](https://github.com/MhAllan/TcpServiceCore), [2](https://github.com/leuchterag/Net.Ipc)) attempting to better facilitate IPC and it will be interesting to see how they mature with the ecosystem. My hope is that some flavor of WCF server makes its way over to .Net core, to make porting code that much easier.

