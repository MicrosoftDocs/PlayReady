---
author:
title: "Licenses Overview"
description: "Licenses store the information necessary to access the associated content and store the rules by which that content can be accessed."
ms.assetid: "ead76d10-fe40-bf74-4fcd-e109fc2ba1bb"
kindex: licenses, overview
kindex: direct license acquisition, licenses overview
kindex: predelivery, licenses overview
keywords:  overview licenses,  licenses overview direct license acquisition,  licenses overview predelivery
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Licenses Overview

Licenses store the information necessary to access the associated content and store the rules by which that content can be accessed. Users must acquire their own licenses to play protected content, even if the protected content was copied from someone who already had a license for it. Licenses contain the encryption key to decrypt the corresponding content or, in the case of chained licenses, contain an intermediary key. Licenses also contain rights and other properties that specify the use of the content. For example, the license determines the number of times a protected file can be played, and whether the license ever expires. The properties are configured in the license separately from the protected file.

Licenses can be acquired in several ways:

   *  **Direct license acquisition**&mdash;The DRM client initiates license acquisition. If the user tries to play a file and a valid license is not found, the player opens the license acquisition URL, which points to the license server.<br/>
   *  **Predelivery**&mdash;The license is delivered to the DRM client before the content. For example, while a user is downloading a protected song, the content provider redirects the user to a Web site that issues a license for the content, thus allowing the user to play the content immediately after the download is complete, rather than having to acquire a license in a separate process.<br/>

Each license contains the following information:

   *  The content encryption key.<br/>
   *  The rights and conditions of the license.<br/>
   *  Optional attributes, such as a name and description of the license.<br/>

## License management in the PlayReady ecosystem


License management enables scenarios in which existing licenses are migrated and restored with license chains, simplifies license updates, and identifies the licenses that need to be transferred from a server to a client.

The following topics describe license management principles.

| Topic| Description|
| --- | --- |
| [About License Generation and Issuance](licensegenerationandissuance.md)| Describes how licenses are created and issued to clients.|
| [About License Chaining](licensechaining.md)| Describes how license chaining enables more efficient use of multiple licenses.|

## Policies and strategies for distributing licenses for PlayReady content

After a client retrieves a protected file, that client needs to acquire a license before it can perform actions that use that content. Licenses encapsulate information describing the policies associated with particular content, along with information that is required to decrypt the content. In other words, a license is the key for unlocking content as well as the rules for how that content may be used. Different licenses for the same piece of content may grant different rights for that content.

Licenses contain the policy and protection information for the content associated with the license. Before a client can decrypt the content associated with a license, it must retrieve the policy from the license. The content protection information within the license is encrypted using a client's public key or a client's domain's public key encryption information. The license is considered "bound" to the client or domain that has the private key for decrypting the content protection information.

Licenses are acquired either directly from license servers or through a proxy server.

Information about policies and strategies for distributing licenses are covered in the following topics.

| Topic| Description|
| --- | --- |
| [About License Acquisition](licenseacquisition.md)| Describes license acquisition and the steps required to acquire a license.|
| [About Embedded Licenses](embeddedlicenses.md)| Provides an overview of embedded licenses.|
| [Licenses Restricted by Binding Policies](licensesrestrictedbybindingpolicy.md)| Describes how to restrict licenses using different types of binding policies.|
| [Licenses Restricted by Extensible Policies](licensesrestrictedbyextensiblepolicy.md)| Describes how to restrict licenses by extending the existing XMR policy system.|


