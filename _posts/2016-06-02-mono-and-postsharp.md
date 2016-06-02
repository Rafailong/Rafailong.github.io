---
layout: post
title: Mono and Postsharp
---

# PostSharp with Mono (v3.2.3) 4.0 Framework


I have the task to add AOP to a project in my current job to attend some cross-cutting concerns like tracing and logging and exception catching.

I have used Postsharp but with .Net Framework v4.5 and VS 2012 and everything worked like a charm. To include Postsharp in the project was really easy and the generating custom aspect was just a codding pleasure! :)

Now I am working in a project that exposes a ServiceStack REST API and we have the idea to change all the servers from Windows to Linux with Mono so yes, I am doing some experiments with Mono and Postsharp.

I am running on a Windows box with Mono and VisualStudio with Mono 3.2.3 as target framework. If you want more information about the setting up VS with Mono go [here](http://erictummers.wordpress.com/2012/01/25/target-mono-from-visual-studio/).

As we all know Postsharp integrates with VS really well and adding it to a project is a trivial process BUT only if you have a .Net framework as target.

So adding Postsharp to a Mono targeted project was a manual task, adding the references to the assemblies and modifying the project file and adding _psproj_ file and _pssln_ file too.

The thing that I tested of Postsharp framework were:

- Multicast _aspecting_
- OnMethodBoundaryAspect
- OnExceptionAspect
- and Postsharp Diagnostic NLog

The results were:

### Multicast _aspecting_ ###

It just did not work. The reason is something that I do not know jet but I will update this  when I know it.

My scenario was: having a method that throws a ´NotSupportedException´ the method just kept throwing the exception and the method was never completed.

### OnMethodBoundaryAspect ###

This aspect was applied the correct way either when applied to a method or to a class.

### OnExceptionAspect ###

This method was applied the correct way too.

### Postshrp Diagnostic ###

The things that I tested were logging with NLog plug-in and it worked fine.

### Conclusion ###

I thing that my test in incomplete BUT at least it has some point in favor and I show that Postsharp, even if Mono is not supported, we can use it. It is a shame that Multicast does not work :(

> You can find the code [here](https://github.com/Rafailong/MonoAndPostsharp)
