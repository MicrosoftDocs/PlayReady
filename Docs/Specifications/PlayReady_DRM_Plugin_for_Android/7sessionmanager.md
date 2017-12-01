---
author: 
title: "7. SessionManager"
description: ""
ms.assetid: "f58242d1-78d7-0984-6d75-65187cf16f96"
kindex: SessionManager
keywords: SessionManager
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: playready
---


# 7. SessionManager
   
  
A singleton session manager needs to be implemented to hold the **DRM_APP_CONTEXT** and allow sharing it between the [PlayReadyDrmPlugin](4playreadydrmplugin.md) and [PlayReadyCryptoPlugin](5playreadycryptoplugin.md).   
   
  
Other designs that achieve the same purpose are also acceptable.   
 
| SessionManager| 
| --- | 
| static DRM_APP_CONTEXT soAppContext| 
| static Mutex sLock| 
 
