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


A *PlayReady Trusted Clock* is a general term for a clock that is used to enforce time-based limitations set to PlayReady protected content on PlayReady clients. Any client that implements a trusted clock ensures that the client that restricts playback to a beginning date and time, an expiration date and time, or expiration date and time after first play cannot be tampered with using hacking tools to a level defined in the [Robustness Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/)

Microsoft does not require client developers to use a trusted clock. However, clients without a trusted clock won't be allowed to manage license with time based policies, including expiration. Because this scenario is very common in the industry (like rental or subscription), Microsoft does recommend implemeting a secure clock in every client.

Client developers can choose amongst two types of PlayReady Trusted Clocks in their design. They both allow manage licenses with time-based policies:
1. *PlayReady Secure Clock*
2. *PlayReady Anti-rollback Clock*


## PlayReady Secure Clock
A *PlayReady Secure Clock* is "a hardware real-time clock that has been designed to resist unauthorized access at the level defined in the Robustness Rules", as defined in the [Defined Terms document for the Compliance and Robutness Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/) 

![PlayReady Secure Clock](../images/secure_clock.png)


## PlayReady Anti-rollback Clock
A *PlayReady Anti-rollback Clock* is "a real-time clock that is periodically verified by the PlayReady Final Product to have advanced", as defined in the [Defined Terms document for the Compliance and Robutness Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/) 

![PlayReady Anti-rollback Clock](../images/anti_rollback_clock.png)
