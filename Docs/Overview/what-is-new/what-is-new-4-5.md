---
title: What's New in PlayReady Version 4.5
description: This section provides an overview of changes from PlayReady version 4.4 to PlayReady version 4.5.
ms.assetid: "578AA33C-54BD-453B-BAD6-B5C67A586B6F"
keywords: playready overview version changes 4.4 4.5
ms.date: 10/22/2021
ms.topic: whats-new
---

# What's New in PlayReady Version 4.5

This page contains an overview of the most significant changes between PlayReady version 4.4 and PlayReady version 4.5.

## General Changes in PlayReady Version 4.5

### Challenge Encryption with PlayReady Server Deployment Certificate

In previous versions of PlayReady, license acquisition and other client challenges are always privacy-encrypted with a fixed public key. Starting with PlayReady 4.5, a client that is coded to talk only to a supporting server may instead privacy-encrypt challenges with the PlayReady Server Deployment Certificate issued to the server licensee by Microsoft. The PlayReady Server SDK then decrypts the challenge with the corresponding private key, passed to it by the PlayReady Server SDK application, instead of a fixed private key.

### License Server Time

In previous versions of PlayReady, using the Secure Time feature usually required the client application to talk to a separate Secure Time server to obtain the time used to set its local clock. Starting with PlayReady 4.5, a client that is coded to talk only to a supporting server may instead use a time provided by the PlayReady Server SDK during license acquisition. For more information, see [PlayReady Trusted Clocks](../../Features/trusted-clocks.md).

### Key Exchange

Using the license acquisition protocol, a PlayReady client and server may now exchange arbitrary keys which can be used to encrypt, decrypt, sign, and verify arbitrary application-provided data where the keys themselves are protected using PlayReady. When the client is SL3000, the keys themselves are protected by the Trusted Execution Environment. For more information, see [PlayReady Key Exchange](../../Features/key-exchange.md).

### Watermarking Policy

Functionality was added to simplify use of the Watermarking Signalling Explicit Digital Video Output Restriction as defined by the PlayReady Compliance Rules.

## Changes in PlayReady Server SDK Version 4.5

### General Server Changes

Key Exchange licenses can be used to provide arbitrary keys to a client during license acquisition.

If provided by the client, the supported watermarking technologies are exposed to the PlayReady Server SDK application. This simplifies use of the Watermarking Signalling Explicit Digital Video Output Restriction as defined by the PlayReady Compliance Rules.

### Server API Documentation Changes

New [Server API documentation](/dotnet/api/Microsoft.Media.Drm) for the [.NET Standard](/dotnet/standard/net-standard) version of the PlayReady Server SDK has been created and published. Microsoft recommends migrating to the .NET Standard SDK.

The Server API documentation in the PlayReady.chm file included in the PlayReady Documentation Pack only applies to the legacy .NET Framework version of the PlayReady Server SDK.  This documentation is now considered deprecated, has not been updated since PlayReady 4.0, and will not receive future updates.

Most APIs in the two SDKs are identical, so the .NET Standard documentation should be sufficient for most purposes.  However, there are a few significant differences where classes, interfaces, and methods differ.

Here are the general differences between the two SDKs.

   1. The .NET Standard SDK uses interfaces in many places where the .NET Framework SDK uses classes.

   1. The .NET Standard SDK handler interfaces implemented by the application uses asynchronous methods where the .NET Framework SDK uses synchronous methods.  Therefore, the .Net Standard SDK handler interface API names end with the word "Async" and return a Task\<class\> instead of simply class (where class is specific to the handler interface method).

   1. The .NET Standard SDK is transport agnostic. As such, no HTTP context is directly provided to the application. When using ASP.NET Core, refer to the ASP.NET Core documentation, especially the [IHttpContextAccessor Interface](/dotnet/api/microsoft.aspnetcore.http.ihttpcontextaccessor).

   1. The .NET Standard SDK does not support the packaging content protocol (e.g. IPackagingDataAcquisitionHandler does not exist). This functionality will be restored in PlayReady 4.6.

Here is a complete list of the specific differences as of PlayReady 4.5. This list does not include functionality that only exists in the .NET Standard SDK nor does it list all of the packaging classes removed which will be restored.

