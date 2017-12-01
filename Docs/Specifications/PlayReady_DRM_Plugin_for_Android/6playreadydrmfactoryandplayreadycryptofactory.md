---
author: 
title: "6. PlayReadyDrmFactory and PlayReadyCryptoFactory"
description: ""
ms.assetid: "c5da4625-2d68-9e42-24a2-e079e5107e90"
kindex: PlayReadyDrmFactory
kindex: PlayReadyCryptoFactory
keywords: PlayReadyDrmFactory, PlayReadyCryptoFactory
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# 6. PlayReadyDrmFactory and PlayReadyCryptoFactory
   
  
Implementation of the **PlayReadyDrmFactory** and **PlayReadyCryptoFactory** interfaces are required for creating instances of both [PlayReadyDrmPlugin](4playreadydrmplugin.md) and [PlayReadyCryptoPlugin](5playreadycryptoplugin.md) respectively.   
   
  
Both factory classes must indicate to callers that they support creating objects that can consume PlayReady protected content by properly implementing the **isCryptoSchemeSupported** API.   
   
```cpp

const uint8_t playready_uuid[16] =
    {0x79, 0xf0, 0x04, 0x9a, 0x40, 0x98, 0x86, 0x42, 0xab, 0x92, 0xe6, 0x5b, 0xe0, 0x88, 0x5f, 0x95};

bool isCryptoSchemeSupported(const uint8_t uuid[16])
{
  return (!memcmp(uuid, playready_uuid, sizeof(playready_uuid)));
}
    
```
 
