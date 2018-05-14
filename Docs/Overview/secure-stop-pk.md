---
author: rolandlefranc
title: PlayReady Secure Stop
description: PlayReady Secure Stop is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content.
ms.assetid: "9736c55e-3628-4d93-8d55-48d4be6af137"
keywords: secure, stop, server, license
ms.author: rolefran
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Secure Stop


Introduced in PlayReady version 3.0, *PlayReady Secure Stop* is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.

A Secure Stop event is reported to a Secure Stop Server by the client when media playback stops, either at the end of the media or because the user stopped the media presentation somewhere in the middle. A Secure Stop is also reported when the previous session ends unexpectedly (for example, due to a system or application crash).

> [!NOTE]
> Secure Stop applies only to non-persistent licenses.

## Secure Stop 2

In PlayReady version 4.2, *PlayReady Secure Stop 2* provides more security by adding a SecureStopAESKey, generated with a new license. That key is used during the SecureStop challenge to stop the playback session in the TEE, and the server checks for signatures upon regeneration of the key.


There are two primary scenarios for sending a Secure Stop challenge:

   *  When the media playback stops either at the end, or because the user stopped the media presentation somewhere in the middle.
   *  When the previous session ends unexpectedly (for example, due to a system or app crash). The app will need to query, either at startup or shutdown, for any outstanding Secure Stop sessions and send challenge(s) separate from any other media playback.

![](../images/securestop.gif)