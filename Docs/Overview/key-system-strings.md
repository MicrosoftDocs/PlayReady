---
title: PlayReady Encrypted Media Extensions Key System Strings
description: Describes the Key System Strings to use for Encrypted Media Extensions
ms.assetid: "e982455f-96d2-4e2b-8084-ac3b4d0ea54c"
keywords: clients, playready, initialization, EME, keysystem
ms.date: 10/28/2022
ms.topic: conceptual
---

# PlayReady Encrypted Media Extensions Key System Strings

Support for Encrypted Media Extensions (EME) Key System Strings varies based on client and version.

The following table shows the key system string availability and support for each PlayReady client and version.

&nbsp;
>[!div class="mx-tdBreakAll"]
>| Key System String | Microsoft Edge | Porting Kit |
>|:--- |:---|:---|
>| com.microsoft.playready.recommendation | - Supported.<br/>- Security Level 2000.<br/>- Best effort compliance with latest EME specification. | - Supported in PK 3.3 and higher.<br/>- Security Level depends on OEM device.<br/>- Best effort compliance with latest EME specification as of PK version's release date. |
>| com.microsoft.playready.recommendation.3000 | - Supported on devices with required hardware.<br/>- Security Level 3000.<br/>- Best effort compliance with latest EME specification. | - Not supported. |
>| com.microsoft.playready | - Deprecated.<br/>- Will be removed in a future release.<br/>- Non-compliant with any version of the EME specifification. | - Supported in PK 3.2.<br/>- Deprecated in PK 3.3-4.2.<br/>- Not supported in PK 4.3 or higher.<br/>- All versions only compliant with EME specification circa 2017.<br/>- Security Level depends on OEM device. |

