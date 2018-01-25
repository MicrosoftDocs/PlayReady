---
author:
title: PlayReady Secure Stop
description: PlayReady Secure Stop is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content.
ms.assetid: "A269D7DC-57B8-4B78-A91E-1DD9707FA6FE"
kindex: license, Secure Stop
kindex: processing, Secure Stop
kindex: stop, secure
keywords: Secure Delete, Secure Delete license
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Secure Stop Server


Introduced in PlayReady version 3.0, *PlayReady Secure Stop* is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.

A secure stop is reported to a secure stop server by the client when media playback stops, either at the end of the media or because the user stopped the media presentation somewhere in the middle. A secure stop is also reported when the previous session ends unexpectedly (for example, due to a system or application crash).
