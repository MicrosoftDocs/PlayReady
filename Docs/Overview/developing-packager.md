---
author: rolandlefranc
title: Developing and Operating a PlayReady Packager
description: Developing and Operating a PlayReady Packager
ms.assetid: "CFAF35FD-CCBE-49EF-B4CE-708FBCDE298A"
keywords:  PlayReady, Packager, Encryptor
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Developing and Operating a PlayReady Packager

Companies developing an encoder or a packager (also known as encryptor) utilizing PlayReady technologies need to integrate two functionalities in their product:

* One that encrypts content in a PlayReady compatible encryption format.

* Another that generates a PlayReady Header and inserts it in the encrypted content.

>[!NOTE]
>A PlayReady licensing agreement is not necessary to build a PlayReady encoder or packager. In addition, there is no royalty applicable to PlayReady encoders or packagers.

## Steps to develop a PlayReady Packager

First of all, you must decide whether to develop your own PlayReady packager or license one from a [PlayReady partner](https://www.microsoft.com/playready/partners/). If you decide to develop your own PlayReady Packager, you will need to decide how you want the packager to work, based on how you want your content stored and delivered. The following list provides the necessary steps required to add PlayReady functionality to your packager.

1. Choose your encryption format. Any encryption format that uses AES-128 keys used in CTR mode or CBC mode is allowed by the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/). For more information, see [PlayReady Content Encryption Modes](content-encryption-modes.md).

2. Choose how you are going to encrypt your content. For more information, see [Using encryption keys](content-encryption-and-delivery.md#using-encryption-keys).

3. Choose whether you want to encrypt your content using only PlayReady, or whether you want to use multiple DRMs. For more information, see [Using encryption tools](content-encryption-and-delivery.md#using-encryption-tools).

4. Choose how you are going to generate and store keys (Key Value and Key ID). 

   Your packager should include some kind of key generator that creates the Key Value used to encrypt and decrypt your content. In addition, the key generator should associate a Key ID to the Key Value. The Key Value remains a secret, and the Key ID is public and is inserted in the PlayReady header in your content.

   You will either need to develop a key management system to store multiple Key Values and their associated Key IDs, or license one from a third party. The key management system could be a database or any other type of storage system, but must be secure to prevent anyone from accessing the key values without authorization. Microsoft does not supply a key management system with PlayReady.

5. Choose how you are going to insert a PlayReady Object (including the PlayReady header) in your encrypted content. For more information, see [How to generate a PlayReady Header](how-to-generate-playready-header.md).

6. Choose how you are going to provide the key values and key IDs to a PlayReady Server, which will then distribute the key values to PlayReady clients. 

    You can create your own PlayReady Server (requires a license from PlayReady&mdash;however no fees or royalties are collected by Microsoft for your development or use of a PlayReady Server), or you can use a PlayReady Server provided or operated by a third party. Whether you develop your own PlayReady Server or the PlayReady Server is provided or operated by a third party, you must be able to communicate the key values and the key IDs to the server in a timely manner for the client to be able to play back your content efficiently.


## Operating a PlayReady Packager

The following figure shows the overall view of how a PlayReady packager operates with other parts of the content delivery system.

![PlayReady Packager Operation](../images/packager_operation.png)

Clear content is provided to the packager, which then 

Describe how to generate keys. Describe for one key, multiple keys, and rotating keys.

Describe the KMS.


## See also
[PlayReady Test Server Content](http://test.playready.microsoft.com/)
