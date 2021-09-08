---
title: What's New in PlayReady Version 4.5
description: This section provides an overview of changes from PlayReady version 4.4 to PlayReady version 4.5.
ms.assetid: "578AA33C-54BD-453B-BAD6-B5C67A586B6F"
keywords: playready overview version changes 4.4 4.5
ms.date: 09/07/2021
ms.topic: conceptual
---

# What's New in PlayReady Version 4.5

This page contains an overview of the most significant changes between PlayReady version 4.4 and PlayReady version 4.5.

## General Changes in PlayReady Version 4.5

### Challenge Encryption with PlayReady Server Deployment Certificate

In previous versions of PlayReady, license acquisition and other client challenges are always privacy-encrypted with a fixed public key.  Starting with PlayReady 4.5, a client that is coded to talk only to a supporting server may instead privacy-encrypt challenges with the PlayReady Server Deployment Certificate issued to the server licensee by Microsoft.  The PlayReady Server SDK then decrypts the challenge with the corresponding private key, passed to it by the PlayReady Server SDK application, instead of a fixed private key.

### License Server Time

In previous versions of PlayReady, using the Secure Time feature usually required the client application to talk to a separate Secure Time server to obtain the time used to set its local clock.  Starting with PlayReady 4.5, a client that is coded to talk only to a supporting server may instead use a time provided by the PlayReady Server SDK during license acquisition.  For more information, see [PlayReady Trusted Clocks](../../Features/trusted-clocks.md).

### Key Exchange

Using the license acquisition protocol, a PlayReady client and server may now exchange arbitrary keys which can be used to encrypt, decrypt, sign, and verify arbitrary application-provided data where the keys themselves are protected using PlayReady.  When the client is SL3000, the keys themsevles are protected by the Trusted Execution Environment.  For more information, see [PlayReady Key Exchange](../../Features/key-exchange.md).

### Watermarking Policy

Functionality was added to simplify use of the Watermarking Signalling Explicit Digital Video Output Restriction as defined by the PlayReady Compliance Rules.

## Changes in PlayReady Server SDK Version 4.5

### General

Key Exchange licenses can be used to provide arbitrary keys to a client during license acquisition.

If provided by the client, the supported watermarking technologies are exposed to the PlayReady Server SDK application.  This simplifies use of the Watermarking Signalling Explicit Digital Video Output Restriction as defined by the PlayReady Compliance Rules.

### API

This is merely an overview.  Refer to the API documentation [TODO: link] for more information.

The LicenseResponse.GetLicenses method now returns an empty array instead of null when no licenses have been added.

The following classes and enums were added.

   *  AdvancedLicense class (abstract, inherits from License) - a subset existing properties and methods from MediaLicense were moved into this class, and MediaLicense now inherits from AbstractLicense.  No application changes are required to use MediaLicense.
   *  KeyExchangeLicense class (inherits from AdvancedLicense) - used to create licenses that provide arbitrary keys to a client during license acquisition.
   *  KeyExchangeRight class (inherits from Right) - used to specify the key and its allowed usage to a KeyExchange license.
   *  KeyExchangeAlgorithm enum - used to specify the allowed usage for a key in a KeyExchange license.
   *  WatermarkVendor class - used to expose the client's supported watermarking technologies to the application.
   *  LicenseServerTimeCertificate class - used to contain the certificate for signing the license server time returned in the license acquisition response.

