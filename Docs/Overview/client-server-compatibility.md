---
author: timrule
title: PlayReady Client-Server Compatibility and Migration Considerations
description: Most versions of PlayReady Clients and PlayReady Servers interoperate correctly.
ms.assetid: "9A903AA9-BBAD-424D-9740-9C8C1D7E5F45"
keywords: client, server, compatibility, migration
ms.author: timrule
ms.date: 02/01/2018
ms.topic: conceptual
---

# PlayReady Client-Server Compatibility and Migration Considerations

## Abstract

Microsoft® PlayReady® 3.0 brings important new functionalities that OEMs want to integrate in their devices. This brings a few compatibility issues with services designed more than 5 years ago. This paper discusses them and provides guidance for both services and OEMs in the upgrade path to PlayReady 3.0

Table of Contents

[Overview](#overview)

[PlayReady Compatibility Matrix](#playready-compatibility-matrix)

[Recommendations for PlayReady Services](#recommendations-for-playready-services)

[Recommendations for PlayReady Device Manufacturers](#recommendations-for-playready-device-manufacturers)

[Migrations Notes for Services](#migrations-notes-for-services)

[Migrating a PlayReady service to Server SDK 3.0](#migrating-a-playready-service-to-server-sdk-30)

[Compiling and deploying an updated license handler will need to take into account the following](#compiling-and-deploying-an-updated-license-handler-will-need-to-take-into-account-the-following)

[Supporting different Server SDK versions for a Service](#supporting-different-server-sdk-versions-for-a-service)

[Supporting Clients based on PK 3.0 with legacy license services](#supporting-clients-based-on-pk-30-with-legacy-license-services)

[Supporting PlayReady 3.0 features for services](#supporting-playready-30-features-for-services)

[Supporting both SL2000 and SL3000 in services](#supporting-both-sl2000-and-sl3000-in-services)

[Testing PlayReady clients with versions of the PlayReady Server SDK](#testing-playready-clients-with-versions-of-the-playready-server-sdk)

[Scenario 1: non-persistent licenses](#scenario-1-non-persistent-licenses)

[Scenario 2: persistent licenses](#scenario-2-persistent-licenses)

[Scenario 3: chained licenses](#scenario-3-chained-licenses)

[Scenario 4: domain-bound license](#scenario-4-domain-bound-license)

## Overview

PlayReady license services maintain backward compatibility for legacy PlayReady devices. For example, a new license service developed with the PlayReady Server SDK 3.0 can deliver licenses to a legacy device which was developed using the PlayReady Porting Kit(PK) 1.2 from its initial release (2008).

There are, however, some nuances in compatibility as services and devices move into the PlayReady 3 releases. PlayReady Clients developed with the 3.0 Porting Kit cannot obtain licenses from a license service built prior to the 2011 release of the Server SDK 2.0. Services running earlier versions of the Server SDK will need to upgrade to be compatible with PlayReady 3.0.

## PlayReady Compatibility Matrix

Most versions of PlayReady on the client can work with the different versions of the PlayReady Server SDK. There are some subtleties as noted below as well as a change with PlayReady clients developed on the 3.0 Porting Kit.

|&nbsp;| Server SDK 1.x  | Server SDK 2.0 (2011)  | Server SDK 2.1 (2013)  | Server SDK 2.9 (2014)  | Server SDK 3.0 (2015)  |
|----|----|----|----|----|----|
| PK 1.x (2008)      |   | *  | *  | *  | *  |
| PK 2.x (2011)    |   |   |   |   |   |
| PK 3.0 (2015)  | **  | ***  | ***  | ***  |   |

| &nbsp;| Server SDK v1.5.2| Server SDK v2.1 and Server SDK v2.9| Server SDK v3.0| Server SDK v4.0 |
| --- | --- | --- | --- | --- |
| PK v4.x| No| Yes | Yes | Yes |
| PK v3.x| No| Yes| Yes| Yes |
| PK v2.5 and v2.11| Yes| Yes| Yes| Yes |

| Incompatible | Compatible |
|:-------------|:-----------|
|              |            |

\* Some PK 1.2 clients did not support revocation which is required in Server SDK 2.x+. This is not common.

**  PK3.0 Clients cannot use a Server SDK prior to version 2.0 to get a media playback license.

*** PK3.0 Clients can use license servers using a 2.X SDK but can only obtain a license with a SL2000 security level. In addition, new features such as support for version 4.2 headers (multiple keys) and policies such as Secure Stop and MaxResDecode are not available when creating a license. There have been issues with chained licenses(root/leaf) on some PK3.0 clients with Server SDK 2.0. Services will need to test clients to validate compatibility. There are a set of scenarios at the end of this document which can assist in testing.

## Recommendations for PlayReady Services

1. Ensure that a service is upgraded to the latest version of the PlayReady SDK. This will provide the best compatibility across new and legacy devices. The recent versions of the Server SDK also have added significant performance and stability improvements. Note that *no additional licensing or license fees are required* to upgrade to the newest PlayReady Server 3.0.

2. As new devices continue the migration of PlayReady to the hardware(SoC), there will be more and more devices reporting to a service as PlayReady 3.0 and SL3000. For example, all Windows 10 devices now report as PlayReady 3.0 devices. Services are encouraged to upgrade to the latest version of the server SDK to maintain compatibility as well as leverage some of the new features.

3. Use this guide to handle edge cases such as maintaining legacy license services as-is while supporting new devices.

4. Licensees can contact askdrm@microsoft.com to gain access to our feedback site to submit migration questions

## Recommendations for PlayReady Device Manufacturers

It is strongly recommended that OEMs upgrade their devices to PK3.0 released in April 2015, which is the only version allowing devices to leverage the latest functionalities being implemented by top media services.

| **Pros**| **Cons – Attention points** |
|:---------|:--------|
|Can support SL3000 Not compatible with Server SDK 1.X | |
|Can implement latest functionalities like SecureStop, MaxResDecode, etc.| |
|Better Codebase| |
| |Ensure new license policies as requested by content owners can be enforced|

### OEM Upgrade Plan

1. Contact your services and make sure they all migrate or add a Server SDK 2.0+ version o Verify their Server SDK version

   * Reiterate considerations for the service: **no additional Licensing requirements from Microsoft and no additional** fees.

   * If they run a Server SDK v2.0+ based license service, they will likely be compatible. The service URLs and scenarios in the next section can assist in compatibility testing. o If they run a Server SDK v1.X based license server, they can migrate their license server or add a newer license server for the new clients - based on Server SDK 2.0+ (latest version is recommended).

1. Download the PK3.0 from Microsoft

1. Get support from Microsoft’s partners or directly from Microsoft on [https://connect.microsoft.com/playready](https://connect.microsoft.com/playready).

1. Implement PK3.0 and release your product.

## Migrations Notes for Services

For optimal device compatibility, ensure the license server is running the latest version of the Server

SDK. The most recent Server SDK will be able to deliver licenses to all PlayReady clients regardless of the Porting Kit version used. If a Client developed with the 3.0 Porting Kit attempts to obtain a license from a license service using PlayReady SDK 1.x, the license service will return a generic service specific SOAP fault. The server will log an exception to the Windows log noting that the challenge was missing the client certificate chain.

## Migrating a PlayReady service to Server SDK 3.0

A service upgrade will usually not involve any code changes but just a recompilation and deployment of the updated libraries. In some cases, there might be minor code changes due to some deprecated APIs. The recompilation and deployment of the license handler library should be transparent to devices accessing the service.

### Compiling and deploying an updated license handler will need to take into account the following

* The project will need to remove references to the old PlayReady libraries and reference the new one prior to recompiling.

* The newer Server SDKs require .NET 4.0 or greater. When upgrading the license service handler from an early version such as 1.52, the target framework will need to be updated in the project properties to that of 4.0 or greater.

* If the legacy handler is referencing other libraries that were targeting a .NET version less than 4.0 there could be additional migration steps. However, a .NET library can reference a lesser version without any issues in general. It would be worth investigating the opportunity to recompiling referenced libraries to the version of the handler or acquiring library updates for third party components.

* Only Microsoft.Media.Drm.RMCore needs to be referenced within the project. When deploying a solution, the other DLLs need to be deployed in the bin directory of the website. They do not need to be referenced within the project as was the case with earlier SDKs.

* A minimum .NET CLR version of 4.0 is required for the *Application Pool* utilized by the license service. If the license service was running 2.0 or earlier, it is likely that it is running within a .NET CLR version less than 4.0.

* The latest PlayReady Server SDK is only supported under Windows Server 2012 and greater. Windows Server 2008 R2, however, is not known to have any issues with the Server SDK.

## Supporting different Server SDK versions for a Service

It’s recommended to migrate to the latest version of the SDK soon after its released. In some cases, however, a service may want to run multiple versions of the server SDK. This can be due to maintaining legacy and archive services and endpoints that are not easily updated. In this case a service can point new clients to an updated license service while leaving the legacy service untouched. For example, a service may have a number of legacy devices within their ecosystem running a client built with PlayReady PK 1.2. Their new devices are developed using the PlayReady PK 3.0. The new client would need to point to a license service built with Server SDK 2.0 or greater. If both the legacy and new devices use the same application (such as an HTML based app platform), then logic will be needed to be added to the application to detect version of the client. The client application can then direct license requests to a newer license service.

The recommended migration is to update the license service to the latest version of the Server SDK. This can provide compatibility across all devices for many services. A service will need to test across clients to validate compatibility.

If a service does not want to make alterations to a legacy client and service configuration, the recommendation is to host a second license service that has been upgraded to the latest version of the SDK and is utilized by modern clients.

If a service uses the same application for legacy new devices a proxy can be configured in legacy devices need to continue using the legacy service.

A service can also direct legacy clients to a legacy service and new clients to an updated service. This can be done in a proxy by inspecting the license challenge. The PK version will be noted in the `<CLIENTVERSION>` element.

The element is located within the SOAP challenge under the following element:

```xml
<Challenge><LA><CLIENTINFO><CLIENTVERSION>3.1.0.1017</CLIENTVERSION>
```

## Supporting Clients based on PK 3.0 with legacy license services

A client device developed with the PlayReady Porting Kit 3.0 will likely work with existing services developed with the Server SDK 2.0 and greater. As noted above, a service need to test the PK 3.0 clients to validate compatibility.

If the device has a SL3000 certificate, the Security Level exposed via the client certificate in the license handler will report as 3000. This can possibly cause problems with some license handlers if they are looking for a specific Security Level value to differentiate between production and test devices.

Differentiating between Security Levels is common for services which provide limited content access for test devices to validate playback licenses from a live service. Only devices that reported as Security Level 2000 would have playback licenses delivered for commercial content. The service would throw a service specific exception which would result in a SOAP fault on the client.

In the example below the Security Level is being checked in the client certificate to ensure that it is a production device. Since it has been hardcoded to 2000, devices with the security level of 3000 will not be seen as production devices.

This example updates the check for security level to whether it is greater than or equal to 2000. This will ensure compatibility with SL3000 devices.

## Supporting PlayReady 3.0 features for services

In addition to the new hardware DRM security level, the PlayReady 3 release also introduced a variety of new features. In order to take advantage of these new features the service will need to first determine if the client is capable of PlayReady 3 features. The client certificate class now supports a

GetSupportedFeatures method which will return a collection of features to help in the logic of defining policies within the handler. If the client was developed with the 3.0 Porting Kit, it will have the SupportedFeature.PlayReady3Features in the collection. There are additional useful features in the collection such as whether the client is using a secure clock or anti-rollback clock.

Here’s an example of how to detect whether the device is a PlayReady 3 client.

Once detected the handler can add policies such as Secure Stop, Real-time license expiration, and MaxResDecode for example.

## Supporting both SL2000 and SL3000 in services

PlayReady introduced a new security level SL3000 which is reported by devices who have met the

PlayReady hardware security level for running within a trusted execution environment as defined in the Compliance and Robustness Rules. It will be common for services to have some client report as SL2000 and others report as SL3000. For example, in Windows, older devices that have upgraded to Windows 10 may report as SL2000. New Windows 10 devices will report as SL3000 where the DRM has been incorporated into the newer chips.

Here is an example of a service providing different policies based on the reported security level from the client’s challenge:

A service will determine how policies should differ between software-based DRM clients and hardwarebased DRM clients. These policies may be driven by studio requirements. For example, a studio may require in the future that Ultra-HD or 4K content be limited to devices that support hardware-based PlayReady DRM.

With PlayReady 3 policies around resolutions can be accomplished in a couple of different ways. One way is to set the MaxResDecode policy of SL2000 licenses to the allowable limits provided by the content owner. The SL3000 devices would not get this policy restriction. Another option applicable to adaptive streaming technologies is to use a different KeyID when protecting the various resolutions. When detecting the security level, a service can then only provide licenses for the resolutions allowed for a software-based. A clients reporting a security level of SL3000 would get playback licenses for all the resolutions. PlayReady introduced a new DRM header to support this latter scenario by enabling multiple KeyIDs in the schema.

## Testing PlayReady clients with versions of the PlayReady Server SDK

The PlayReady testing website contains a set of license services that use current and legacy versions of the Server SDK. These license services can be used to assist in the testing of client compatibility. For example, when updating a client to PK 3.0 the client can be tested against previous service versions to review compatibility.

The versioned services are listed in the table below.

| **SDK Version**  | **License Service URL**  |
|:--|:--|
| **SDK 1.52**  | [https://test.playready.microsoft.com/directtaps/svc/pr152/rightsmanager.asmx](https://test.playready.microsoft.com/directtaps/svc/pr152/rightsmanager.asmx) |
| **SDK 2.0**  | [https://test.playready.microsoft.com/directtaps/svc/pr20/rightsmanager.asmx](https://test.playready.microsoft.com/directtaps/svc/pr20/rightsmanager.asmx) |
| **SDK 2.1**  | [https://test.playready.microsoft.com/directtaps/svc/pr21/rightsmanager.asmx](https://test.playready.microsoft.com/directtaps/svc/pr21/rightsmanager.asmx) |
| **SDK 2.9**  | [https://test.playready.microsoft.com/directtaps/svc/pr29/rightsmanager.asmx](https://test.playready.microsoft.com/directtaps/svc/pr29/rightsmanager.asmx) |
| **SDK 3.0**  | [https://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx](https://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx) |

These versioned services can utilize the parameters listed on the PlayReady test site for testing specific policies: [https://testweb.playready.microsoft.com/](https://testweb.playready.microsoft.com/).

>[NOTE!]
>Not all of the policy parameters will work with each of the service versions. For example, MaxResDecode is a new policy and only works with services developed with the Server SDK 3.0 or later.

To assist in capability testing, the following tests can be used with the different versioned license services to cover four unique licensing scenarios.

## Scenario 1: non-persistent licenses

Non-persistent licenses are the most common license scenario used by streaming services.

Test Steps:

1. Package the content using the KeySeed noted on the PlayReady test site. For this test any KeyID can be utilized when packaging.

1. Test a license request from the client using the following URL:  

   `{versioned *license service* URL}?UseSimpleNonPersistentLicense=1`

   Example:

   `https://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx?UseSimpleNonPersistentLicense=1`

1. Validate a license is returned and that playback is successful.

## Scenario 2: persistent licenses

Persistent licenses are commonly utilized by services that enable the playback content offline.

Test Steps:

1. Package the content using the KeySeed noted on the PlayReady test site. For this test any KeyID can be utilized when packaging.

1. Test a license request from the client using the following URL:

   `{versioned license service URL}?PlayRight=1&FirstPlayExpiration=60`

This parameter will direct the license service to return a license that expires 60 seconds after its first played. Example:

   `https://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx?PlayRight=1&FirstPlayExpiration=60`

1. Validate that a license is returned and that playback is successful. Add or change the time based policy parameters as listed on the test site to test other persistent scenarios.

## Scenario 3: chained licenses

Root bound licenses are used by some subscription services most commonly for music. With the rootbound scenario, several leaf licenses can be bound to a single root license. When the root license expires then the leaf licenses are no longer useable unless a new root is reissued.

Test Steps:

1. Package the content using the KeySeed noted on PlayReady test site and the following KeyID:

   Base64: **uPeXHrR3K0icGCpYMBGsZw==**

1. Test the client using the following URL to request a license:

   `{versioned license service URL}`  **without any parameters** Example:

   `https://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx?UseSimpleNonPersistentLicense=1`

1. Validate that a license is returned and that playback is successful. In this scenario a single response from the service should contain two licenses. One of them will be a root license and the other a leaf license. The licenses should expire 5 minutes after being issued to the client.

## Scenario 4: domain-bound license

Domain are not as commonly used by services. PlayReady domains provide both a way for service to manage the number of active devices in an account and for devices within the account to share content and licenses offline.

1. Package the content using the KeySeed noted on PlayReady test site and the following KeyID:

   Base64: **m1HAERIu8E+uABCZY4TX2g==**

The test client will using the following URL for joining the domain and acquiring a license:

   `{versioned license service url}?AccountID=A/uHOj7F+UaM+Jlny2obFA==`

   Example:

   `http://playready.directtaps.nehttp/test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx?AccountID=A/uHOj7F+UaM+Jlny2obFA==`

1. Have the test client generate and send a JoinDomain challenge and validate that there is a domain certificate is in the service response.

1. Have the test client send a license request to the service using the same URL including the accountID.

1. Validate that a license is returned and that playback is successful. A LeaveDomain request can additionally be sent to the license service to reset the scenario.
