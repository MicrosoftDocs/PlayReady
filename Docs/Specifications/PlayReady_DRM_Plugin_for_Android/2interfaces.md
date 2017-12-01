---
author: 
title: "2. Interfaces"
description: ""
ms.assetid: "a735d434-4201-05ca-29a5-a693d721d369"
kindex: interfaces, PlayReady DRM for Android
kindex: PlayReady DRM for Android, interfaces
keywords:  PlayReady DRM for Android interfaces,  interfaces PlayReady DRM for Android
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# 2. Interfaces
   
  
 [PlayReadyDrmPlugin](4playreadydrmplugin.md) provides the implementation for the DRM plug-in interface. **PlayReadyDrmPlugin** is responsible for wrapping the DRM Manager APIs and doing the proper translation for the parameters as specified by the interface into a format that PlayReady can operate on.   

 ![PlayReadyDRMPlugin interface](../../images/DrmPlugin.jpg)   
  
 [PlayReadyCryptoPlugin](5playreadycryptoplugin.md) provides the implementation for the Crypto plug-in interface, which is responsible for decrypting the samples. The OEM must ensure that the decrypted samples never leave the trusted execution environment (TEE).   

 ![PlayReadyCryptoPlugin interface](../../images/CryptoPlugin.jpg) 
