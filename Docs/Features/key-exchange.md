---
title: PlayReady Key Exchange
description: Key Exchange is the process for providing arbitrary keys to a client for application-specific cryptographic operations.
ms.assetid: "7E53CF48-9CFC-4875-8EC8-4BA38AB2E602"
keywords: PlayReady Key Exchange, Key Exchange architecture, Key Exchange licenses
ms.date: 10/15/2021
ms.topic: article
---

# PlayReady Key Exchange

*Key Exchange* is the process by which arbitrary cryptographic keys (for supported algorithms), protected by PlayReady, are sent to the client from the [License Server](../Overview/license-server.md). This allows the Server to perform cryptographic operations with those keys (encrypt, decrypt, sign, verify) and the client to perform the corresponding operation (decrypt, encrypt, verify, sign) with the same keys.

> [!NOTE]
> This feature is only supported when both the client and server are using PlayReady version 4.5 or higher.

> [!IMPORTANT]
> Data on which the cryptographic operation is performed is *not* protected by PlayReady. PlayReady only protects the cryptographic keys themselves.

## Key Exchange architecture

Keys are delivered to the client via a KeyExchangeLicense, a unique type of license which can only be used for key exchange operations, during ordinary license acquisition.

Keys are protected on the client by PlayReady at the same [Security Level](../Overview/security-level.md) as content keys themselves.

> [!IMPORTANT]
> Keys used for protection of content itself must not be sent to the client via a KeyExchangeLicense. Doing so is a violation of the [PlayReady Compliance and Robustness Rules (CR&RRs)](../Overview/compliance-and-robustness-rules.md).

## Key Exchange licenses

A single KeyExchangeLicense contains the following

- A single cryptographic key
- Policy indicating which unique cryptographic operation (algorithm plus type, e.g. "decrypt) the client may perform
- Additional policy associated with the key such as absolute expiration

## Key Exchange cryptography

On the server, a KeyExchangeLicense is generally constructed and used in the [PlayReady Sever SDK](../Overview/server-sdk.md) like a MediaLicense with the following primary differences.

- The cryptographic key requires its cryptographic operation to be specified at the same time as said key
- Some MediaLicense policies are not supported, primarily those such as [Output Protection Levels](../Overview/output-protection-levels.md) which are only relevant for playback

Refer to the [KeyExchangeLicense Class](/dotnet/api/microsoft.media.drm.keyexchangelicense) documentation for more information.

On the client, a KeyExchangeLicense is used via new Drm_KeyExchange_* APIs. They enable a client to perform the following operations. Refer to the API documentation provided in the associated code comments in the [PlayReady Device Porting Kit](/playready/overview/device-porting-kit) for more information.

- Bind to a KeyExchange license which verifies associated license policy
- Perform the single allowed cryptographic operation with the associated key (repeatedly, as desired)
