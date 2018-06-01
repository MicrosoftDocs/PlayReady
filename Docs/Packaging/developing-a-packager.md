---
author: dougklopfenstein
title: Developing a PlayReady Packager
description: Developing a PlayReady Packager
ms.assetid: "CFAF35FD-CCBE-49EF-B4CE-708FBCDE298A"
keywords:  PlayReady, packager, encryptor, developing packager
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

* Packager&mdash;packages the content using the key value supplied by the key generator and the PlayReady Object created by the PlayReady header generator.

* Key Generator&mdash;generates the key value used to encrypt the content (along with its associated KeyID).

* PlayReady Header Generator&mdash;generates the PlayReady Object (including the PlayReady Header and/or an embedded license store).

* Key Management System&mdash;stores the key value and its associated KeyId (not required if using the KeySeed mechanism).

* PlayReady Server&mdash;supplies the key value to the client that is requesting content using the KeyID embedded in the PlayReady Header of the encrypted content.

## Development considerations

The basic development considerations for incorporating PlayReady in your packager are:

* A function must be developed to generate the key value and KeyID used to package the content.

* A function must be developed to generate the PlayReady Object, insert the key value and KeyID into the header, include the URL of the PlayReady license server, and include any custom value you require for your encrypted content. This function must follow the requirements outlined in the [PlayReady Header Specification](../Specifications/playready-header-specification.md).

* Some means of storing the key values and KeyIDs (a key management system) or a KeySeed mechanism.

* Optional packaging using more than one DRM.

* A method of communicating the key values and KeyIDs to a PlayReady license server.

You will need to allocate time in your budget for these tasks. For more information on development considerations, see [Developing a PlayReady Packager](developing-a-packager.md).

## Additional considerations

The key value and KeyID used to package content using your packager must be supplied to a PlayReady license server, which will then be queried by the client for the key value associated with the KeyID. Depending on how you accomplish this, you will need to budget for the following extra development: 

* If you are using a third-party license server, you will need to allocate in your budget the time and expense of acquiring the rights to use the third-party PlayReady license server.

* If you are planning to use your own PlayReady server, you need to consider the following extra development expenses:

  * You must allocate the time required to request and receive a PlayReady deployment certificate. For more information about the process and timeline for obtaining a PlayReady deployment certificate, see the [PlayReady Licensing Process](http://public.wmlalicensing.com/public/#licensingprocess) web page, and look under the "Agreements *without* Fees/Royalties" heading. (A PlayReady server does not require any fees or royalties.)

  * Any development beyond supplying the key value for the KeyID sent by the client (such as rights and right restrictions) must also be budgetted (which is beyond the scope of this topic).


# Developing a PlayReady Packager

>[!NOTE]
>Some [Microsoft PlayReady Partners](https://www.microsoft.com/playready/partners/) can develop a PlayReady packager for your company if you're not willing to develop it yourself.


If you have decided to develop your own PlayReady Packager, you will need to decide how you want the packager to work, based on how you want your content stored and delivered. The following list provides the necessary steps required to add PlayReady functionality to your packager.

1. Choose your encryption format. Several different types of encryption are used to protect content. Microsoft PlayReady systems use the symmetric key algorithm, Advanced Encryption Standard (AES). Starting with version 4.0, PlayReady systems support AES 128 keys in both CBC (Cipher Block Chaining) and CTR (Counter Mode) modes, as defined in the ISO standard ISO/IEC 23001-7. The encryption mechanisms used to protect content are encapsulated in a container, so that files can be efficiently browsed and decrypted on a variety of platforms. 

   Any encryption format that uses AES-128 keys used in CTR mode or CBC mode is allowed by the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/). For more information, see [PlayReady Content Encryption Modes](content-encryption-modes.md).

2. Choose how you are going to encrypt your content. For more information, see [Using encryption keys](content-packaging-and-delivery.md#using-encryption-keys).

3. Choose whether you want to encrypt your content using only PlayReady, or whether you want to use multiple DRMs. For more information, see [Using encryption tools](content-packaging-and-delivery.md#using-encryption-tools).

4. Choose how you are going to generate and store content keys (Key Value and Key ID). 

   Your packager should include some kind of key generator that creates the Key Value used to encrypt and decrypt your content. In addition, the key generator should associate a Key ID to the Key Value. The Key Value remains a secret, and the Key ID is public and is inserted in the PlayReady header in your content.

   You will either need to develop a key management system to store multiple Key Values and their associated Key IDs, or license one from a third party. The key management system could be a database or any other type of storage system, but must be secure to prevent anyone from accessing the key values without authorization. Microsoft does not supply a key management system with PlayReady. Alternatively, you can use the KeySeed mechanism supplied with PlayReady in place of the key management system (the KeySeed mechanism must be incorporated in your packager and in the PlayReady Server that supplies the licences for decrypting the content).

5. Choose how you are going to insert a PlayReady Object (including the PlayReady header and/or the embedded license store) in your encrypted content. For more information, see [How to generate a PlayReady Header](how-to-generate-playready-header.md).

6. Choose how you are going to provide the key values and key IDs to a PlayReady Server, which will then distribute the key values to PlayReady clients. 

    You can create your own PlayReady Server (requires a license from PlayReady&mdash;however no fees or royalties are collected by Microsoft for your development or use of a PlayReady Server), or you can use a PlayReady Server provided or operated by a third party. Whether you develop your own PlayReady Server or the PlayReady Server is provided or operated by a third party, you must be able to communicate the key values and the key IDs to the server in a timely manner for the client to be able to play back your content efficiently. In addition, you will need to include the URL of the PlayReady Server that manages the licenses for your content in the PlayReady Header that's inserted in your content at packaging time.

## See also
[PlayReady Test Server Content](http://test.playready.microsoft.com/)
