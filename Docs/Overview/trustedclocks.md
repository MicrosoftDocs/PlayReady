---
author:
title: "Trusted Clocks"
description: ""
ms.assetid: "5ab667e2-7eb9-df4c-798e-ee3a4b9106a2"
kindex: clock, about trusted
kindex: about, trusted clocks
kindex: secure clock, about
kindex: anti-rollback clock, about
kindex: clock, about anti-rollback
kindex: clock, about secure
kindex: about, secure clock
kindex: about, anti-rollback clock
keywords:  about trusted clock,  trusted clocks about,  about secure clock,  about anti-rollback clock,  about anti-rollback clock,  about secure clock,  secure clock about,  anti-rollback clock about
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Trusted Clocks


A *trusted clock* is a general term for a clock that is used to enforce time-based limitations on PlayReady protected content. Any client that implements a trusted clock ensures that the client that restricts playback to a beginning date and time, an expiration date and time, or expiration date and time after first play cannot be tampered with using hacking tools to a level defined in the PlayReady robustness rules. 

Microsoft does not require client developers to use a trusted clock. However, Microsoft does recommend using a secure clock  as most real content delivery scenarios involve some sort of time restriction in the rights delivered in a license, like rental or subscription.