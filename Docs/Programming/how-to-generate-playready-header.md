---
author: rolandlefranc
title: How to generate a PlayReady Header
description: This page describes how to generate a PlayReady Header in order to encrypt or package audio video content
ms.assetid: "D2F152D4-D0EC-4B32-9A50-A296670F4563"
keywords: PlayReady Header, PlayReady Object, Programming Guide
ms.author: rolefran
ms.date: 04/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# How to generate a PlayReady Header

The packager needs to include a PlayReady Header in the encrypted content.

For a detailed description of the PlayReady Header and the PlayReady Object, see the [PlayReady Header Specification](../Specifications/playready-header-specification.md).

The PlayReady Header contains information about the content being played back, including the key identifiers (KIDs) that identify the keys used to encrypt the data, the default license acquisition URL of the PlayReady License Server, and any custom data that you want to include. The key and KID used to encrypt the content must be shared with the PlayReady License Server that will be issuing the licenses for that specific content, typically through a Key Management System (KMS).

>[!NOTE]
>Microsoft does not provide a Key Management System with PlayReady.

Here is an example of a PlayReady Header, which may be inserted in the header of a fragmented MP4 file, typically for On-Demand content:

```xml
<WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.3.0.0">
  <DATA>
    <PROTECTINFO>
      <KIDS>
        <KID ALGID="AESCTR" VALUE="PV1LM/VEVk+kEOB8qqcWDg=="></KID>
        <KID ALGID="AESCTR" VALUE="tuhDoKUN7EyxDPtMRNmhyA=="></KID>
      </KIDS>
    </PROTECTINFO>
    <LA_URL>http://rm.contoso.com/rightsmanager.asmx</LA_URL>
    <DS_ID>AH+03juKbUGbHl1V/QIwRA==</DS_ID>
  </DATA>
</WRMHEADER>
```

Here is an example of a PlayReady Header, for Live Linear content:

```xml
To do
<WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.3.0.0">
</WRMHEADER>
```

## Method 1 - Build your own code based on spec

To do

## Method 2 - Use a Windows app

To do


## Method 3 - Use a PK based app

To do
