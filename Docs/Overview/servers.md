---
title: PlayReady Servers
description: This topic describes the different types of PlayReady Servers.
ms.assetid: "ECD043B6-9F4B-4801-A3AE-9FD822DCD9E4"
keywords: playready servers
ms.date: 02/01/2018
ms.topic: conceptual
---

# PlayReady Servers
PlayReady Servers can take different forms depending on whether they are programmed to deliver licenses, or manage PlayReady domains of clients, or receive and aggregate metering data from clients, and so on. These logical Servers are all developed in C# based on the same [PlayReady Server SDK](https://docs.microsoft.com/dotnet/api/microsoft.media.drm), and a single Server application can implement one or several of the PlayReady Server functionalities.


## PlayReady License Server

A PlayReady License Server allows processing of incoming license acquisition requests from clients, generates licenses, and issues them in a license acquisition response back to clients.

For more information about PlayReady license servers, see [PlayReady License Server](license-Server.md).

## PlayReady Domain Server

An optional PlayReady Domain Server allows you to manage content access for multiple clients through a single entity. Domains provide simplified and more robust service access for multiple clients, including mobile device clients.

> [!NOTE]
> A PlayReady domain is not the same as network or Web domains.

For more information about PlayReady domains, see [PlayReady Domain Server](domain-Server.md).

## PlayReady Metering Server

An optional PlayReady Metering Server provides a process that indicates how many times specific content has been played. For example, you could use this metering aggregation service in a subscription scenario to track content usage and charge the user appropriately.

For more information about PlayReady metering, see [PlayReady Metering Server](metering-Server.md).

## PlayReady Secure Stop Server

An optional PlayReady Secure Stop Server provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provides accurate enforcement and reporting of usage limitations on different devices for a given account.

For more information about PlayReady Secure Stop, see [PlayReady Secure Stop Server](secure-stop-Server.md).

## PlayReady Secure Delete Server

PlayReady Secure Delete allows service providers to receive secure acknowledgement of license deletion. This optional feature provides a PlayReady Secure Delete Server with a means to track which licenses are available and which have been deleted on a particular client.

For more information about PlayReady Secure Delete, see [PlayReady Secure Delete](secure-delete-Server.md).

## Development and operation by the licensee or a third party

A company, typically a service provider, with an active PlayReady Server licensing agreement can access the PlayReady Server SDK and use it to develop and operate a PlayReady Server (License Server, Domain controller, Metering Server, Secure Stop Server, or Secure Delete Server).

All of these Servers must be deployed on a physical or virtual Server running Windows Server. You do not need to deploy each type of Server on their own machine; instead multiple PlayReady Server types can be run on the same physical machine.

This company can, however, share roles with third parties:

  *  PlayReady Server Development partners &mdash; these companies can develop the logic of a PlayReady Server on behalf of the customer.

  *  PlayReady application service provider (ASP) partners &mdash; these companies can develop and operate, or operate a PlayReady Server on behalf of the customer. This Server may be connected to the customer’s backend logic and Key Management System in different ways to provide a complete DRM system.

See the [PlayReady Partners](https://www.microsoft.com/playready/partners) page for more information.

## PlayReady Server Sample

The following is a description of the PlayReady Server SOAP interface available at **[https://test.playready.microsoft.com/service/rightsmanager.asmx](https://test.playready.microsoft.com/service/rightsmanager.asmx)**

```
RightsManager

The following operations are supported. For a formal definition, please review the Service Description.

  - AcknowledgeLicense

  - AcquireLicense

  - AcquirePackagingData

  - GetMeteringCertificate

  - JoinDomain

  - LeaveDomain

  - ProcessDeleteLicenseData

  - ProcessMeteringData

  - ProcessSecureStopData
```

&nbsp;

## In this section

[PlayReady License Server](license-server.md)

[Best Practices for License Policies](policies-best-practices.md)

[PlayReady Domain Server](domain-server.md)

[PlayReady Metering Server](metering-server.md)

[PlayReady Secure Stop Server](secure-stop-server.md)

[PlayReady Secure Delete](secure-delete-server.md)


## See also
[PlayReady Test Server](https://test.playready.microsoft.com/)

[PlayReady Test License Server](https://test.playready.microsoft.com/service/rightsmanager.asmx)

[PlayReady Server SDK](https://docs.microsoft.com/dotnet/api/microsoft.media.drm)
