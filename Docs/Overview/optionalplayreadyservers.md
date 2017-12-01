---
author: 
title: "Optional PlayReady Servers"
description: ""
ms.assetid: "44971D99-B5E5-4E69-B014-5F303E830B9D"
kindex: servers, optional
kindex: optional, PlayReady servers
keywords: server, optional, metering, secure stop, secure delete, domain
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Optional PlayReady Servers

In addition to the PlayReady license server, the PlayReady Server SDK contains libraries and C# sample code that allow you to develop optional types of PlayReady Servers. These optional servers are:

  *  PlayReady domain server
  *  PlayReady metering server
  *  PlayReady Secure Stop server
  *  PlayReady Secure Delete server

You can either develop and deploy these optional servers yourself, or these services can be provided to you from third parties, such as a [PlayReady Partner](https://www.microsoft.com/playready/partners/). All of these optional servers must be deployed on a server running Windows Server. You do not need to deploy each type of server on their own machine; instead multiple PlayReady server types can be run on the same physical machine.

## PlayReady domain server

An optional PlayReady domain server allows you to manage content access for multiple clients through a single entity. Domains provide simplified and more robust service access for multiple clients,including mobile device clients.

> [!NOTE]   
> A PlayReady domain is not the same as network or Web domains.

For more information about PlayReady domains, see [PlayReady Domains](playreadydomains.md).

## PlayReady metering server

An optional PlayReady metering server provides a process that indicates how many times specific content has been played. For example, you could use this metering aggregation service in a subscription scenario to track content usage and charge the use appropriately.

For more information about PlayReady metering, see [PlayReady Metering](playreadymetering.md).

## PlayReady Secure Stop server

An optional PlayReady Secure Stop server provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.

For more information about PlayReady Secure Stop, see [PlayReady Secure Stop](playreadysecurestop.md).

## PlayReady Secure Delete server

PlayReady Secure Delete allows service providers to receive secure acknowledgement of license deletion. This optional feature provides a PlayReady Secure Delete server with a means to track which licenses are available and which have been deleted on a particular client.

For more information about PlayReady Secure Delete, see [PlayReady Secure Delete](playreadysecuredelete.md).
