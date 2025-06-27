---
title: What's New in PlayReady Version 4.7
description: This section provides an overview of changes from PlayReady version 4.6 to PlayReady version 4.7.
ms.assetid: "A10B5956-D837-4789-883A-9E855AD93841"
keywords: playready overview version changes 4.6 4.7
ms.date: 7/1/2025
ms.topic: whats-new
---

# What's New in PlayReady Version 4.7

This page provides an overview of the most significant changes between PlayReady version 4.6 and PlayReady version 4.7.

## General Changes in PlayReady Version 4.7

### Support for Counter-Signed Certificates

Starting with PlayReady 4.7, dual-signed (counter-signed) certificates are now supported.

## Changes in PlayReady Server SDK Version 4.7

### General Server Changes

* The .NET Core SDK has been migrated to .NET version 8.0.
* Root-of-trust validation options have been implemented across appsettings.json files and server-side configurations.
* RMSDK versioning is now embedded in server responses to improve telemetry and facilitate client compliance tracking.
* A new property was added to the Certificate object to expose the raw bytes of the certificate chain.
* Gets or sets a value indicating whether the server should sign the license response. By default, only responses that contain persistent licenses are signed.

### Server API Changes

This is merely an overview. Refer to the [Server API documentation](/dotnet/api/Microsoft.Media.Drm) for more information.

The following APIs were added:
*  public byte[] Microsoft.Media.Drm.Certificate.CertificateChain
*  public bool Microsoft.Media.Drm.LicenseResponse.ForceSignature


## Changes in PlayReady Device Porting Kit Version 4.7

### General Device Porting Kit changes
* Counter-signature validation was added to the PK.
* Resolved an issue with PlayReady Device Credentials Renewal after rolling to a new CTK (Current TEE Key).
* PK certificates were updated to include counter-signed extensions as required for this release.
* Removed several unused files—such as pre-generated certificates, mock data, and test assets—from the PK test infrastructure.
