---
author: rolandlefranc
title: PlayReady Server on Azure
description: PlayReady Server on Azure
ms.assetid: "6fb880fa-b2b1-bae3-064b-0e0345d6edf8"
keywords:  PlayReady, License Server, Azure, Azure Media Service Content Protection, AMS
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Server on Azure

## PlayReady License Server in Azure Media Services

Microsoft Azure Media Services (AMS) provides a service for encrypting content and delivering PlayReady DRM licenses, called Content Protection (AMS CP). Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user plays back protected content. When a user requests PlayReady protected content, the player application will request a license from the AMS license service. The AMS license service will issue a license to the player if it is authorized. A PlayReady license contains the decryption key that can be used by the client player to decrypt and stream the content.

For more information about PlayReady on Azure, see [Announcing Azure Media Services Live Streaming With PlayReady encryption capability](https://azure.microsoft.com/en-us/blog/announcing-azure-media-services-live-streaming-with-playready-encryption-capability/) and the [Azure Protecting Content Overview](https://docs.microsoft.com/en-us/azure/media-services/media-services-content-protection-overview).


## PlayReady Servers in Azure App Services

All types of PlayReady Servers developed on top of PlayReady Server SDK can run in Azure App Services (also known as Web App), and leverage the full power of Platform as a Service (PaaS).

App Services are scalable, reliable and geo-redundant. They require minimal maintenance.


## PlayReady Servers in Virtual Machines

All types of PlayReady Servers can run in virtual environments such as Azure Virtual Machines and other virtualization engines, and leverage the power of Infrastructure as a Service (IaaS).
