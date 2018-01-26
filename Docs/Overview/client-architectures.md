---
author:
title: PlayReady Client Architectures
description: This topic provides a brief description on the different ways to implement a DRM client in a device and how to develop applications using DRM.
ms.assetid: "B58235E5-3E78-44CA-8BDE-22961773DDF4"
kindex: clients, architecture
kindex: PlayReady, client architecture
keywords: client, architecture, options
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Client Architectures


This topic provides a brief description on the different ways to implement a DRM client in a device and how to develop applications using DRM. This topic also gives details of the overall PlayReady Device Porting Kit structure.

A PlayReady client can be either a device or an application that receives content for playback. The PlayReady Device Porting Kit is intended for original equipment manufactures (OEMs) who are developing devices (such as physical hardware or operating systems), and for application developers who are integrating their applications in a device.

The following figure shows the client implementation options available using PlayReady.

![PlayReady Client Options](../images/client_options.png)

A device that embeds a DRM client (by using the Content Decryption Module (CDM)), exposes an API to applications that have different forms. Some of these forms are:

   *  On Windows 10 UWP, the **Windows.Media.Protection.PlayReady** namespace is available in C#, JavaScript, and C++. See [Windows.​Media.​Protection.​Play​Ready Namespace](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Protection.PlayReady) for more information.

      *  For more information on using PlayReady for Windows 10, see [PlayReady DRM](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk).

      *  For more information on using PlayReady for Windows 8, see [Developing PlayReady Windows 8.1 Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx).

   *  On HTML5, the [Encrypted Media Extensions (EME)](http://www.w3.org/TR/encrypted-media/).

   *  On Android, the [**DrmManagerClient** class](https://developer.android.com/reference/android/drm/DrmManagerClient.html). See the [PlayReady DRM Plugin for Android Microsoft Specification](../Specifications/playready-drm-plugin-for-android-specification.md) for more information.

There is another possible deployment model&mdash;developing the porting kit in the application. How you do this is entirely up to you (that is, whether you develop it yourself, or use an SDK supplied by a [PlayReady Partner](https://www.microsoft.com/playready/partners/), and will not be discussed in this document.

The following table shows the current availability and percentage of units that ship PlayReady in non-Windows clients.

<table>
  <tr>
    <th></th>
    <th>Embedded in the device</th>
    <th>In the application</th>
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