&nbsp;

| .NET Framework class or interface | .NET Standard equivalent | Differences |
|:---|:---|:---|
| ProtocolChallengeContext class | IProtocolChallengeContext interface | The HttpRequest Request property only exists in the .NET Framework SDK as discussed above. |
| ProtocolChallenge class | IProtocolChallenge interface | None. |
| IDeleteLicenseHandler interface | Same | ProcessDeleteLicenseDataAsync is synchronous in the .NET Framework SDK as discussed above. |
| DeleteLicenseDataChallenge class | IDeleteLicenseDataChallenge interface | None. |
| IDomainHandler interface | Same | HandleJoinDomainAsync and HandleLeaveDomainAsync are synchronous in the .NET Framework SDK as discussed above. |
| JoinDomainChallenge class | IDomainChallenge and IJoinDomainChallenge interfaces | The static JoinDomainChallenge.GenerateDomainKeyPair method does not exist in the .NET Standard SDK. The loss of this functionality is a bug that will be fixed in PlayReady 4.6 by adding it as a static method to DomainCertificateBuilder. |
| LeaveDomainChallenge class | ILeaveDomainChallenge interface | None. |
| ILicenseAcknowledgementHandler interface | Same | HandleLicenseAcknowledgementAsync is synchronous in the .NET Framework SDK as discussed above. |
| LicenseAcknowledgementChallenge class | ILicenseAcknowledgementChallenge interface | None. |
| ILicenseAcquisitionHandler interface | Same | HandleLicenseAcquisitionAsync is synchronous in the .NET Framework SDK as discussed above. |
| LicenseChallenge class | ILicenseChallenge interface | None. |
| IMeteringHandler interface | Same | GetMeteringCertificateAsync and ProcessMeteringDataAsync are synchronous in the .NET Framework SDK as discussed above. |
| MeteringCertificateChallenge class | IMeteringCertificateChallenge interface | None. |
| ProcessMeteringDataChallenge class | IProcessMeteringDataChallenge interface | None. |
| ISecureStopHandler interface | Same | ProcessSecureStopDataAsync is synchronous in the .NET Framework SDK as discussed above. |
| SecureStopDataChallenge class | ISecureStopDataChallenge interface | The GetSecureStopData method overload that takes an ISecureStop2Handler only exists in the .NET Framework SDK. The .NET Standard SDK instead loads this handler like any other. |
| ISecureStopHandler2 interface | Same | GetSecureStop2AESKeyAsync is synchronous in the .NET Framework SDK as discussed above. |
| PlayReadyServerAuthorization class | Same | The class's methods are static in the .NET Framework SDK and instance in the .NET Standard SDK. |

### Server API Changes

This is merely an overview. Refer to the [Server API documentation](/dotnet/api/Microsoft.Media.Drm) for more information.

The LicenseResponse.GetLicenses method now returns an empty array instead of null when no licenses have been added.

The following classes and enums were added.

* AdvancedLicense class (abstract, inherits from License) - a subset existing properties and methods from MediaLicense were moved into this class, and MediaLicense now inherits from AbstractLicense. No application changes are required to use MediaLicense.
* KeyExchangeLicense class (inherits from AdvancedLicense) - used to create licenses that provide arbitrary keys to a client during license acquisition.
* KeyExchangeRight class (inherits from Right) - used to specify the key and its allowed usage to a KeyExchange license.
* KeyExchangeAlgorithm enum - used to specify the allowed usage for a key in a KeyExchange license.
* WatermarkVendor class - used to expose the client's supported watermarking technologies to the application.
* LicenseServerTimeCertificate class - used to contain the certificate for signing the license server time returned in the license acquisition response.

The following were added to individual classes.