The following were added to individual classes.

   *  The PlayReadyHeader class exposes whether the header indicates support for per-stream keys and whether it explicitly requests a license or not.
   *  The ContentKeyType enum adds the value KeyExchange.
   *  The Certificate class adds byte array properties exposing the certificate's digest and issuer public key.
   *  The License class adds a guid property exposing the license's unique id and an IEnumerable<Right> property to return the rights that were added to the license.
   *  The LicenseChalengeTeeAPIs enum adds values for all new PK 4.5 TEE APIs.
   *  The LicenseChallengeReeFeatures enum adds values for LicenseServerTime and KeyExchange.
   *  The LicenseChallenge class adds the list of KeyExchangeAlgorithms the client supports, the WatermarkVendors the client supports, the PK versions of the client's TEE and REE (which may or may not be the same), and whether the client requires the current LicenseServerTime.
   *  The LicenseResponse class adds a LicenseServerTimeCertificate property for setting the certificate used to sign the License Server Time returned in the license acquisition response.
   *  The ExplicitOutputRestrictionsConstants class adds constants for Watermark and InternalScreenOnly.  Refer to the PlayReady Compliance Rules for more information on these guids.

## Changes in PlayReady Device Porting Kit Version 4.5

### General

   *  The entire PlayReady Device Porting Kit has been updated to Microsoft Source-code Annotation Language (SAL) 2.0.
   *  Some unsupported codepaths only used in Microsoft-internal implementations were removed to eliminate confusion and reduce compile times and binary sizes.  Further improvements in this area is expected to be included in future releases.
   *  Where supported by the underlying compiler and machine architecture, native 128-bit integer types can now be used to accelerate the default implementation of ECC256.
   *  A default implementation of the SHA256 HMAC algorithm was added.

### API

This is merely an overview.  Refer to the API documentation provided in the associated code comments in the PlayReady Porting Kit for more information.

DRM_CDMI_SetServercertificate is now allowed to be called with a PlayReady Server Deployment Certificate for privacy-encrypting license acquisition and other client challenges.  The function forwards to Drm_AppContext_SetProperty in this scenario.  Existing usage reamins as-is.

The following public functions were added.

```c
Drm_AppContext_SetProperty
Drm_KeyExchange_Prepare
Drm_KeyExchange_Perform
Drm_KeyExchange_Close
```

The following structures were added.

```c
DRM_DGP_REE_FEATURE_LIST_4_5
DRM_DGP_TEE_API_LIST_4_5
```

The following TEE APIs were added.

```c
DRM_TEE_BASE_GetSystemTime2
DRM_TEE_LICPREP_PackageKey2
DRM_TEE_LICENSESERVERTIME_ProcessResponseData
DRM_TEE_DECRYPT_PrepareToDecrypt2
DRM_TEE_LICGEN_CompleteLicense2
DRM_TEE_KEYEXCHANGE_Prepare
DRM_TEE_KEYEXCHANGE_Perform
```

The following OEM TEE APIs were added.

```c
OEM_TEE_BASE_ECC256_SetKey
OEM_TEE_CRYPTO_SHA256_HMAC_VerifyMAC
OEM_TEE_CRYPTO_SHA256_HMAC_CreateMAC
OEM_TEE_PERSISTENTSTORAGE_Read
OEM_TEE_PERSISTENTSTORAGE_Write
OEM_TEE_GetSupportedWatermarkVendors
```

The following OEM TEE APIs were renamed without functional changes.

```c
OEM_TEE_DECRYPT_UnshuffleScalableContentKeys -> OEM_TEE_BASE_UnshuffleScalableContentKeys
OEM_TEE_DECRYPT_CalculateContentKeyPrimeWithAES128Key -> OEM_TEE_BASE_CalculateContentKeyPrimeWithAES128Key
OEM_TEE_DECRYPT_DeriveScalableKeyWithAES128Key -> OEM_TEE_BASE_DeriveScalableKeyWithAES128Key
OEM_TEE_DECRYPT_InitUplinkXKey -> OEM_TEE_BASE_InitUplinkXKey
OEM_TEE_DECRYPT_UpdateUplinkXKey -> OEM_TEE_BASE_UpdateUplinkXKey
OEM_TEE_DECRYPT_DecryptContentKeysWithDerivedKeys -> OEM_TEE_BASE_DecryptContentKeysWithDerivedKeys
OEM_TEE_DECRYPT_EnforcePolicy -> OEM_TEE_POLICY_Enforce
```


