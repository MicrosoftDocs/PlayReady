---
title: Packaging Content
description: PlayReady helps secure encrypted content by distributing and controlling the use of content encryption keys over networks and in Clients.
ms.assetid: "4B45DCD6-73FE-45B4-A5DF-926942695B7B"
keywords: playready content encryption, encryption, content encryption
ms.date: 02/01/2018
ms.topic: concept-article
---


# Packaging Content

PlayReady helps secure encrypted content by distributing and controlling the use of content encryption keys over networks and in clients. With this technology, content owners and services distributing high-valued content can monetize their content with full control over their business model.

The packager is an appliance, or a software or a cloud service that takes a piece of video and audio in the clear and protects it with PlayReady and encrypts it. The packager is sometimes also called the encryptor. The packager is frequently integrated in the encoder, but it may be a separate function that runs on the output of the encoder.

Companies developing a standalone packager (or a packaging function in an encoder) utilizing PlayReady technologies need to integrate two functionalities in their product:

* One that encrypts content in a PlayReady compatible encryption format.

* Another that generates a PlayReady Object (along with its associated PlayReady Header) and inserts it in the encrypted content.

>[!IMPORTANT]
>Developing or operating a PlayReady packager can be done without signing any PlayReady licensing agreement with Microsoft, and without paying any fee or royalty to Microsoft for the PlayReady technology.




## In this section

[Content Packaging and Delivery](content-packaging-and-delivery.md)

[PlayReady Content Encryption](content-encryption.md)

[PlayReady Content Encryption Modes](content-encryption-modes.md)

[Developing a PlayReady Packager](developing-a-packager.md)

[Operating a PlayReady Packager](operating-a-packager.md)

[How to generate a PlayReady Header](how-to-generate-playready-header.md)

[How to package MP4-based content](how-to-package-mp4-based.md)

[MP4-based Formats Supported by PlayReady Clients](mp4-based-formats-supported-by-playready-clients.md)
