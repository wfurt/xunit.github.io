---
layout: default
title: Getting Test Results in Visual Studio Team Services (VSTS)
breadcrumb: Documentation
---

# Getting Test Results in Visual Studio Team Services (VSTS)

<p class="important">
  <strong>Important note</strong>: These directions are for testing <strong>desktop</strong> unit test assemblies only.
  In particular, these directions will not work for .NET Core.
</p>

## Referencing the Visual Studio test runner

* Using NuGet Package Manager (or Package Manager Console), add `xunit.runner.visualstudio` to at least one of your test projects.  
`install-package xunit.runner.visualstudio`

## Configure VSTS

* Add a build step of type `Visual Studio Test`.

These instructions are written for `Version 1.*` of the `Visual Studio Test` task. You may need to change the version as it defaults to `Version 2.*` or whichever is latest.

### Locate test assemblies

* Under `Execution Options/Test Assembly`, point to your generated test assemblies, e.g. `**\bin\$(BuildConfiguration)\*test*.dll;-:**\xunit.runner.visualstudio.testadapter.dll`.  
(The second part excludes the xUnit test adapter from being considered a test assembly.)

### Enable Code Coverage (optional)

* Select the `Execution Options/Code Coverage Enabled` checkbox.
* Add `/InIsolation` under `Advanced Execution Options/Other console options`.  
(This will supress a warning otherwise generated.)

## Viewing the results

After a successful build, the test results are available on the main view of the build. It should look something like this:

![](../images/getting-test-results-in-vsts/test-results.png)

## Comments

* You no longer need to manually configure the test adapter path, because Nuget restored test adapters are automatically searched for.

* Sometimes you get this error one or many times  
`Warning: System.AppDomainUnloadedException: Attempted to access an unloaded AppDomain. This can happen if the test(s) started a thread but did not stop it. Make sure that all the threads started by the test(s) are stopped before completion.`  
It is not related to VSTS and does not affect the results. For more information, see [xUnit Issue 490](https://github.com/xunit/xunit/issues/490) and [MS Connect](https://connect.microsoft.com/VisualStudio/feedback/details/797525/unexplained-appdomainunloadedexception-when-running-a-unit-test-on-tfs-build-server).
