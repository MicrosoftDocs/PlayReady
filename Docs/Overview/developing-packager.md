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

If you are developing an encoder utilizing PlayReady technologies, you will need to include a PlayReady Header in the encrypted content. The PlayReady Header contains information about the content being played back, including the key identifiers (KIDs) that identify the keys used to encrypt the data, the default license acquisition URL of the PlayReady license server, and any custom data that you want to include. The key and KID used to encrypt the content must be shared with the PlayReady license server that will be issuing the licenses for that specific content, typically through a Key Management System.

For more information about encrypting content and generating the PlayReady Header, see [Content Encryption and Delivery](content-encryption-and-delivery.md) and the [PlayReady Header Object Specification](../Specifications/playready-header-specification.md).

>[!NOTE]
>Microsoft does not provide a Key Management System with PlayReady.
