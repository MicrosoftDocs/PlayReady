---
author: rolandlefranc
title: "OEM or App Vendor Services for PlayReady Clients"
description: ""
ms.assetid: "27BE5F0E-C171-4091-BACE-A029C6FE53B5"
keywords: soap, PlayReady protocols, PlayReady communication
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# OEM or App Vendor Services for PlayReady Clients


OEMs or App Vendors releasing PlayReady Clients may design their device or application so as to contact a service when they perform PlayReady operations. A very common scenario is the remote provisioning service, which delivers a unique Client Certificate to a Client the first time it performs a PlayReady operation.

These services are specific to the Client, owned by the device maker or app developer, and use ad-hoc protocols.

Microsoft operates some of these services for the Clients that it owns, including Windows 10, Windows 8.1, Xbox, Silverlight.