---
author: rolandlefranc
title: Developing and Operating a PlayReady Packager
description: Developing and Operating a PlayReady Packager
ms.assetid: "01e7b2ed-2204-9f0c-9d2d-901b4fe5f7c0"
keywords:  PlayReady, Packager, Encryptor
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Developing and Operating a PlayReady Packager

Companies developing an encoder or a packager (also known as encryptor) utilizing PlayReady technologies need to integrate two functionalities in their product:

1. A functionality that encrypt content in a PlayReady compatible encryption format.

2. A functionality that generates a PlayReady Header and inserts it in the encrypted content

>[!NOTE]
> A PlayReady licensing agreement is not necessary to build a PlayReady encoder or packager. In addition, there is no royalty applicable to PlayReady encoders or packagers.

## Content Encryption

Any encryption format that uses AES-128 keys used in CTR mode or CBC mode is allowed. Microsoft recommends using Common Encryption: CENC or CBCS.

For more information, see [Content Encryption and Delivery](content-encryption-and-delivery.md)


## PlayReady Header generation

The packager needs to include a PlayReady Header in the encrypted content.

The PlayReady Header contains information about the content being played back, including the key identifiers (KIDs) that identify the keys used to encrypt the data, the default license acquisition URL of the PlayReady license server, and any custom data that you want to include. The key and KID used to encrypt the content must be shared with the PlayReady license server that will be issuing the licenses for that specific content, typically through a Key Management System (KMS).

>[!NOTE]
>Microsoft does not provide a Key Management System with PlayReady.

Here is an example of a PlayReady Header, which may be inserted in the header of a fragmented MP4 file:

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


For more information about generating the PlayReady Header, see the [PlayReady Header Object Specification](../Specifications/playready-header-specification.md).

