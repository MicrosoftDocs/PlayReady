---
title: Developing a PlayReady Packager
description: Developing a PlayReady Packager
ms.assetid: "CFAF35FD-CCBE-49EF-B4CE-708FBCDE298A"
keywords:  PlayReady, packager, encryptor, developing packager
ms.date: 05/11/2018
ms.topic: conceptual
---

# Developing a PlayReady Packager 

There are several considerations you should examine before you begin incorporating PlayReady in your packager to protect content. Note that developing a packager that provides PlayReady protection for content you want to encrypt:

* Does not require a licensing agreement from Microsoft. 
* There are no fees to Microsoft associated with inserting PlayReady in your content.
* There are no royalty payments to Microsoft applicable to PlayReady encoders or packagers.

Therefore, you do not need to allocate any time or budget for these items.

>[!NOTE]
>Some [Microsoft PlayReady Partners](https://www.microsoft.com/playready/partners/) can develop a PlayReady packager for your company if you don't want to develop it yourself.

## Development Overview

The development time for incorporating the PlayReady functionality in your packager will depend on the development and testing of the following components:

* Key Generator &mdash; generates the key value used to encrypt the content (along with its associated KeyID). If you use the KeySeed mechanism, this generator needs to implement the function as defined in the [PlayReady Key Seed](../Specifications/playready-key-seed.md) specification.

* PlayReady Header Generator &mdash; generates the PlayReady Object (including the PlayReady Header and/or an Embedded License Store). This PlayReady Header includes the KeyID or the list of KeyIDs, the default URL of the PlayReady license server, and any custom value you require for your protected content. This function must follow the requirements outlined in the [PlayReady Header Specification](../Specifications/playready-header-specification.md).

* Packager &mdash; packages the content using the key value supplied by the key generator and the PlayReady Object created by the PlayReady header generator.

* Key Management System &mdash; stores the key value and its associated KeyId (not required if using the KeySeed mechanism).


## Developing a PlayReady Packager

If you have decided to develop your own PlayReady Packager, you will need to decide how you want the packager to work, based on how you want your content stored and delivered. The following list provides the necessary steps required to add PlayReady functionality to your packager.

1. Choose your encryption format. Several different types of encryption are used to protect content. Microsoft PlayReady systems use the symmetric key algorithm, Advanced Encryption Standard (AES). Starting with version 4.0, PlayReady systems support AES 128 keys in both CBC (Cipher Block Chaining) and CTR (Counter Mode) modes, as defined in the ISO standard ISO/IEC 23001-7. The encryption mechanisms used to protect content are encapsulated in a container, so that files can be efficiently browsed and decrypted on a variety of platforms. 

   Any encryption format that uses AES-128 keys used in CTR mode or CBC mode is allowed by the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/). For more information, see [PlayReady Content Encryption Modes](content-encryption-modes.md).

2. Choose how you are going to encrypt your content. For more information, see [Using encryption keys](content-packaging-and-delivery.md#using-encryption-keys).

3. Choose whether you want to decrypt your content using only PlayReady, or whether you want to support multiple DRMs. For more information, see [Using encryption tools](content-packaging-and-delivery.md#using-encryption-tools).

4. Choose how you are going to generate and store content keys (Key Value and Key ID). 

   Your packager should include some kind of key generator that creates the Key Value used to encrypt and decrypt your content. The key generator should associate a Key ID to the Key Value. The Key Value remains a secret, and the Key ID is public and is inserted in the PlayReady header in your content. If the packager does not include a key generator, you need to develop or source one separately.

   You will either need to develop a key management system to store multiple Key Values and their associated Key IDs, or license one from a third party. The key management system could be a database or any other type of storage system, but must be secure to prevent anyone from accessing the key values without authorization. Microsoft does not supply a key management system with PlayReady. Alternatively, you can use the KeySeed mechanism supplied with PlayReady in place of the key management system (the KeySeed mechanism must be incorporated in your packager and in the PlayReady Server that supplies the licences for decrypting the content).

5. Choose how you are going to insert a PlayReady Object (including the PlayReady header and/or the embedded license store) in your encrypted content. For more information, see [How to generate a PlayReady Header](how-to-generate-playready-header.md).

6. Choose how you are going to provide the key values and key IDs to a PlayReady Server, which will then distribute the key values to PlayReady clients. 

    You can develop your own PlayReady License Server (requires a license from PlayReady &mdash; however no fees or royalties are collected by Microsoft for your development or use of a PlayReady Server), or you can use a PlayReady Server provided or operated by a third party. Whether you develop your own PlayReady Server or the PlayReady Server is provided or operated by a third party, you must be able to communicate the key values and the key IDs to the server in a timely manner for the client to be able to play back your content efficiently.
    
7. Choose how the clients are going to contact the PlayReady License Server to acquire the content encryption keys. The client apps must be aware of the PlayReady License Server URL (also known as License Acquisition URL, or LA URL) when they need to acquire a license. The client apps could be programmed to have that LA URL value hardcoded, or retrieve it dynamically from the server. If the client app doesn't have this LA URL value, it will use the LA URL value found in the content's PlayReady Header, which is the default LA URL. Although it is not required, it is very common for services to include a default LA URL value in the content's PlayReady Header at packaging time.

## See also
[PlayReady Test Server Content](http://test.playready.microsoft.com/)
