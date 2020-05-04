---
title: "How to Determine What Features a Client Supports"
description: This section describes how a server application can determine whether a client supports a given feature or not.
ms.assetid: "345F02F1-4233-4D60-81CB-7403702CFEF6"
keywords: playready server client feature support
ms.date: 10/02/2019
ms.topic: conceptual
---

# How to Determine What Features a Client Supports

Starting with PlayReady Device Porting Kit Version 4.4, the client sends information about what features it supports to the License Server as part of its license acquisition challenge. This includes both the Rich Execution Environment (REE) features and the Trusted Execution Environment (TEE) features.

Starting with PlayReady Server SDK Version 4.4, this information is made publically available to an application via the LicenseChallenge class. (Previous versions of the PlayReady Server SDK will ignore this information if present in the license acquisition challenge.) This page describes how to use this feature to make decisions in a server application based on what functionality the client has implemented.

Features are exposed through the LicenseChallenge class in three different catagories: TEE Properties, TEE APIs, and REE Features. In order to access an individual catagory of client features, you can use the properties of the License Challenge to get either a list of enums corresponding to each feature or access the raw XML containing feature information sent within the license challenge. The features exposed in the LicenseChallenge class as of version 4.4 are listed below with their corresponding enum values.

TeePropertyList:<br/>
    SUPPORTS_HEVC_HW_DECODING                            <br/>
    SUPPORTS_REMOTE_PROVISIONING                         <br/>
    SUPPORTS_PRE_PROCESS_ENCRYPTED_DATA                  <br/>
    REQUIRES_PRE_PROCESS_ENCRYPTED_DATA_WITH_FULL_FRAMES <br/>
    REQUIRES_SAMPLE_PROTECTION                           <br/>
    SUPPORTS_SECURE_CLOCK                                <br/>
    SUPPORTS_SECURE_STOP                                 <br/>
    SUPPORTS_SECURE_HDCP_TYPE_1                          <br/>
    REQUIRES_PREPARE_POLICY_INFO                         <br/>
    SUPPORTS_DEBUG_TRACING                               <br/>
    REQUIRES_MINIMAL_REVOCATION_DATA                     <br/>
    SUPPORTS_OPTIMIZED_CONTENT_KEY2                      <br/>

TeeApiList:<br/>
    DRM_TEE_BASE_AllocTEEContext                         <br/>
    DRM_TEE_BASE_FreeTEEContext                          <br/>
    DRM_TEE_BASE_SignDataWithSecureStoreKey              <br/>
    DRM_TEE_BASE_CheckDeviceKeys                         <br/>
    DRM_TEE_BASE_GetDebugInformation                     <br/>
    DRM_TEE_BASE_GenerateNonce                           <br/>
    DRM_TEE_BASE_GetSystemTime                           <br/>
    DRM_TEE_LPROV_GenerateDeviceKeys                     <br/>
    DRM_TEE_RPROV_GenerateBootstrapChallenge             <br/>
    DRM_TEE_RPROV_ProcessBootstrapResponse               <br/>
    DRM_TEE_RPROV_GenerateProvisioningRequest            <br/>
    DRM_TEE_RPROV_ProcessProvisioningResponse            <br/>
    DRM_TEE_LICPREP_PackageKey                           <br/>
    DRM_TEE_SAMPLEPROT_PrepareSampleProtectionKey        <br/>
    DRM_TEE_DECRYPT_PreparePolicyInfo                    <br/>
    DRM_TEE_DECRYPT_PrepareToDecrypt                     <br/>
    DRM_TEE_DECRYPT_CreateOEMBlobFromCDKB                <br/>
    DRM_TEE_AES128CTR_DecryptContent                     <br/>
    DRM_TEE_SIGN_SignHash                                <br/>
    DRM_TEE_DOM_PackageKeys                              <br/>
    DRM_TEE_RESERVED_20                                  <br/>
    DRM_TEE_RESERVED_21                                  <br/>
    DRM_TEE_RESERVED_22                                  <br/>
    DRM_TEE_RESERVED_23                                  <br/>
    DRM_TEE_REVOCATION_IngestRevocationInfo              <br/>
    DRM_TEE_LICGEN_CompleteLicense                       <br/>
    DRM_TEE_LICGEN_AES128CTR_EncryptContent              <br/>
    DRM_TEE_RESERVED_27                                  <br/>
    DRM_TEE_RESERVED_28                                  <br/>
    DRM_TEE_RESERVED_29                                  <br/>
    DRM_TEE_RESERVED_30                                  <br/>
    DRM_TEE_RESERVED_31                                  <br/>
    DRM_TEE_RESERVED_32                                  <br/>
    DRM_TEE_RESERVED_33                                  <br/>
    DRM_TEE_H264_PreProcessEncryptedData                 <br/>
    DRM_TEE_SECURESTOP_GetGenerationID                   <br/>
    DRM_TEE_AES128CTR_DecryptAudioContentMultiple        <br/>
    DRM_TEE_SECURETIME_GenerateChallengeData             <br/>
    DRM_TEE_SECURETIME_ProcessResponseData               <br/>
    DRM_TEE_AES128CTR_DecryptContentMultiple             <br/>
    DRM_TEE_AES128CBC_DecryptContentMultiple             <br/>
    DRM_TEE_SECURESTOP2_GetSigningKeyBlob                <br/>
    DRM_TEE_SECURESTOP2_SignChallenge                    <br/>
    DRM_TEE_BASE_GetFeatureInformation                   <br/>

