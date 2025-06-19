---
title: Licenses
description: After a Client retrieves a protected file, that Client needs to acquire a license before it can perform actions that use that content.
ms.assetid: "EF3BEE65-8412-4A9A-8AA9-A3F6AF2E3D92"
keywords: playready licenses, key, policies, encryption, decrypt
ms.date: 02/01/2018
ms.topic: article
---


# Licenses

After a client retrieves a protected file, that client needs to acquire a license before it can perform actions that use that content. Licenses store the information necessary to access the associated content and store the rules by which that content can be accessed. Users must acquire their own licenses to play protected content, even if the protected content was copied from someone who already had a license for it. Licenses contain the encryption key to decrypt the corresponding content or, in the case of chained licenses, contain an intermediary key. Licenses also contain rights and other properties that specify the use of the content. For example, the license determines the number of times a protected file can be played, and whether the license ever expires. These properties are configured in the license separately from the protected file.

Each license contains the following information:

   *  The content encryption key.
   *  The rights and conditions of the license, otherwise known as policies.
   *  Optional attributes, such as a name and description of the license.

Before a client can decrypt the content associated with a license, it must retrieve the policy from the license. The content protection information within the license is encrypted using a client's public key or a client's domain's public key encryption information. The license is considered "bound" to the client or domain that has the private key for decrypting the content protection information.

Clients acquire licenses either directly from License Servers or through a proxy Server.

## In this section

[Output Protection Levels](output-protection-levels.md)

[License Acquisition](license-acquisition.md)

[License Chaining](license-chaining.md)

[Embedded Licenses](embedded-licenses.md)

[License Nonce](license-nonce.md)

[Key and Key IDs](key-and-key-ids-kids.md)

[License and Policies](license-and-policies.md)

[Licenses Restricted by Binding Policy](licenses-restricted-by-binding-policy.md)

[Licenses Restricted by Extensible Policy](licenses-restricted-by-extensible-policy.md)

[Best Practices for License Policies](policies-best-practices.md)
