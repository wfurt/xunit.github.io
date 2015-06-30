---
layout: default
title: Getting Test Results in TeamCity
breadcrumb: Documentation
---
# Getting Test Results in TeamCity

xUnit.net 1.1 added support for [JetBrains' TeamCity](https://www.jetbrains.com/teamcity/). This support is automatically enabled, and requires no end-user configuration.

You must use an external build runner (like MSBuild) when building your project in TeamCity, so that you can add calls to the MSBuild task, the Console runner, or the DNX runner. You cannot use TeamCity's SLN builder, because your SLN file does not have any references to running xUnit.net (and TeamCity does not understand xUnit.net tests natively).

The runners in xUnit.net detect TeamCity is running through environment variables (specifically, it looks for `TEAMCITY_PROJECT_NAME`). If for some reason your build environment does not pass the TeamCity environment variables through to the runner, you can force TeamCity mode manually; on the console or DNX runner, add the `-teamcity` switch; on the MSBuild runner, add the property `Reporter="teamcity"` to your `<xunit>` task.

*For more information on using the Console runner, see [Getting Started](getting-started.html).*<br>
*For more information on using the DNX runner, see [Getting Started with DNX](getting-started-dnx.html).*<br>
*For more information on using MSBuild, see [Running xUnit.net Tests in MSBuild](how-to-use-msbuild.html).*
