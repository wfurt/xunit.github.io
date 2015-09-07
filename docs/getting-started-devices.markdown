---
layout: default
title: Getting started with Devices
breadcrumb: Documentation
---
# Getting started with Devices

If you want to run your xUnit tests on a supported device, then the device runners are the way to do it. Running unit tests on a device is the surest way to ensure correct behavior, after things like Ahead of Time (AOT) compilation, .NET Native or other device-specific transformations happen. There's simply no substitute for running "on the metal."

## The general pattern
xUnit for Devices projects all follow a similar approach: create a new blank application to host the runner, add `xunit.runner.devices` and tell it which assemblies contain your unit tests. The unit tests may live directly within the application you created or in other referenced libraries, including PCLs.

## Supported devices
xUnit for Devices supports the following platforms. Click for a platform-specific getting started guide.
 
* [Universal Windows Platform](/docs/getting-started-devices-uwp.html) ( Desktop, Mobile, Tablet, IoT, etc)
* Windows 8.1
* Windows Phone 8.1
* Windows Phone Silverlight 8.0
* Xamarin.Android
* Xamarin.iOS Classic* 
* Xamarin.iOS Unified

*Xamarin.iOS Classic is deprected and won't be supported after xUnit for Devices 1.2.





