---
title: "How to Determine What Features a Client Supports"
description: This section describes how a server application can determine whether a client supports a given feature or not.
ms.assetid: "345F02F1-4233-4D60-81CB-7403702CFEF6"
keywords: playready server client feature support
ms.date: 10/02/2019
ms.topic: conceptual
---

# How to Determine What Features a Client Supports

Starting with PlayReady Device Porting Kit Version 4.3, the client sends information about what features it supports to the License Server as part of its license acquisition challenge.  Starting with PlayReady Server SDK Version 4.3, this information is made publically available to an application via the LicenseChallenge class.  (Previous versions of the PlayReady Server SDK will ignore this information if present in the license acquisition challenge.)  This page describes how to use this feature to make decisions in a server application based on what functionality the client has implemented.

Features are exposed through the LicenseChallenge class in three different catagories: TEE Properties, TEE APIs, and REE Features. In order to access an individual catagory of client features, you can use the properties of the License Challenge to get either a list of enums corresponding to each feature or access the raw XML containing feature information sent within the license challenge. The current features exposed in the LicenseChallenge class are listed below with their corresponding enum values.

TeePropertyList:<br/>
    SUPPORTS_HEVC_HW_DECODING                            => 0<br/>
    SUPPORTS_REMOTE_PROVISIONING                         => 1<br/>
    SUPPORTS_PRE_PROCESS_ENCRYPTED_DATA                  => 2<br/>
    REQUIRES_PRE_PROCESS_ENCRYPTED_DATA_WITH_FULL_FRAMES => 3<br/>
    REQUIRES_SAMPLE_PROTECTION                           => 4<br/>
    SUPPORTS_SECURE_CLOCK                                => 5<br/>
    SUPPORTS_SECURE_STOP                                 => 6<br/>
    SUPPORTS_SECURE_HDCP_TYPE_1                          => 7<br/>
    REQUIRES_PREPARE_POLICY_INFO                         => 8<br/>
    SUPPORTS_DEBUG_TRACING                               => 9<br/>
    REQUIRES_MINIMAL_REVOCATION_DATA                     => 10<br/>
    SUPPORTS_OPTIMIZED_CONTENT_KEY2                      => 11<br/>

TeeApiList:<br/>
    DRM_TEE_BASE_AllocTEEContext                         => 0<br/>
    DRM_TEE_BASE_FreeTEEContext                          => 1<br/>
    DRM_TEE_BASE_SignDataWithSecureStoreKey              => 2<br/>
    DRM_TEE_BASE_CheckDeviceKeys                         => 3<br/>
    DRM_TEE_BASE_GetDebugInformation                     => 4<br/>
    DRM_TEE_BASE_GenerateNonce                           => 5<br/>
    DRM_TEE_BASE_GetSystemTime                           => 6<br/>
    DRM_TEE_LPROV_GenerateDeviceKeys                     => 7<br/>
    DRM_TEE_RPROV_GenerateBootstrapChallenge             => 8<br/>
    DRM_TEE_RPROV_ProcessBootstrapResponse               => 9<br/>
    DRM_TEE_RPROV_GenerateProvisioningRequest            => 10<br/>
    DRM_TEE_RPROV_ProcessProvisioningResponse            => 11<br/>
    DRM_TEE_LICPREP_PackageKey                           => 12<br/>
    DRM_TEE_SAMPLEPROT_PrepareSampleProtectionKey        => 13<br/>
    DRM_TEE_DECRYPT_PreparePolicyInfo                    => 14<br/>
    DRM_TEE_DECRYPT_PrepareToDecrypt                     => 15<br/>
    DRM_TEE_DECRYPT_CreateOEMBlobFromCDKB                => 16<br/>
    DRM_TEE_AES128CTR_DecryptContent                     => 17<br/>
    DRM_TEE_SIGN_SignHash                                => 18<br/>
    DRM_TEE_DOM_PackageKeys                              => 19<br/>
    DRM_TEE_RESERVED_20                                  => 20<br/>
    DRM_TEE_RESERVED_21                                  => 21<br/>
    DRM_TEE_RESERVED_22                                  => 22<br/>
    DRM_TEE_RESERVED_23                                  => 23<br/>
    DRM_TEE_REVOCATION_IngestRevocationInfo              => 24<br/>
    DRM_TEE_LICGEN_CompleteLicense                       => 25<br/>
    DRM_TEE_LICGEN_AES128CTR_EncryptContent              => 26<br/>
    DRM_TEE_RESERVED_27                                  => 27<br/>
    DRM_TEE_RESERVED_28                                  => 28<br/>
    DRM_TEE_RESERVED_29                                  => 29<br/>
    DRM_TEE_RESERVED_30                                  => 30<br/>
    DRM_TEE_RESERVED_31                                  => 31<br/>
    DRM_TEE_RESERVED_32                                  => 32<br/>
    DRM_TEE_RESERVED_33                                  => 33<br/>
    DRM_TEE_H264_PreProcessEncryptedData                 => 34<br/>
    DRM_TEE_SECURESTOP_GetGenerationID                   => 35<br/>
    DRM_TEE_AES128CTR_DecryptAudioContentMultiple        => 36<br/>
    DRM_TEE_SECURETIME_GenerateChallengeData             => 37<br/>
    DRM_TEE_SECURETIME_ProcessResponseData               => 38<br/>
    DRM_TEE_AES128CTR_DecryptContentMultiple             => 39<br/>
    DRM_TEE_AES128CBC_DecryptContentMultiple             => 40<br/>
    DRM_TEE_SECURESTOP2_GetSigningKeyBlob                => 41<br/>
    DRM_TEE_SECURESTOP2_SignChallenge                    => 42<br/>
    DRM_TEE_BASE_GetFeatureInformation                   => 43<br/>

