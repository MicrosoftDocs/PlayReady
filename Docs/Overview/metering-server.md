---
author: rolandlefranc
title: PlayReady Metering Server
description: Metering is the process for counting the number of times content is played.
ms.assetid: "fec11f72-95f0-a80c-83cd-beafe53b4a57"
keywords: PlayReady metering, metering architecture, metering certificate acquisition
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Metering Server

*PlayReady Metering* is a feature that allows services receive usage information from PlayReady clients. For example, how many times a certain piece of content was played. This information is secured by PlayReady, and can be trusted by the service. For example, it can be used to pay royalties to the content owner if the content distribution deal is based on user consumption.

A *PlayReady Metering Server*, also known as a *PlayReady Metering Aggregation Service*, is a server that receives PlayReady transactions from PlayReady clients that contain the metering information. It parses the information received, uses it for the purpose defined by the service (e.g. stores the information in a database, counts totals), and sends acknowledgement to clients so they can delete this usage information from their memory.

It is a logical server based on the *PlayReady Server SDK* like all the PlayReady Server types, and can be operated on the same machine as the other PlayReady servers, or on a different machine.

## See also

[PlayReady Metering](../Features/metering.md)