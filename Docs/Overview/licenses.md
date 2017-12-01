---
author:
title: "Licenses"
description: ""
ms.assetid: "EF3BEE65-8412-4A9A-8AA9-A3F6AF2E3D92"
kindex: licenses
keywords:  licenses, key, policies, encryption, decrypt
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Licenses

After a client retrieves a protected file, that client needs to acquire a license before it can perform actions that use that content. Licenses store the information necessary to access the associated content and store the rules by which that content can be accessed. Users must acquire their own licenses to play protected content, even if the protected content was copied from someone who already had a license for it. Licenses contain the encryption key to decrypt the corresponding content or, in the case of chained licenses, contain an intermediary key. Licenses also contain rights and other properties that specify the use of the content. For example, the license determines the number of times a protected file can be played, and whether the license ever expires. These properties are configured in the license separately from the protected file.

Each license contains the following information:

   *  The content encryption key.
   *  The rights and conditions of the license.
   *  Optional attributes, such as a name and description of the license.

Before a client can decrypt the content associated with a license, it must retrieve the policy from the license. The content protection information within the license is encrypted using a client's public key or a client's domain's public key encryption information. The license is considered "bound" to the client or domain that has the private key for decrypting the content protection information.

Clients acquire licenses either directly from license servers or through a proxy server.

## In This Section

[Output Protection Levels](outputprotectionlevels.md)

[License Generation and Issuance](licensegenerationandissuance.md)

[License Acquisition](licenseacquisition.md)

[License Chaining](licensechaining.md)

[Embedded Licenses](embeddedlicenses.md)

[License Nonce](licensenonce.md)

[Key and Key IDs](keyandkeyidskids1.md)

[License and Policies](licenseandpolicies.md)

[Licenses Restricted by Binding Policy](licensesrestrictedbybindingpolicy.md)

[Licenses Restricted by Extensible Policy](licensesrestrictedbyextensiblepolicy.md)

[Best Practices for License Policies](bestpractices.md)
