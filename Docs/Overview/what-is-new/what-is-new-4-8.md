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

### Activation v2 Protocol

PlayReady 4.8 introduces an updated Activation v2 protocol for device individualization. The new protocol uses a new XML-based challenge/response format under the `ActivationService/v2` namespace and points to updated activation endpoints. Activation v2 also introduces a v1-to-v2 reactivation path, allowing devices that were previously individualized using the legacy activation protocol to seamlessly transition to the new protocol. The legacy Activation v1 protocol remains functional for existing devices but is no longer the default for new activations on supported platforms.

### OP-TEE Platform Support

PlayReady 4.8 adds full platform support for OP-TEE (Open Portable Trusted Execution Environment), enabling PlayReady to run as a trusted application within ARM TrustZone-based TEEs. The OP-TEE platform includes OEM-layer implementations for file I/O, cryptography, secure time, device model identification, and tracing, as well as a TEE bridge and broker trusted application. A Buildroot external package is provided for streamlined integration into embedded Linux build systems. Comprehensive documentation is included covering integration, quick start, and troubleshooting guidance.

## Changes in PlayReady Server SDK Version 4.8

### General Server Changes

* The .NET Framework version is fully deprecated. This is the first release where it is not included.
* The Certificate Revocation List must now be downloaded from a new URL, your choice of https://go.microsoft.com/fwlink/?LinkId=2359173 or https://aka.ms/revinfo2.
* Converted PlayReady Server SDK Samples to run on .NET Core
* Added a revoked query syntax argument to the CfgHandler to simulate device revocation.
* Improved XML Validation for the License Server Time challenge.

### Server API Changes

There have been no changes to the Server API.

## Changes in PlayReady Device Porting Kit Version 4.8

### General Device Porting Kit changes

* Added new Activation v2 Protocol and point the activation URL at the new v2 endpoints.
* Full OP-TEE (ARM TrustZone TEE) platform added.
* Added CMake Build Infrastructure for Linux and Cross-Platform targets.
* Provenance PK Module cleanup. Removed: `merkletree`, `mp4parser`, `provenance`, `provenancemanifest`, `utilities/map`, and `utilities/vector`.
* Various Bug fixes, including with the `DRM_TEE_PROPERTY_REQUIRES_MINIMAL_REVOCATION_DATA` TEE Property

