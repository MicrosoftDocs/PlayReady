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

TeePropertyList:
    SUPPORTS_HEVC_HW_DECODING                            => 0
    SUPPORTS_REMOTE_PROVISIONING                         => 1
    SUPPORTS_PRE_PROCESS_ENCRYPTED_DATA                  => 2
    REQUIRES_PRE_PROCESS_ENCRYPTED_DATA_WITH_FULL_FRAMES => 3
    REQUIRES_SAMPLE_PROTECTION                           => 4
    SUPPORTS_SECURE_CLOCK                                => 5
    SUPPORTS_SECURE_STOP                                 => 6
    SUPPORTS_SECURE_HDCP_TYPE_1                          => 7
    REQUIRES_PREPARE_POLICY_INFO                         => 8
    SUPPORTS_DEBUG_TRACING                               => 9
    REQUIRES_MINIMAL_REVOCATION_DATA                     => 10
    SUPPORTS_OPTIMIZED_CONTENT_KEY2                      => 11

TeeApiList:
    DRM_TEE_BASE_AllocTEEContext                         => 0
    DRM_TEE_BASE_FreeTEEContext                          => 1
    DRM_TEE_BASE_SignDataWithSecureStoreKey              => 2
    DRM_TEE_BASE_CheckDeviceKeys                         => 3
    DRM_TEE_BASE_GetDebugInformation                     => 4
    DRM_TEE_BASE_GenerateNonce                           => 5
    DRM_TEE_BASE_GetSystemTime                           => 6
    DRM_TEE_LPROV_GenerateDeviceKeys                     => 7
    DRM_TEE_RPROV_GenerateBootstrapChallenge             => 8
    DRM_TEE_RPROV_ProcessBootstrapResponse               => 9
    DRM_TEE_RPROV_GenerateProvisioningRequest            => 10
    DRM_TEE_RPROV_ProcessProvisioningResponse            => 11
    DRM_TEE_LICPREP_PackageKey                           => 12
    DRM_TEE_SAMPLEPROT_PrepareSampleProtectionKey        => 13
    DRM_TEE_DECRYPT_PreparePolicyInfo                    => 14
    DRM_TEE_DECRYPT_PrepareToDecrypt                     => 15
    DRM_TEE_DECRYPT_CreateOEMBlobFromCDKB                => 16
    DRM_TEE_AES128CTR_DecryptContent                     => 17
    DRM_TEE_SIGN_SignHash                                => 18
    DRM_TEE_DOM_PackageKeys                              => 19
    DRM_TEE_RESERVED_20                                  => 20
    DRM_TEE_RESERVED_21                                  => 21
    DRM_TEE_RESERVED_22                                  => 22
    DRM_TEE_RESERVED_23                                  => 23
    DRM_TEE_REVOCATION_IngestRevocationInfo              => 24
    DRM_TEE_LICGEN_CompleteLicense                       => 25
    DRM_TEE_LICGEN_AES128CTR_EncryptContent              => 26
    DRM_TEE_RESERVED_27                                  => 27
    DRM_TEE_RESERVED_28                                  => 28
    DRM_TEE_RESERVED_29                                  => 29
    DRM_TEE_RESERVED_30                                  => 30
    DRM_TEE_RESERVED_31                                  => 31
    DRM_TEE_RESERVED_32                                  => 32
    DRM_TEE_RESERVED_33                                  => 33
    DRM_TEE_H264_PreProcessEncryptedData                 => 34
    DRM_TEE_SECURESTOP_GetGenerationID                   => 35
    DRM_TEE_AES128CTR_DecryptAudioContentMultiple        => 36
    DRM_TEE_SECURETIME_GenerateChallengeData             => 37
    DRM_TEE_SECURETIME_ProcessResponseData               => 38
    DRM_TEE_AES128CTR_DecryptContentMultiple             => 39
    DRM_TEE_AES128CBC_DecryptContentMultiple             => 40
    DRM_TEE_SECURESTOP2_GetSigningKeyBlob                => 41
    DRM_TEE_SECURESTOP2_SignChallenge                    => 42
    DRM_TEE_BASE_GetFeatureInformation                   => 43

ReeFeatureList:
    Assembly                                             => 0
    PersistentStorePrealloc                              => 1
    ECCProfiling                                         => 2
    ForceAlign                                           => 3
    InlineDwordCopy                                      => 4
    FileLocking                                          => 5
    MultiThreading                                       => 6
    Native64BitTypes                                     => 7
    PrecomputedECCGlobalTable                            => 8
    Tracing                                              => 9
    PersistentStoreWriteThrough                          => 10
    AddLicenseWriteThrough                               => 11
    NoOptimizations                                      => 12
    DebugBuild                                           => 13
    Profiling                                            => 14
    Activation                                           => 15
    AntirollbackClock                                    => 16
    CDMI                                                 => 17
    CleanStore                                           => 18
    ErrorCodeContract                                    => 19
    PKCRT                                                => 20
    DeviceAssets                                         => 21
    Domains                                              => 22
    EmbeddedLicenseStore                                 => 23
    PersistentStore                                      => 24
    PersistentStoreBlockHeaderCache                      => 25
    CDMIPersistentStore                                  => 26
    ContentKeyGeneration                                 => 27
    LocalLicenseGeneration                               => 28
    MeteringCertificateRevocation                        => 29
    Metering                                             => 30
    ModelCertificateRevocation                           => 31
    InMemoryOnlyLicenses                                 => 32
    Performance                                          => 33
    Reactivation                                         => 34
    Revocation                                           => 35
    SecureDelete                                         => 36
    SecureStop                                           => 37
    SecureTime                                           => 38
    StructuredSerialization                              => 39
    XmlParsingCache                                      => 40
    LicenseAcquisition                                   => 41
    LegacyXmlCertificates                                => 42
    AESCBCS                                              => 43

There are a few common states that the LicenseChallenge class can be in with respect to the client feature set exposed. If the TeePropertyList, TeeApiList, and ReeFeatureList are all empty, then it means that the client is running a version of the PK older than 4.3. If the ReeFeatureList is non-empty and the TeePropertyList and TeeApiList are both empty, then it can mean one of two things. The client is either running in Software DRM, or the client's PK is version 4.3+ but with an old TEE. Finally, if the TeePropertyList, TeeApiList, and ReeFeatureList are all non-empty, then the client is running PK version 4.3+ with an updated TEE in Hardware DRM.

<br/><br/>