ReeFeatureList:<br/>
    Assembly                                             <br/>
    PersistentStorePrealloc                              <br/>
    ECCProfiling                                         <br/>
    ForceAlign                                           <br/>
    InlineDwordCopy                                      <br/>
    FileLocking                                          <br/>
    MultiThreading                                       <br/>
    Native64BitTypes                                     <br/>
    PrecomputedECCGlobalTable                            <br/>
    Tracing                                              <br/>
    PersistentStoreWriteThrough                          <br/>
    AddLicenseWriteThrough                               <br/>
    NoOptimizations                                      <br/>
    DebugBuild                                           <br/>
    Profiling                                            <br/>
    Activation                                           <br/>
    AntirollbackClock                                    <br/>
    CDMI                                                 <br/>
    CleanStore                                           <br/>
    ErrorCodeContract                                    <br/>
    PKCRT                                                <br/>
    DeviceAssets                                         <br/>
    Domains                                              <br/>
    EmbeddedLicenseStore                                 <br/>
    PersistentStore                                      <br/>
    PersistentStoreBlockHeaderCache                      <br/>
    CDMIPersistentStore                                  <br/>
    ContentKeyGeneration                                 <br/>
    LocalLicenseGeneration                               <br/>
    MeteringCertificateRevocation                        <br/>
    Metering                                             <br/>
    ModelCertificateRevocation                           <br/>
    InMemoryOnlyLicenses                                 <br/>
    Performance                                          <br/>
    Reactivation                                         <br/>
    Revocation                                           <br/>
    SecureDelete                                         <br/>
    SecureStop                                           <br/>
    SecureStop2                                          <br/>
    SecureTime                                           <br/>
    StructuredSerialization                              <br/>
    XmlParsingCache                                      <br/>
    LicenseAcquisition                                   <br/>
    LegacyXmlCertificates                                <br/>
    AESCBCS                                              <br/>

There are a few common states that the LicenseChallenge class can be in with respect to the client feature set exposed.

* If the TeePropertyList, TeeApiList, and ReeFeatureList are all empty, then it means that the client is running a version of the PK older than 4.4.
* If the ReeFeatureList is non-empty and the TeePropertyList and TeeApiList are both empty, then it can mean one of two things.
    * On Windows clients, the client is either running in Software DRM or the client's TEE is older than PK version 4.4.
    * On non-Windows clients, the client's REE is running PK version 4.4+ but the client's TEE is older than PK version 4.4.
* If the TeePropertyList, TeeApiList, and ReeFeatureList are all non-empty, then the client is running PK version 4.4+ for all components.
    * Note: The TeePropertyList and TeeApiList are provided by the client's TEE and can be trusted to its security level.

<br/><br/>

