---
author: 
title: "License Generation and Issuance"
description: ""
ms.assetid: "3da1f73f-e8a0-aa6a-a9cf-24a74226311b"
kindex: license, generation and issuance
kindex: generating, licenses
kindex: issuing, licenses
keywords:  about generation and issuance license,  license generation and issuance about
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# License Generation and Issuance
   
  
License servers built using PlayReady Server SDK issue licenses to clients. These licenses contain policy information for the content with which they are associated. Licenses may be issued over any transport, but typically licenses are issued over the Web.  
   
  
PlayReady licenses can be:  
 
   *  Persistent

      Persistent licenses are stored in non-volatile memory (for example, in the local license store) and last for the lifetime of the store or until a time-based restriction is reached. Generally, persistent licenses can either be used immediately or can be stored to be used in the future, and can be used to play back content for the life of the license. In addition, persistent licenses can be used to play back downloaded content while the device is offline.
  
   *  Non-persistent

      Non-persistent licenses are stored in volatile memory and only last for as long as the current session. Generally, non-persistent licenses are used for immediate playback of content and will require another license when playback begins again.  

   
  
Both persistent and non-persistent licenses include rights and right restrictions set by the issuing service. These rights, such as Play, and rights restrictions, such as date/time expiration, begin time, expiration after first play, and so on, are described in detail in the Microsoft PlayReady Extensible Media Rights Specification, which is contained in the PlayReady documentation provided to licensees.   

> [!NOTE]   
> For content that was purchased to own, users expect the content to play indefinitely on their devices. Services would most likely issue licenses for this content with no expiration at all. However, because users change devices frequently, and because each device may change its PlayReady identity some time (when a re-individualization is run, or when a device is completely reinstalled), services should be ready at any time to re-issue licenses for purchased content that was previously delivered to a user or a device.  
 
