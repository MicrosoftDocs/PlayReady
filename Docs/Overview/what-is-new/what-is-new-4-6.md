---
title: What's New in PlayReady Version 4.6
description: This section provides an overview of changes from PlayReady version 4.5 to PlayReady version 4.6.
ms.assetid: "BD2B7B22-18AA-4029-BD64-41D9B79E6B23"
keywords: playready overview version changes 4.5 4.6
ms.date: 11/17/2022
ms.topic: conceptual
---

# What's New in PlayReady Version 4.6

This page contains an overview of the most significant changes between PlayReady version 4.5 and PlayReady version 4.6.

## General Changes in PlayReady Version 4.6

### Key Exchange

Starting with PlayReady 4.6, a single Key Exchange license can include multiple keys with different algorithms.

## Changes in PlayReady Server SDK Version 4.6

### General Server Changes

* The .NET Core SDK was migrated to .NET version 6.0.
* Key Exchange licenses can now include multiple keys with different algorithms.

### Server API Changes

This is merely an overview. Refer to the [Server API documentation](/dotnet/api/Microsoft.Media.Drm) for more information.

* The LicenseChallengeReeFeatures enum now includes value KeyExchangeMultiple.
* The KeyExchangeLicense class method AddRight can now be called multiple times with different KeyExchangeRight instances with different algorithms if the challenge's ReeFeatureList contains LicenseChallengeReeFeatures.KeyExchangeMultiple.
* IPackagingDataAcquisitionHandler has been added to .NET Core version. .NET Core Server SDK was originally released without this functionality. It was added back to close this functionality gap between the Legacy and .NET Core editions.
* IServerAuthorization now includes OnServerCertificateParsed. This method is called after the Server Certificate is validated by Server SDK. If validation succeeded, the certificate object is provided to the handler; otherwise, the validation exception is provided.

## Changes in PlayReady Device Porting Kit Version 4.6

### General Device Porting Kit changes

* More unsupported codepaths only used in Microsoft-internal implementations were removed to eliminate confusion and reduce compile times and binary sizes.
* Code was moved across various files to enable linkers to do better optimization.
* A single KeyExchangeLicense with multiple different algorithms will be properly handled.
* The xmrlicensetoxml.exe tool and source code were added.
* All memory allocation functions such as Oem_MemAlloc now take sizes based on the architecture of the system (32bit or 64bit) instead of always taking 32bit sizes.
* A memory leak in Drm_SecureDelete_GenerateChallenge was fixed.
* The drmmanager test area was broken up into numerous separate test areas to make logs easier to navigate. As a single test area, the log file was enormous.

### Device Porting Kit API changes

This is merely an overview. Refer to the API documentation provided in the associated code comments in the [PlayReady Device Porting Kit](/playready/overview/device-porting-kit) for more information.

The following OEM REE and TEE APIs were changed to use a DRM_SIZE_T instead of a DRM_DWORD for sizes.

* Oem_MemAlloc
* Oem_Broker_MemAlloc
* OEM_TEE_BASE_SecureMemAlloc
* DRMCRT_ScrubMemory
* DRMCRT_LocalMemcpy
* DRMCRT_LocalMemset
* DRMCRT_LocalDWORDSetZero
* DRMCRT_LocalAreEqual
* DRMCRT_LocalDWORDcpy

The following OEM REE APIs were added:

* Oem_Device_GetClientOSInformation (optional).

The following OEM TEE APIs were changed:

* OEM_TEE_BASE_SecureMemHandleFree now returns DRM_RESULT instead of DRM_VOID.
* OEM_TEE_RPROV_WrapProvisioningRequest now includes the session key on input when available.