ReeFeatureList:<br/>
    Assembly                                             => 0<br/>
    PersistentStorePrealloc                              => 1<br/>
    ECCProfiling                                         => 2<br/>
    ForceAlign                                           => 3<br/>
    InlineDwordCopy                                      => 4<br/>
    FileLocking                                          => 5<br/>
    MultiThreading                                       => 6<br/>
    Native64BitTypes                                     => 7<br/>
    PrecomputedECCGlobalTable                            => 8<br/>
    Tracing                                              => 9<br/>
    PersistentStoreWriteThrough                          => 10<br/>
    AddLicenseWriteThrough                               => 11<br/>
    NoOptimizations                                      => 12<br/>
    DebugBuild                                           => 13<br/>
    Profiling                                            => 14<br/>
    Activation                                           => 15<br/>
    AntirollbackClock                                    => 16<br/>
    CDMI                                                 => 17<br/>
    CleanStore                                           => 18<br/>
    ErrorCodeContract                                    => 19<br/>
    PKCRT                                                => 20<br/>
    DeviceAssets                                         => 21<br/>
    Domains                                              => 22<br/>
    EmbeddedLicenseStore                                 => 23<br/>
    PersistentStore                                      => 24<br/>
    PersistentStoreBlockHeaderCache                      => 25<br/>
    CDMIPersistentStore                                  => 26<br/>
    ContentKeyGeneration                                 => 27<br/>
    LocalLicenseGeneration                               => 28<br/>
    MeteringCertificateRevocation                        => 29<br/>
    Metering                                             => 30<br/>
    ModelCertificateRevocation                           => 31<br/>
    InMemoryOnlyLicenses                                 => 32<br/>
    Performance                                          => 33<br/>
    Reactivation                                         => 34<br/>
    Revocation                                           => 35<br/>
    SecureDelete                                         => 36<br/>
    SecureStop                                           => 37<br/>
    SecureTime                                           => 38<br/>
    StructuredSerialization                              => 39<br/>
    XmlParsingCache                                      => 40<br/>
    LicenseAcquisition                                   => 41<br/>
    LegacyXmlCertificates                                => 42<br/>
    AESCBCS                                              => 43<br/>

There are a few common states that the LicenseChallenge class can be in with respect to the client feature set exposed.

* If the TeePropertyList, TeeApiList, and ReeFeatureList are all empty, then it means that the client is running a version of the PK older than 4.3.
* If the ReeFeatureList is non-empty and the TeePropertyList and TeeApiList are both empty, then it can mean one of two things.
    * On Windows clients, the client is either running in Software DRM or the client's TEE is older than PK version 4.3.
    * On non-Windows clients, the client's REE is running PK version 4.3+ but the client's TEE is older than PK version 4.3.
* If the TeePropertyList, TeeApiList, and ReeFeatureList are all non-empty, then the client is running PK version 4.3+ for all components.

<br/><br/>

