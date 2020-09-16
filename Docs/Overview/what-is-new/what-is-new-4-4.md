---
title: "What's New"
description: This section provides an overview of changes from PlayReady version 4.2 to PlayReady version 4.4.
ms.assetid: "D9B3FE09-931E-4B28-8A7A-5D422C86AB12"
keywords: playready overview version changes 4.2 4.4
ms.date: 10/02/2019
ms.topic: conceptual
---

# What's New in PlayReady Version 4.4

This page contains an overview of the most significant changes between PlayReady version 4.2 and PlayReady version 4.4.
<br/><br/>

## General Changes in PlayReady Version 4.4

The ability to determine what features a given Porting Kit implementation supports is added on both client and server.
<br/><br/>

## Changes in PlayReady Server SDK Version 4.4

### General

A server application can now determine what features the client has implemented if the client is also version 4.4 or higher. For more information, see [How to Determine What Features a Client Supports](../../Advanced/how-to-determine-client-features.md).

A server application can now explicitly request that one or more revoked client certificates be treated as if they were not revoked.  For more information, see [PlayReady Revocation](../revocation.md).
<br/><br/>

## Changes in PlayReady Device Porting Kit Version 4.4

### General

The client application can now determine what features the specific OEM implementation of the PlayReady Device Porting Kit has implemented. For more information, refer to structure definitions in source code file source/inc/drmmanagertypes.h.

The client sends what features the specific OEM implementation of the PlayReady Device Porting Kit has implemented to the server as part of its License Acquisition challenge. For more information see [How to Determine What Features a Client Supports](../../Advanced/how-to-determine-client-features.md).
<br/><br/>

### API

The non-spec-compliant CDMI interface is no longer included (formerly source/cdmi/\*). Microsoft recommends migration to the spec-compliant CDMI interface. For more information, refer to source code files source/inc/drmcdmi\* and source/modules/cdmi/real/\*.

The following OEM APIs have been added. For more information, refer to the corresponding source code file where the default implementation of the API resides.

    Oem_Clock_GetSystemTimeOffsetAsInt64
    Oem_Clock_SetSecureClockOffsetValue
    OEM_ECC_GenerateTeeSigningPublicKey_P256Impl
    OEM_ECC_GenerateTeeSigningPublicKey_P256
    OEM_TEE_CRYPTO_ECC256_GenerateTeeSigningPrivateKey
    OEM_TEE_BASE_ECC256_GenerateTeeSigningPrivateKey
    OEM_TEE_BASE_GetExtendedVersion

