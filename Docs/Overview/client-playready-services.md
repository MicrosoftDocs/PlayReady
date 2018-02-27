---
author: rolandlefranc
title: "OEM or App Vendor Services for PlayReady Clients"
description: OEMs optionally design, develop and operate services that allow PlayReady clients to run, including remote provisioning services
ms.assetid: "8C7CED2A-C02F-4866-89AD-5B4DD2E6CA09"
keywords: soap, PlayReady protocols, PlayReady communication
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# OEM or App Vendor Services for PlayReady Clients


OEMs or App Vendors releasing PlayReady Clients may design their device or application so as to contact a service when they perform PlayReady operations. A very common scenario is the remote provisioning service, which delivers a unique Client Certificate to a client the first time it performs a PlayReady operation.

These services are specific to the client, owned by the device maker or app developer, and use ad-hoc protocols.

Microsoft operates some of these services for the clients that it owns, including Windows 10, Windows 8.1, Xbox, Silverlight.