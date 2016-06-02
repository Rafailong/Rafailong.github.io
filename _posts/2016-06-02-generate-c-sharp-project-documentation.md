---
layout: post
title: Generate C# project documentation
---

![document all the things](http://s3.ryanparman.com.s3.amazonaws.com/rage/document_all_the_things.png)

Hi there, this time I will show you the process and things I do to generate the documentation of my C# project (yes, only C# because I have not test it with VB).

- First of all We select the project that We want to generate its documentations then right click on it so We can navigate to its properties.
- Then, We are going to check XML Documentation file checkbox and change the name of the generated file to the name of the project (this rename will easy the things later)
- Now, save the changes and change to Build Event tab where We will add a post build event that will be run on successful build.
- The post build event or command that We are going to add only copy the generated XML file and de DLL to a folder that is located at the same level as out sln file.

```
copy /Y "$(TargetDir)$(ProjectName).XML" "$(SolutionDir)docs\$(ProjectName).XML"
copy /Y "$(TargetPath)" "$(SolutionDir)docs\$(ProjectName).dll"
```

- Until now We have made the hardest part of the configuration, now We are going to download a grate tool that will generate the documentation, [ImmDoc.NET](https://github.com/marek-stoj/ImmDoc.NET)


<iframe src="https://app.box.com/embed_widget/s/426q5tgz5zog12trbh9o?view=list&sort=name&direction=ASC&theme=gray" width="800" height="550" frameborder="0" allowfullscreen webkitallowfullscreen msallowfullscreen>
</iframe>

We now have all in place to generate the documentation. Now using ImmDoc.NET through the command line lets navigate to the folder where the XML and DLL where copied after a VS build. Once We are there lets run the command to generate the docs.

```
ImmDocNet.exe -ForceDelete -IncludeInternalMembers -IncludePrivateMembers
```

You can get help from ImmDoc.NET with

```
ImmDocNet.exe -h
```

That's all!

Happy Coding :-) !!!