* The PlayReadyHeader class exposes whether the header indicates support for per-stream keys and whether it explicitly requests a license or not.
* The ContentKeyType enum adds the value KeyExchange.
* The Certificate class adds byte array properties exposing the certificate's digest and issuer public key.
* The License class adds a guid property exposing the license's unique id and an IEnumerable\<Right\> property to return the rights that were added to the license.
* The LicenseChallengeTeeAPIs enum adds values for all new PK 4.5 TEE APIs.
* The LicenseChallengeReeFeatures enum adds values for LicenseServerTime and KeyExchange.
* The LicenseChallenge class adds the list of KeyExchangeAlgorithms the client supports, the WatermarkVendors the client supports, the PK versions of the client's TEE and REE (which may or may not be the same), and whether the client requires the current LicenseServerTime.
* The LicenseResponse class adds a LicenseServerTimeCertificate property for setting the certificate used to sign the License Server Time returned in the license acquisition response.
* The ExplicitOutputRestrictionsConstants class adds constants for Watermark and InternalScreenOnly. Refer to the PlayReady Compliance Rules for more information on these guids.

## Changes in PlayReady Device Porting Kit Version 4.5

### General Device Porting Kit changes

* The entire PlayReady Device Porting Kit has been updated to Microsoft Source-code Annotation Language (SAL) 2.0.
* Some unsupported codepaths only used in Microsoft-internal implementations were removed to eliminate confusion and reduce compile times and binary sizes. Further improvements in this area is expected to be included in future releases.
* Where supported by the underlying compiler and machine architecture, native 128-bit integer types can now be used to accelerate the default implementation of ECC256.
* A default implementation of the SHA256 HMAC algorithm was added.

### Device Porting Kit API changes

This is merely an overview. Refer to the API documentation provided in the associated code comments in the [PlayReady Device Porting Kit](/playready/overview/device-porting-kit) for more information.

DRM_CDMI_SetServercertificate is now allowed to be called with a PlayReady Server Deployment Certificate for privacy-encrypting license acquisition and other client challenges. The function forwards to Drm_AppContext_SetProperty in this scenario. Existing usage remains as-is.

The following public functions were added:

* Drm_AppContext_SetProperty
* Drm_KeyExchange_Prepare
* Drm_KeyExchange_Perform
* Drm_KeyExchange_Close

The following structures were added:

* DRM_DGP_REE_FEATURE_LIST_4_5
* DRM_DGP_TEE_API_LIST_4_5

The following TEE APIs were added:

* DRM_TEE_BASE_GetSystemTime2
* DRM_TEE_LICPREP_PackageKey2
* DRM_TEE_LICENSESERVERTIME_ProcessResponseData
* DRM_TEE_DECRYPT_PrepareToDecrypt2
* DRM_TEE_LICGEN_CompleteLicense2
* DRM_TEE_KEYEXCHANGE_Prepare
* DRM_TEE_KEYEXCHANGE_Perform

The following OEM TEE APIs were added:

* OEM_TEE_BASE_ECC256_SetKey
* OEM_TEE_CRYPTO_SHA256_HMAC_VerifyMAC
* OEM_TEE_CRYPTO_SHA256_HMAC_CreateMAC
* OEM_TEE_PERSISTENTSTORAGE_Read
* OEM_TEE_PERSISTENTSTORAGE_Write
* OEM_TEE_GetSupportedWatermarkVendors

The following OEM TEE APIs were renamed without functional changes:

| Old name                                              | New name                                           |
|-------------------------------------------------------|----------------------------------------------------|
| OEM_TEE_DECRYPT_UnshuffleScalableContentKeys          | OEM_TEE_BASE_UnshuffleScalableContentKeys          |
| OEM_TEE_DECRYPT_CalculateContentKeyPrimeWithAES128Key | OEM_TEE_BASE_CalculateContentKeyPrimeWithAES128Key |
| OEM_TEE_DECRYPT_DeriveScalableKeyWithAES128Key        | OEM_TEE_BASE_DeriveScalableKeyWithAES128Key        |
| OEM_TEE_DECRYPT_InitUplinkXKey                        | OEM_TEE_BASE_InitUplinkXKey                        |
| OEM_TEE_DECRYPT_UpdateUplinkXKey                      | OEM_TEE_BASE_UpdateUplinkXKey                      |
| OEM_TEE_DECRYPT_DecryptContentKeysWithDerivedKeys     | OEM_TEE_BASE_DecryptContentKeysWithDerivedKeys     |
| OEM_TEE_DECRYPT_EnforcePolicy                         | OEM_TEE_POLICY_Enforce                             |
