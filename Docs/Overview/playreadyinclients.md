---
author: 
title: "PlayReady in Clients"
description: ""
ms.assetid: "B58235E5-3E78-44CA-8BDE-22961773DDF4"
kindex: clients, PlayReady in
kindex: PlayReady, in clients
keywords: clients, OEM, developers
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady in Clients
   
  
This topic provides a brief description the different ways to implement a DRM client in a device, how to develop applications using DRM, and gives details of the overall PlayReady Device Porting Kit structure.

A PlayReady client can be either a device or an application that receives content for playback. The PlayReady Device Porting Kit is intended for original equipment manufactures (OEMs) who are developing devices (such as physical hardware or operating systems), and for application developers who are integrating their applications in a device. 

The following figure shows the client implementation options available using PlayReady.

![PlayReady Client Options](../images/client_options.png)

A device that is embedding a DRM client (using the Content Decryption Module (CDM)) exposes an API to applications that has different forms. Some of these forms are:

   *  On Windows 10 UWP, the **Windows.Media.Protection.PlayReady** namespace is available in C#, JavaScript, and C++. See [Windows.​Media.​Protection.​Play​Ready Namespace](https://docs.microsoft.com/en-us/uwp/api/Windows.Media.Protection.PlayReady) for more information.
   
      *  For more information on using PlayReady for Windows 10, see [PlayReady DRM](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk).
      
      *  For more information on using PlayReady for Windows 8, see [Developing PlayReady Windows 8.1 Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx).

   *  On HTML5, the [Encrypted Media Extensions (EME)](http://www.w3.org/TR/encrypted-media/).
   
   *  On Android, the [**DrmManagerClient** class](https://developer.android.com/reference/android/drm/DrmManagerClient.html). See the [PlayReady DRM Plugin for Android Microsoft Specification](../Specifications/PlayReady_DRM_Plugin_for_Android/playreadydrmpluginforandroidspecification.md) for more information.
   
There is another possible deployment model&mdash;developing the porting kit in the application. How you do this is entirely up to you (that is, whether you develop it yourself, or use an SDK supplied by a [PlayReady Partner](https://www.microsoft.com/playready/partners/), and will not be discussed in this document. 

The following table shows the current availability and percentage of units shipping of PlayReady in non-Windows clients.

<table>
  <tr>
    <th></th>
    <th>In the hardware</th>
    <th>In the OS</th>
    <th>In the application</th>
  </tr>
  <tr>
    <td>MacOS</td>
    <td></td>
    <td></td>
    <td>Silverlight and 3rd parth SDKs</td>
  </tr>
  <tr>
    <td>iOS</td>
    <td></td>
    <td></td>
    <td>1st and 3rd party SDKs</td>
  </tr>
  <tr>
    <td>Apple TV OS</td>
    <td></td>
    <td></td>
    <td>3rd party SDKs</td>
  </tr>
  <tr>
    <td>Chrome OS</td>
    <td></td>
    <td></td>
    <td></td>
  </tr>
  <tr>
    <td>Android Mobile</td>
    <td colspan="2" align="center">Some OEMs (42% units)</td>
    <td>3rd party SDKs</td>
  </tr>
  <tr>
    <td>Android TV</td>
    <td colspan="2" align="center">All OEMs (100% units)</td>
    <td></td>
  </tr>
  <tr>
    <td>Linux TVs</td>
    <td colspan="2" align="center">Most OEMs (80% units)</td>
    <td></td>
  </tr>
  <tr>
    <td>Consoles</td>
    <td colspan="2" align="center">PlayStations and Xbox (87% units)</td>
    <td></td>
  </tr>
  <tr>
    <td >Network Receivers</td>
    <td colspan="2" align="center">Most OEMs (95% units)</td>
    <td></td>
  </tr>
  <tr>
    <td>Blu Ray Disc Players</td>
    <td colspan="2" align="center">Most OEMs (80% units)</td>
    <td></td>
  </tr>
</table>










