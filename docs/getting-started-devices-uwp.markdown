---
layout: default
title: Getting started with Devices: Universal Windows Platform
breadcrumb: Documentation
---
# Getting started with Devices: Universal Windows Platform

1. File -> New Project and create a Blank UWP project:
![](../images/getting-started-devices-uwp/CreateProject.png){: .border }
2. Add the `xunit.runner.devices` package. If you want unit tests in this project, also add `xunit`:
![](../images/getting-started-devices-uwp/AddPackages.png){: .border }
3. Replace App.xaml and App.xaml.cs with the following (using your namespace in `x:Class`):
	* **App.xaml**
{% highlight xml %}
<ui:RunnerApplication
    x:Class="UwpTestRunner.App"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:ui="using:Xunit.Runners.UI"
    RequestedTheme="Light">
</ui:RunnerApplication>
{% endhighlight %} 
	![](../images/getting-started-devices-uwp/App.xaml.png){: .border }
	* **App.xaml.cs**
{% highlight C# %}
using System.Reflection;
using Xunit.Runners.UI;
namespace UwpTestRunner
{
    sealed partial class App : RunnerApplication
    {
        protected override void OnInitializeRunner()
        {
            // tests can be inside the main assembly
            AddTestAssembly(GetType().GetTypeInfo().Assembly);
            // otherwise you need to ensure that the test assemblies will 
            // become part of the app bundle
            // AddTestAssembly(typeof(PortableTests).GetTypeInfo().Assembly);
        }
    }
}
{% endhighlight %} 
	![](../images/getting-started-devices-uwp/App.xaml.cs.png){: .border }
4. Delete `MainPage.xaml` and `MainPage.xaml.cs`
![](../images/getting-started-devices-uwp/DeleteMainPage.png){: .border }
5. Add your unit tests:
![](../images/getting-started-devices-uwp/AddTests.png){: .border }
6. (optional) If your tests are in other assemblies, add a project reference and modify the `App.xaml.cs` to include the assembly containing your tests