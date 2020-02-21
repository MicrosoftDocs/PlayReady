---
title: How to Test PlayReady Clients with Versions of the PlayReady Server SDK
description: Contains scenarios for testing various client versions with various server versions.
ms.assetid: "8607D297-DD0F-4EE5-AE74-342935DE9C39"
keywords: compatibility, testing, clients, Server SDK, content protection
ms.date: 03/30/2018
ms.topic: conceptual
---


# How to Test PlayReady Clients with Versions of the PlayReady Server SDK

The PlayReady testing website contains a set of license services that use current and legacy versions of the Server SDK. These license services can be used to assist in the testing of client compatibility. For example, when updating a client to PK 4.0 the client can be tested against previous service versions to review compatibility.

The versioned services are listed in the table below.

| **SDK Version**  | **License Service URL**  |
|:--|:--|
| **SDK 1.52**  | http(s)://test.playready.microsoft.com/directtaps/svc/pr152/rightsmanager.asmx  |
| **SDK 2.0**  | http(s)://test.playready.microsoft.com/directtaps/svc/pr20/rightsmanager.asmx  |
| **SDK 2.1**  | http(s)://test.playready.microsoft.com/directtaps/svc/pr21/rightsmanager.asmx  |
| **SDK 2.9**  | http(s)://test.playready.microsoft.com/directtaps/svc/pr29/rightsmanager.asmx  |
| **SDK 3.0**  | http(s)://test.playready.microsoft.com/directtaps/svc/pr30/rightsmanager.asmx  |
| **SDK 4.0**  | http(s)://test.playready.microsoft.com/service/rightsmanager.asmx  |


These versioned services can utilize the parameters listed on the PlayReady test site for testing specific policies. The PlayReady Public Test Server now supports multiple syntaxes to provide these parameters so testers can chose the one most appropriate to their case.

The http(s)://test.playready.microsoft.com/service/rightsmanager.asmx site is always used for the latest up to date server.

The recommended syntax is the [Query String Syntax](https://test.playready.microsoft.com/Server/ServiceQueryStringSyntax). Other syntaxes include the [Custom Data JSON Syntax](https://test.playready.microsoft.com/Server/ServiceCustomDataJSONSyntax), the [Base 64 JSON Syntax](https://test.playready.microsoft.com/Server/ServiceBase64JSONSyntax), and the [Legacy Syntax](https://test.playready.microsoft.com/Server/ServiceLegacySyntax).

Note that not all of the policy parameters will work with each of the service versions. For example, MaxResDecode only works with services developed with the Server SDK 3.0 or higher.

To assist in capability testing, the following tests can be used with the different versioned license services to cover four unique licensing scenarios. These scenarios demonstrate how to use the Query String syntax in your tests. However, you can use any of the other syntaxes linked above if they are more appropriate for your case.


## Scenario 1: non-persistent licenses

Non-persistent licenses are the most common license scenario used by streaming services.

Test Steps:

1. Package the content using the [KeySeed](https://test.playready.microsoft.com/Server/Service) noted on the PlayReady test site. For this test any KeyID can be utilized when packaging.

1. Test a license request from the client using the following URL:

   {*versioned license service URL*}**without any parameters**

    ex: [https://test.playready.microsoft.com/service/rightsmanager.asmx](https://test.playready.microsoft.com/service/rightsmanager.asmx)

1. Validate a license is returned and that playback is successful.


## Scenario 2: persistent licenses

Persistent licenses are commonly utilized by services that enable the playback content offline.

Test Steps:

1. Package the content using the KeySeed noted on the PlayReady test site. For this test any KeyID can be utilized when packaging.

1. Test a license request from the client using the following URL:

   {*versioned license service URL*}**?cfg=(persist:true,firstexp:60)**

   This parameter will direct the license service to return a license that expires 60 seconds after its first played. Note that you have to explicitly call out **persist:true** to receive persistent licenses.

   ex: [https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:true,firstexp:60)](https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=\(persist:true,firstexp:60\))


1. Validate that a license is returned and that playback is successful. Add or change the time based policy parameters as listed on the test site to test other persistent scenarios.


## Scenario 3: chained licenses

Root bound licenses are used by some subscription services, most commonly for music. With the root bound scenario, several leaf licenses can be bound to a single root license. When the root license expires, the leaf licenses are no longer useable unless a new root is reissued.

Test Steps:

1. Package the content using the KeySeed noted on the PlayReady test site using the following KeyID:

   Base64: **uPeXHrR3K0icGCpYMBGsZw==**

1. Test the client using the following URL to request a license:

   {*versioned license service URL*}**?cfg=(rootid:uPeXHrR3K0icGCpYMBGsZw==,kid:header),(isroot:true,kid:uPeXHrR3K0icGCpYMBGsZw==)**

   ex: [https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(rootid:uPeXHrR3K0icGCpYMBGsZw==,kid:header),(isroot:true,kid:uPeXHrR3K0icGCpYMBGsZw==)](https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(rootid:uPeXHrR3K0icGCpYMBGsZw==,kid:header),(isroot:true,kid:uPeXHrR3K0icGCpYMBGsZw==))

1. Validate that a license is returned and that playback is successful. In this scenario a single response from the service should contain two licenses. One of them will be a root license and the other a leaf license. The licenses should expire five minutes after being issued to the client.


## Scenario 4: domain-bound license

Domains are not as commonly used by services. PlayReady domains provide both a way for a service to manage the number of active devices in an account and for devices within the account to share content and licenses offline.

1. Package the content using the KeySeed noted on the PlayReady test site using the following KeyID:

   Base64: **m1HAERIu8E+uABCZY4TX2g==**

   The test client will use the following URL for joining the domain and acquiring a license:

   {*versioned license service url*}?cfg=(accountid:A/uHOj7F+UaM+Jlny2obFA==)

   ex: [https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(accountid:A/uHOj7F+UaM+Jlny2obFA==)](https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(accountid:A/uHOj7F+UaM+Jlny2obFA==))

1. Have the test client generate and send a JoinDomain challenge and validate that there is a domain certificate in the service response.

1. Have the test client send a license request to the service using the same URL, including the accountID.

1. Validate that a license is returned and that playback is successful. A LeaveDomain request can additionally be sent to the license service to reset the scenario.


## More information

For more information, visit the PlayReady website at [https://www.microsoft.com/playready/](https://www.microsoft.com/playready/) and  the PlayReady test site at [https://test.playready.microsoft.com/](https://test.playready.microsoft.com/).

