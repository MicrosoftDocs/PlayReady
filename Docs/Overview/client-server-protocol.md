---
author:
title: PlayReady Client-Server Protocol
description: Most communication between a PlayReady client and a PlayReady server are managed through the use of Simple Object Access Protocol (SOAP) messages.
ms.assetid: "27BE5F0E-C171-4091-BACE-A029C6FE53B5"
kindex: SOAP, PlayReady protocols
kindex: protocols, PlayReady communication
kindex: communication, PlayReady SOAP
keywords:
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Client-Server Protocol


Most communication between a PlayReady client and a PlayReady server are managed through the use of Simple Object Access Protocol (SOAP) messages. This communication begins when the client sends a SOAP message containing a challenge. The server responds with a SOAP message that contains a response. Both the challenge and the response contain information in XML format that signifies the type of challenge or response, and the various elements needed to process and identify the specific transaction that needs to take place.

Examples of the challenge and response SOAP messages can also be found on a PlayReady server after installing and configuring IIS for PlayReady.