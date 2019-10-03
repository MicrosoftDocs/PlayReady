---
title: "What's New"
description: An overview of changes from PlayReady version 4.0 to PlayReady version 4.3
ms.assetid: "D9B3FE09-931E-4B28-8A7A-5D422C86AB12"
keywords: playready overview version changes 4.0 4.3
ms.date: 10/02/2019
ms.topic: conceptual
---

# What's New in PlayReady Version 4.3

This page contains an overview of the most significant changes between PlayReady version 4.0 and PlayReady version 4.3.

<br/>

## General Changes in PlayReady Version 4.3

The SecureStop2 feature is added. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).



## Changes in PlayReady Server SDK Version 4.3

### General

The server can now process SecureStop2 messages. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).



## Changes in PlayReady Device Porting Kit Version 4.3

### General

The client now sends SecureStop2 messages to the server. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).

The client application can now choose to reject individual licenses during Drm_Reader_Bind. For more information, refer to enum and structure documentation in source code file source/inc/drmcallbacktypes.h.

The client application can now determine what features the specific OEM implementation of the PlayReady Device Porting Kit has implemented. For more information, refer to structure definitions in source code file source/inc/drmmanagertypes.h.

It is now easier to change compiler settings and add OEM-specific error codes. For more information, refer to source code files source/inc/oemcompiler.h and source/inc/oemresults.h.

The drmcipher_test.exe and drmcrypto_test.exe tools are no longer included in compiled form. They can still be compiled using source code files source/test/cipher/\* and source/test/crypto/\*.

The DrmFileViewer.exe tool and its corresponding source code are no longer included. It only supported file formats which are no longer in widespread use.

The term "batch ID" has been globally replaced with "session ID". This impacts certain public structures. For example, in source code file source/inc/drmlicacqv3.h structure definition DRM_LICENSE_RESPONSE, the member m_oBatchID was renamed to m_idSession. (The term "batch ID" and the term "session ID" have historically been interchangeable in the PlayReady Device Porting Kit.)

### API

Migration from previous versions of PlayReady has been simplified with respect to the Output Protection structures passed to the DRMPFNPOLICYCALLBACK callback. For more information, refer to source code file source/inc/drmoutputleveltypes.h.

The non-spec-compliant CDMI interface is no longer included (formerly source/cdmi/\*). Microsoft recommends migration to the spec-compliant CDMI interface. For more information, refer to source code files source/inc/drmcdmi\* and source/modules/cdmi/real/\*.

The DRM_CDMI_DecryptOpaque API has been updated to support decryptionof AES128CBC content. For more information, refer to source code files source/inc/drmcdmi.h and source/modules/cdmi/real/drmcdmireal.c.

The following public API has been removed.

    Drm_Revocation_StoreRevListArray

The following OEM API has been renamed.

    OEM_TEE_BASE_SignHashWithDeviceSigningKey -> OEM_TEE_BASE_ECDSA_P256_SignHash

The following OEM API now has some of its parameters changed to optional (they may be NULL on input). For more information, refer to source code file source/oem/common/inc/oemtee.h.

    OEM_TEE_BASE_GetVersionInformation

The following OEM APIs have been added. For more information, refer to the corresponding source code file where the default implementation of the API resides.

    Oem_Clock_GetSystemTimeOffsetAsInt64
    Oem_Clock_SetSecureClockOffsetValue
    OEM_ECC_GenerateTeeFeatureInformationSigningPublicKey_P256Impl
    OEM_ECC_GenerateTeeFeatureInformationSigningPublicKey_P256
    OEM_TEE_CRYPTO_ECC256_GenerateTeeFeatureInformationSigningKey
    OEM_TEE_BASE_ECC256_GenerateTeeFeatureInformationSigningKey
    OEM_TEE_BASE_GetExtendedVersion
    OEM_TEE_BASE_ECDSA_P256_SignData
    OEM_TEE_SECURESTOP2_StopDecryptors

The following OEM APIs have been removed.

    Oem_MemRealloc
    OEM_SHA256_Finalize_With_SHA_1_Size
    OEM_SHA256_HMAC_Init
    OEM_SHA256_HMAC_Update
    OEM_SHA256_HMAC_Finalize
    OEM_SHA256_HMAC_FinalizeOffset
    OEM_SHA256_HMAC_CreateMAC
    OEM_SHA256_HMAC_VerifyMAC
    OEM_TEE_LPROV_ECDSA_Sign
    OEM_TEE_LPROV_GetDeviceModelInfo




