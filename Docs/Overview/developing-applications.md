---
author: rolandlefranc
title: Developing Applications using PlayReady
description: This topic provides a description of the different ways to develop applications using PlayReady DRM.
ms.assetid: "B58235E5-3E78-44CA-8BDE-22961773DDF4"
keywords: client, application, development, uwp, android, xbox, sdk
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Developing Applications using PlayReady

## Devices including a PlayReady Client embedded by the OEM

A lot of OEMs have licensed the PlayReady Porting Kit, integrated it in their devices, and made it available to application developers as part of their SDK.

![PlayReady Client Embedded in Device](../images/client_level_os_soc.png)


For example, Microsoft ensures all Windows 10 devices include a PlayReady client integrated in the Windows OS itself, or in the chip's firmware of the device (TEE), and exposes it through UWP APIs to application developers, but also Android TV device makers do the same.

Such devices include Windows devices using the UWP API, Andoid device using the Java DrmManagerClient API, Linux devices using various interfaces, and embedded web browsers using Javascript EME API.

![PlayReady Client APIs on devices](../images/client_apis.png)

On these devices, application developers do not need to license PlayReady, or manipulate PlayReady code or certificate. They just use the SDK provided by the OEM on the platform and run PlayReady operations from within their app, like AcquireLicense(KID), etc.


The following table shows the current availability of a PlayReady client on various devices.

<table>
  <tr>
    <th></th>
    <th>Embedded in the device</th>
    <th>In the application</th>
  </tr>
  <tr>
    <td>Windows 10</td>
    <td>Yes. Windows SDK. UWP or Web app in Edge</td>
    <td></td>
  </tr>
  <tr>
    <td>Windows 8, 8.1</td>
    <td>Yes, Windows SDK</td>
    <td>3rd party SDKs possible</td>
  </tr>
  <tr>
    <td>Windows 7</td>
    <td>Yes, Silverlight</td>
    <td>3rd party SDKs possible</td>
  </tr>
  <tr>
    <td>MacOS</td>
    <td>No</td>
    <td>Silverlight and 3rd party SDKs</td>
  </tr>
  <tr>
    <td>iOS</td>
    <td>No</td>
    <td>1st and 3rd party SDKs</td>
  </tr>
  <tr>
    <td>Apple TV OS</td>
    <td>No</td>
    <td>3rd party SDKs</td>
  </tr>
  <tr>
    <td>Chrome OS</td>
    <td>No</td>
    <td></td>
  </tr>
  <tr>
    <td>Android Mobile</td>
    <td>Yes on some models</td>
    <td>3rd party SDKs</td>
  </tr>
  <tr>
    <td>Android TV</td>
    <td>Yes on all models</td>
    <td></td>
  </tr>
  <tr>
    <td>Linux TVs</td>
    <td>Yes on most models</td>
    <td></td>
  </tr>
  <tr>
    <td>Consoles</td>
    <td>Yes on PlayStations and Xbox</td>
    <td></td>
  </tr>
  <tr>
    <td >Network Receivers</td>
    <td>Yes on most models</td>
    <td></td>
  </tr>
  <tr>
    <td>Blu Ray Disc Players</td>
    <td>Yes on most models</td>
    <td></td>
  </tr>
</table>

## Devices **not** including a PlayReady Client

Some OEMs have made the choice to not embed a PlayReady client in their device, or to embed it but not make it available to application developers through their SDK.

On these devices, applicatio developers can still run PlayReady operations from within their app, but they need to integrate the PlayReady Client in their application, including PlayReady code and certificates.

The integration of a PlayReady Client in the application requires the application developer to license and use the PlayReady Porting Kit.


## Developing Applications using PlayReady on Windows, Xbox

Microsoft develops and distributes a PlayReady Client in every Windows 8, 8.1, and 10 unit, and in every Xbox unit. This PlayReady Client is exposed and freely accessible through a high-level API to application developers.

Application developers can create Universal Windows Platform (UWP) applications capable of providing PlayReady content to the user while enforcing the access rules defined by the content provider. An application can freely use this built-in PlayReady Client in Windows 8, 8.1, or 10, without signing any agreement with Microsoft, and without the need of any PlayReady certificate, or any PlayReady fee or royalty due.

Windows 10 PlayReady documentation can be found at [PlayReady for Windows 10](https://msdn.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk). Samples of PlayReady Windows 10 applications can be found as part of the [UWP Samples collection](https://github.com/Microsoft/Windows-universal-samples) and at [PlayReady sample Universal Windows Apps for Windows 10 (Javascript/C#/EME)](https://code.msdn.microsoft.com/windowsapps/PlayReady-samples-for-124a3738).

You can also create PlayReady Windows Store and Web applications for Windows 8.1. Windows 8.1 PlayReady documentation can be found at [Developing PlayReady Windows Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx). Samples of PlayReady Windows 8.1 applications can be found at [PlayReady sample for Windows 8.1 Store apps](https://code.msdn.microsoft.com/windowsapps/PlayReady-sample-for-bb3065e7).

Some PlayReady Partners provide SDKs to run PlayReady on Windows 7 and Mac OS, based on Electron, Xamarin, or other technologies. You can contact these [PlayReady Partners](https://www.microsoft.com/playready/partners) directly for more information.

Silverlight is a deprecated application framework running on Windows 7 and Mac OS that includes a fully functional PlayReady client. It runs in browsers with limitations, and can also run out of browsers to provide standalone apps on Windows 7 and Mac OS.

# Integrating PlayReady in Devices
This topic provides an overview of the different PlayReady Client architectures that are available. A PlayReady client can be either a device or an application that receives content for playback. The PlayReady Device Porting Kit is intended for original equipment manufactures (OEMs) who are developing devices (such as physical hardware or operating systems), and for application developers who are integrating their applications in a device.

The following figure shows the client implementation options available using PlayReady.


A device that embeds a DRM client (by using the Content Decryption Module (CDM)), exposes an API to applications that have different forms. Some of these forms are:

   *  On Windows 10 UWP, the **Windows.Media.Protection.PlayReady** namespace is available in C#, JavaScript, and C++. See [Windows.​Media.​Protection.​Play​Ready Namespace](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Protection.PlayReady) for more information.

      *  For more information on using PlayReady for Windows 10, see [PlayReady DRM](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk).

      *  For more information on using PlayReady for Windows 8, see [Developing PlayReady Windows 8.1 Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx).

   *  On HTML5, the [Encrypted Media Extensions (EME)](http://www.w3.org/TR/encrypted-media/).

   *  On Android, the [**DrmManagerClient** class](https://developer.android.com/reference/android/drm/DrmManagerClient.html). See the [PlayReady DRM Plugin for Android Microsoft Specification](../Specifications/playready-drm-plugin-for-android-specification.md) for more information.

There is another possible deployment model &mdash; developing the porting kit in the application. How you do this is entirely up to you (that is, whether you develop it yourself, or use an SDK supplied by a [PlayReady Partner](https://www.microsoft.com/playready/partners/)), and will not be discussed in this document.

