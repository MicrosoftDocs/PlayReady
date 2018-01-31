---
author:
title: PlayReady Servers
description: This topic describes the different types of PlayReady Servers.
ms.assetid: "C23CC7D6-BB81-41D7-8E6F-347B526129BB"
kindex: server, PlayReady license
kindex: license, PlayReady server
keywords: license, server
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Servers
PlayReady Servers can take different forms depending on whether they are programmed to deliver licenses, or manage PlayReady domains of clients, or receive and aggregate metering data from clients, etc. These logical servers are all developed in C# based on the same PlayReady Server SDK, and a single server application can implement one or several of the PlayReady Server functionalities.


## PlayReady License Server

A PlayReady license server allows process incoming license acquisition requests from clients, generate licenses, and issue them in a license acquisition response back to clients.

For more information about PlayReady domains, see [PlayReady License Server](license-server.md).

## PlayReady Domain server

An optional PlayReady domain server allows you to manage content access for multiple clients through a single entity. Domains provide simplified and more robust service access for multiple clients,including mobile device clients.

> [!NOTE]
> A PlayReady domain is not the same as network or Web domains.

For more information about PlayReady domains, see [PlayReady Domain Server](domain-server.md).

## PlayReady Metering server

An optional PlayReady metering server provides a process that indicates how many times specific content has been played. For example, you could use this metering aggregation service in a subscription scenario to track content usage and charge the use appropriately.

For more information about PlayReady metering, see [PlayReady Metering Server](metering-server.md).

## PlayReady Secure Stop server

An optional PlayReady Secure Stop server provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.

For more information about PlayReady Secure Stop, see [PlayReady Secure Stop Server](secure-stop-server.md).

## PlayReady Secure Delete server

PlayReady Secure Delete allows service providers to receive secure acknowledgement of license deletion. This optional feature provides a PlayReady Secure Delete server with a means to track which licenses are available and which have been deleted on a particular client.

For more information about PlayReady Secure Delete, see [PlayReady Secure Delete](secure-delete-server.md).

## Development and operation by a third party

You can either develop and deploy these servers yourself, or these services can be provided to you from third parties, such as a [PlayReady Partner](https://www.microsoft.com/playready/partners/). All of these servers must be deployed on a server running Windows Server. You do not need to deploy each type of server on their own machine; instead multiple PlayReady server types can be run on the same physical machine.


## In this section

[PlayReady License Server](license-server.md)

[Best Practices for License Policies](policies-best-practices.md)

[PlayReady Domain Server](domain-server.md)

[PlayReady Metering Server](metering-server.md)

[PlayReady Secure Stop Server](secure-stop-server.md)

[PlayReady Secure Delete](secure-delete-server.md)