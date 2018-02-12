---
author: rolandlefranc
title: PlayReady Client-Server Protocol
description: Most communication between a PlayReady Client and a PlayReady Server are managed through the use of Simple Object Access Protocol (SOAP) messages.
ms.assetid: "3EC7CBF9-8E17-4F9A-849D-14C2C482D62E"
keywords: soap, playready client server protocols
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Client-Server Protocol


Most communication between a PlayReady Client and a PlayReady Server are managed through the use of Simple Object Access Protocol (SOAP) messages. This communication begins when the client sends a SOAP message containing a challenge. The Server responds with a SOAP message that contains a response. Both the challenge and the response contain information in XML format that signifies the type of challenge or response, and the various elements needed to process and identify the specific transaction that needs to take place.

These SOAP messages can be exchanged over HTTP or HTTPS.

Note that service providers may wrap the protocol into their own custom protocol if they desire. The PlayReady Server SDK, as well as most PlayReady Clients allow access and manipulate the SOAP challenges and responses and extend them or wrap them into another type of protocol.


Examples of the challenge and response SOAP messages can also be found on a PlayReady Server after installing and configuring IIS for PlayReady.

