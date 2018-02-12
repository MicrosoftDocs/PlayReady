---
author: rolandlefranc
title: PlayReady Ecosystem
description: This sections describes the PlayReady ecosystem.
ms.assetid: "dfb65490-8a56-fdda-a81d-b106ad0c69bb"
keywords: about the Microsoft PlayReady ecosystem, PlayReady ecosystem
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Ecosystem


Clients and Servers are the two main components in the PlayReady ecosystem. These components communicate using protocols specified by Microsoft. Content is protected by a content packaging service using PlayReady, then transferred to clients that decrypt the content by using information stored in a license. The information in this section serves as a primer to the PlayReady concepts that are provided as scenarios in [Common PlayReady Scenarios](common-playready-scenarios.md).

<a id="ID4EV"></a>



## PlayReady Clients


PlayReady Clients are devices capable of playing back protected content when given a license for that content (such as media player programs on personal computers or applications on devices such as cell phones, tablets, and smart TVs). PlayReady Clients must also be able to enforce the rights and restrictions associated with a policy included in a license.


The following figure shows the icons used throughout this document that symbolize devices used as PlayReady Clients.


![PlayReady Clients](../images/image26_0.jpg)

<a id="ID4EDB"></a>



## PlayReady Servers


Customized application Servers enable interoperation with the clients. Service providers use the PlayReady Server Software Development Kit (SDK) to build Servers with service-specific business logic. For example, a subscription service would customize Servers to have a service-specific license. The license might include expiration times and license issuance restrictions that tie to a specific data backend that has subscriber information. By using the PlayReady Server SDK, the customized Server builder can be confident the service will protect content and issue licenses that work with PlayReady Clients.


PlayReady Servers include License Servers, Domain Controllers, Metering Servers, Secure Stop Servers, and Secure Delete Servers. These Servers are all developed on the same PlayReady Server SDK.

In addition, a service also has a content packager to encrypt and encode content, and a Streaming backend and CDN to distribute the content on the network.

The following figure shows the icons used throughout this document to represent the different Servers.


![PlayReady Servers](../images/image26_1.jpg)

> [!NOTE]
> Content is stored and distributed using Web Servers, but PlayReady products do not include or require a specialized Web Server for content storage and distribution.

<a id="ID4ETB"></a>



## Content and license flow


In PlayReady systems, a content packaging service encrypts content and stores it on a Web Server. Clients acquire this encrypted content through streaming or download. Clients also acquire a PlayReady license from a License Server, which contains the information needed to decrypt content for rendering.

The following figure depicts content and license flow for license acquisition (LA). The gray arrow indicates clear content transfer, black arrows indicate protected content transfer without a license, and white arrows indicate license transfers.


![Content License Flow](../images/image26_2.jpg)


The following steps describe the content and license flow for license acquisition shown in the previous figure:

   1. A content provider packages unprotected content by using either third party software or the PlayReady Server SDK.

   1. When the content is packaged, the content provider copies the protected content to a content distribution Server/system.

   1. The content provider transfers the license information to a License Server.

   1. A client will then acquire the protected content.

   1. When the client attempts to play the content, the header indicates that the client needs to acquire a license. The client then performs license acquisition from a License Server.



For more information about license acquisition, see [License Acquisition](license-acquisition.md).

The PlayReady encryption and licensing process is more fully explained in [Basic encryption and licensing process](simple-end-to-end-system.md#basicprocess).

