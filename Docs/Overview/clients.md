---
author: rolandlefranc
title: PlayReady Clients
description: PlayReady Clients may be embedded in a device and used by an application, or be embedded in the application itself
ms.assetid: "83200B8C-6C24-4ACE-95D6-28C1C5B3C412"
keywords: clients, playready
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Clients
This topic provides a description of the different ways to implement a PlayReady Client in a device or in an application. Regarding application development, there are two cases depending on whether the device embeds a PlayReady Client exposed to applications through an API or not:
- if the device embeds a PlayReady Client in the OS or in the SOC and makes it available to application developers, then application development is simpler and cheaper. This is the Windows 10 or Android TV case.
- if the device does not embed a PlayReady Client in the OS or in the SOC or does not make it available to application developers, then the application must include the PlayReady Client itself. This is the iOS case.

<br/>

![PlayReady Client Options on devices](../images/client_level_app_os_soc.png)

<br/>
<br/>

## In this section

[Developing Applications using PlayReady](developing-applications.md)

[Integrating PlayReady in Devices](integrating-in-devices.md)

[PlayReady Initialization](initialization.md) 

[PlayReady Revocation](revocation.md) 
