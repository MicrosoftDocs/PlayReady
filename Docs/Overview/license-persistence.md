---
author: rolandlefranc
title: Persistent and Non-persistent Licenses
description: License servers built using PlayReady Server SDK issue licenses to clients.
ms.assetid: "3da1f73f-e8a0-aa6a-a9cf-24a74226311b"
kindex: license, generation and issuance
kindex: generating, licenses
kindex: issuing, licenses
keywords:  about generation and issuance license,  license generation and issuance about
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# License Persistence


License servers built using PlayReady Server SDK issue licenses to clients. These licenses contain policy information for the content with which they are associated. Licenses may be issued over any transport, but typically licenses are issued over the Web.


PlayReady licenses can be:

   *  Persistent

      Persistent licenses are stored in non-volatile memory (for example, in the local license store on a hard drive or in a NAND memory) and last for the lifetime of the store or until a time-based restriction is reached. Generally, persistent licenses can either be used immediately or can be stored to be used in the future, and can be used to play back content for the life of the license. In addition, persistent licenses can be used to play back downloaded content while the device is offline.

   *  Non-persistent

      Non-persistent licenses are stored in volatile memory and only last for as long as the current session. Generally, non-persistent licenses are used for immediate playback of content and will require another license when playback begins again. Non-persistent licenses are also known as in-memory licenses, or in-memory-only licenses.



Both persistent and non-persistent licenses include rights and right restrictions set by the issuing service. These rights, such as Play, and rights restrictions, such as date/time expiration, begin time, expiration after first play, and so on, are described in detail in the *Microsoft PlayReady Extensible Media Rights Specification*, which is contained in the PlayReady documentation provided to licensees.
