---
layout: default
title: Getting the source and building xUnit.net
breadcrumb: Documentation
---
# Getting the source and building xUnit.net

## Get a Git Client

Download a Git client, such as:

* [TortoiseGit](http://code.google.com/p/tortoisegit/downloads/list)
* [Github for Windows](http://windows.github.com/)
* [Command line client](http://code.google.com/p/msysgit/downloads/list)

## Get the xUnit.net source code

Using your Git client of choice, do a clone of <https://github.com/xunit/xunit.git>.

If you want help understanding and using Git, please see the [Pro Git](http://learn.github.com/p/intro.html) e-book.

## Open Visual Studio solution

xUnit.net's source code currently requires Visual Studio 2015. It uses several optional features of Visual Studio,
including Windows 8, Windows 8.1, Windows Phone 8, and Windows Phone Application 8.1 support. It also uses Xamarin
to target Android and iOS.

If you have Xamarin installed, open `xunit.vs2015.sln`; if you do not have Xamarin, open `xunit.vs2015.NoXamarin.sln`.
You should be able to immediately build the solution, as all external dependencies are automatically retrieved with
[NuGet Package Restore](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages). If you want to
run the unit tests from within Visual Studio, we strongly recommend you use [TestDriven.net](http://www.testdriven.net/).

## Build and run the tests from the command

For the purposes of demonstration, we will assume that you checked out the source code to `C:\xUnit`.

* Open a PowerShell command prompt (`Start` -> `Run` -> `powershell.exe`)
* Change to the directory with the source code: `cd C:\xUnit`
* Type the following command to build and run the tests: `.\build` (or `.\build -noXamarin`)
* Ensure there are no errors at the end of the build process.
