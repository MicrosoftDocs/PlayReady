---
title: What's New in PlayReady Version 4.8
description: This section provides an overview of changes from PlayReady version 4.7 to PlayReady version 4.8.
ms.assetid: "01882315-8FFE-49EB-A7D6-69EC3E702FFF"
keywords: playready overview version changes 4.7 4.8
ms.date: 4/14/2026
ms.topic: whats-new
---

# What's New in PlayReady Version 4.8

This page provides an overview of the most significant changes between PlayReady version 4.7 and PlayReady version 4.8.

## General Changes in PlayReady Version 4.8

### Certificate Revocation List Improvements

Starting with PlayReady 4.8, PlayReady Server SDK Clients will use a new certificate revocation list, downloaded from your choice of https://go.microsoft.com/fwlink/?LinkId=2359173 or https://aka.ms/revinfo2. This new certificate revocation list greatly improves performance and reduces strain on the PlayReady Porting Kit implementations of all versions. Please note that the download URL changed for 4.8 and future clients of the PlayReady Server SDK, but the download URL is unchanged for 4.7 and earlier clients. A failure to use the correct revocation list for 4.8 and future versions will result in a PlayReady Server Software Development Kit error to be thrown. A failure to use the correct revocation list for 4.7 and earlier versions will produce no error but  will result in your server offering fewer protections.

Porting Kit implementers can now safely use the TEE property `DRM_TEE_PROPERTY_REQUIRES_MINIMAL_REVOCATION_DATA` in order to reduce the size of the revocation data package passed into the TEE when building the RKB. 

### ECC Validation Patch Detection Improvements (4.8.95 QFE)

Added more ways for Device PK clients to communicate they have the ECC Patch to the Server SDK. In addition to updating your Company Certificate to use our new ECC Patch Root, clients can also use the TEE Property `DRM_TEE_PROPERTY_SUPPORTS_ECC_POINT_VALIDATION` with the 4.8.95 QFE Device PK, or update their Device Certificate's Model Name to include the string `[ECV]` on any Device PK version.

A new boolean property `IsECCPatched` has been added to the `ILicenseChallenge` interface. This property will perform the three checks described above and will be set to `true` if **any** of them are true.

## Changes in PlayReady Server SDK Version 4.8

### General Server Changes

* The .NET Framework version is fully deprecated. This is the first release where it is not included.
* The Certificate Revocation List must now be downloaded from a new URL, your choice of https://go.microsoft.com/fwlink/?LinkId=2359173 or https://aka.ms/revinfo2.
* Converted PlayReady Server SDK Samples to run on .NET Core
  * Added Samples for Extended Restriction and Limited Duration Chained Licenses. Removed AES Packaging, Static Reheadering, and CfgHandler.Legacy Samples
* Added a revoked query syntax argument to the CfgHandler to simulate device revocation.
* Improved XML Validation for the License Server Time challenge.
* Security Improvements

### Server API Changes

There have been no changes to the Server API.

### 4.8.95 QFE Patch Notes

The following changes were made in the 4.8.95 patch:

* General bug fixes around ECC Validation to improve support for Legacy PlayReady Clients.
* Bug fixes around reading Wide Strings as Narrow, which caused many Certificate fields to include null escape characters.
* Added boolean `IsECCPatched` property to the `ILicenseChallenge` interface that reflects if the the client has taken the ECC Patch yet.
  * All checks for ECC Vulnerability presence should use this property
* Expose the new TEE Property as `LicenseChallengeTeeProperties.SUPPORTS_ECC_POINT_VALIDATION` in the `ILicenseChallenge`'s `TeePropertyList` property.
* Added a `eccpatch` query syntax argument to the CfgHandler to simulate ECC Patch enforcement.
  * Treats devices without the ECC Patch as revoked.
* Add proper error handling to validate and handle invalid client SOAP requests.

## Changes in PlayReady Device Porting Kit Version 4.8

### General Device Porting Kit changes

* Added CMake Build Infrastructure for Linux and Cross-Platform targets.
* Various Bug fixes, including with the `DRM_TEE_PROPERTY_REQUIRES_MINIMAL_REVOCATION_DATA` TEE Property
* Security Improvements

### 4.8.95 QFE Patch Notes

* Added the ECC Validation Test to the `pritee_test_utility`.
* Expose a new TEE Property, `DRM_TEE_PROPERTY_SUPPORTS_ECC_POINT_VALIDATION`, which can be used to show the device has taken the ECC Patch.

