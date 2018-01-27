---
author: rolandlefranc
title: Revocation
description: When Microsoft identifies a client with compromised security, the device may be revoked and added to a revocation list.
ms.assetid: "09869289-666b-272e-1cc2-97079cb71204"
kindex: revocation, about
kindex: about, revocation
keywords: playready revocation,  revocation list
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Revocation


Revocation is a process to identify clients that have compromised security, and prevent those clients from getting access to additional licenses for decrypting content that has been protected.


When Microsoft identifies a client with compromised security, the device may be revoked and added to a revocation list. The revocation list is periodically downloaded by the license servers that issue licenses for protected content. License servers use this revocation list to deny licenses to devices that have been revoked, thereby preventing the device from playing newly protected content.


Revocation lists are refreshed on devices when they are not up to date. The revocation list may also be issued with licenses. The DRM component on the device checks this revocation list before transferring content to other devices. By preventing communication with revoked components, revoked applications no longer work. Once revoked, the only way to fix the situation is to replace the revoked element or remove the revoked component from a newer version of the revocation list.


Microsoft builds and maintains the revocation list and its versioning structure.

