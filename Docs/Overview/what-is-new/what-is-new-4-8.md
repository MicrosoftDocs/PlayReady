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

### CMake Build Infrastructure

Starting with PlayReady 4.8, the PlayReady Device Porting Kit includes CMake build infrastructure for Linux, macOS, and cross-platform targets. This provides a modern, flexible build system that supports multiple compilers and architectures out of the box, including cross-compilation for ARM64. For full instructions, see [Building with CMake](../cmake-build.md).

This is a new addition to the Device Porting Kit and we would love feedback from partners who use the new build system. Please reach out through your normal support channels with any suggestions or issues.

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

## Changes in PlayReady Device Porting Kit Version 4.8

### General Device Porting Kit changes

* Added new Activation v2 Protocol and point the activation URL at the new v2 endpoints.
* Added CMake Build Infrastructure for Linux and Cross-Platform targets.
* PK Module cleanup. Removed: `merkletree`, `mp4parser`, `provenance`, `provenancemanifest`, `utilities/map`, and `utilities/vector`.
* Various Bug fixes, including with the `DRM_TEE_PROPERTY_REQUIRES_MINIMAL_REVOCATION_DATA` TEE Property
* Security Improvements

