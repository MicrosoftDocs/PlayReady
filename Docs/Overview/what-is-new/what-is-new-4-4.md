---
title: What's New in PlayReady Version 4.4
description: This section provides an overview of changes from PlayReady version 4.3 to PlayReady version 4.4.
ms.assetid: "D9B3FE09-931E-4B28-8A7A-5D422C86AB12"
keywords: playready overview version changes 4.3 4.4
ms.date: 10/02/2019
ms.topic: conceptual
---

# What's New in PlayReady Version 4.4

This page contains an overview of the most significant changes between PlayReady version 4.3 and PlayReady version 4.4.

## General Changes in PlayReady Version 4.4

The ability to determine what features a given Porting Kit implementation supports is added on both client and server.

When multiple non-leaf licenses are acquired in a single license acquisition response, the server can optionally perform additional cryptography to reduce cryptography on the client.

## General changes in PlayReady Server SDK Version 4.4

Windows now supports CBCS for both hardware and software DRM.  Additionally, the PlayReady license server extends CBCS support for SL2000.

The server can now process SecureStop2 messages. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).

A server application can now determine what features the client has implemented if the client is also version 4.4 or higher. For more information, see [How to Determine What Features a Client Supports](../../Advanced/how-to-determine-client-features.md).

Property LicenseResponse.IncludeOptimizedContentKey2 has been added (defaulting to false).

1. If the Optimized Content Key 2 feature cannot improve performance on the client, the property has no effect.  For example, if the client is older than version 4.4, the property is ignored.
2. Otherwise, setting the property to true will cause the server to perform one additional asymmetric encrypt operation when generating the license acquisition response and include an "Optimized Content Key 2" in each non-leaf license included in the response.
See "Changes in PlayReady Device Porting Kit Version 4.4" below for the corresponding benefits of this feature.

## Changes in PlayReady Device Porting Kit Version 4.4

### General

The client application can now determine what features the specific OEM implementation of the PlayReady Device Porting Kit has implemented. For more information, refer to structure definitions in source code file source/inc/drmmanagertypes.h.

The client sends what features the specific OEM implementation of the PlayReady Device Porting Kit has implemented to the server as part of its License Acquisition challenge. For more information see [How to Determine What Features a Client Supports](../../Advanced/how-to-determine-client-features.md).

A license may now contain an Optimized Content Key 2 XMR object.  When multiple non-leaf licenses from a single license acquisition response containing this XMR object are bound (via Drm_Reader_Bind) in the same DRM_APP_CONTEXT, the client will only perform one asymmetric crypto operation total instead of one per license.  This can be particularly useful when a client might receive multiple bitrates or streams with different content keys; a single asymmetric crypto operation on the server could eliminate several such operations on the client.

### API

The non-spec-compliant CDMI interface is no longer included (formerly source/cdmi/\*). Microsoft recommends migration to the spec-compliant CDMI interface. For more information, refer to source code files source/inc/drmcdmi\* and source/modules/cdmi/real/\*.

The following OEM APIs have been added. For more information, refer to the corresponding source code file where the default implementation of the API resides.

```c
Oem_Clock_GetSystemTimeOffsetAsInt64
Oem_Clock_SetSecureClockOffsetValue
OEM_ECC_GenerateTeeSigningPublicKey_P256Impl
OEM_ECC_GenerateTeeSigningPublicKey_P256
OEM_TEE_CRYPTO_ECC256_GenerateTeeSigningPrivateKey
OEM_TEE_BASE_ECC256_GenerateTeeSigningPrivateKey
OEM_TEE_BASE_GetExtendedVersion
```
