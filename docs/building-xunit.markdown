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

Using your Git client of choice, do a clone of <https://github.com/xunit/xunit.git>. When cloning, ensure the client automatically checks out Git submodules (from the command line, add the `--recurse-submodules` switch).

If you want help understanding and using Git, please see the [Pro Git](http://learn.github.com/p/intro.html) e-book.

## Open Visual Studio solution

The core project ([https://github.com/xunit/xunit](https://github.com/xunit/xunit)) requires the following things installed:

* [.NET Core 1.0 w/ VS2015 Tooling Preview 2](https://www.microsoft.com/net/core#windows) (or later) 
* [Visual Studio 2015](https://www.visualstudio.com/downloads/) w/ Update 3 (or later), with the following options enabled:
  * Programming Languages &gt; Visual F#
  * Windows and Web Development &gt; Microsoft Web Developer Tools

Other projects may require other additional features (like Windows 10 SDK 10.0.10240, Windows Phone 8.1 SDK, and Xamarin).

You should be able to immediately build the solution, as all external dependencies are automatically retrieved with
[NuGet Package Restore](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages). If you want to
run the unit tests from within Visual Studio, we strongly recommend you use [TestDriven.net](http://www.testdriven.net/).

## Build and run the tests from the command

For the purposes of demonstration, we will assume that you checked out the source code to `C:\xUnit`.

* Open a PowerShell command prompt (`Start` -> `Run` -> `powershell.exe`)
* Change to the directory with the source code: `cd C:\xUnit`
* Type the following command to build and run the tests: `.\build`
* Ensure there are no errors at the end of the build process.

_If you have problems building the assertion library, you may have forgotten to update the submodules. From the command line, run `git submodule update --init`._
