---
author: dougklopfenstein
title: Preparing a Packager for PlayReady
description: Discusses the requirements and time required to prepare a packager for PlayReady functionality
ms.assetid: "FE42F0CE-754B-43C4-B661-EF4DC16B0294"
keywords:  PlayReady, packager, encryptor, preparing packager
ms.author: v-doklo
ms.date: 05/11/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Preparing a Packager for PlayReady

There are several considerations you should examine before you begin incorporating PlayReady in your packager to protect content. Note that developing a packager that provides PlayReady protection for content you want to encrypt:

* Does not require a licensing agreement from Microsoft. 

* There are no fees to Microsoft associated with inserting PlayReady in your content.

* There are no royalty payments to Microsoft applicable to PlayReady encoders or packagers.

Therefore, you do not need to allocate any time in your budget for these tasks.

## Development time

The development time for incorporating the PlayReady functionality in your packager will depend on the development and testing of the following components:

* Packager&mdash;packaging the content using the key value supplied by the key generator.

* Key Generator&mdash;generating the key value used to encrypt the content (along with its associated KeyID).

* Key Management System&mdash;storing the key value and its associated KeyId (not required if using the KeySeed mechanism).

* PlayReady Server&mdash;supplying the key value to the client that is requesting content using the KeyID embedded in the PlayReady Header of the encrypted content.

## Development considerations

The basic development considerations for incorporating PlayReady in your packager are:

* A function must be provided to generate the key value and KeyID used to package the content. This functionality is not provided by PlayReady.

* Some means of storing the key values and KeyIDs (a key management system) or a KeySeed mechanism. This functionality is not provided by PlayReady.

* Optional packaging using more than one DRM.

* A method of communicating the key values and KeyIDs to a PlayReady license server.

You will need to allocate time in your budget for these tasks. For more information on development considerations, see [Developing a PlayReady Packager](developing-a-packager.md).

## Additional considerations

The key value and KeyID used to package content using your packager must be supplied to a PlayReady license server, which will then be queried by the client for the key value associated with the KeyID. Depending on how you accomplish this, you will need to budget for the following extra development: 

* If you are using a third-party license server, you will need to allocate in your budget the time and expense of acquiring the rights to use the third-party PlayReady license server.

* If you are planning to use your own PlayReady server, you need to consider the following extra development expenses:

  * You must allocate the time required to request and receive a PlayReady deployment certificate. For more information about the process and timeline for obtaining a PlayReady deployment certificate, see the [PlayReady Licensing Process](http://public.wmlalicensing.com/public/#licensingprocess) web page, and look under the "Agreements *without* Fees/Royalties" heading. (A PlayReady server does not require any fees or royalties.)

  * Any development beyond supplying the key value for the KeyID sent by the client (such as rights and right restrictions) must also be budgetted (which is beyond the scope of this topic).

