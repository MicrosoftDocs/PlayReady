---
author: rolandlefranc
title: PlayReady Server SDK
description: PlayReady Server Software Development Kit (SDK) is a collection of APIs that make it easier for developers to create PlayReady license delivery, domain, metering, secure stop, and secure delete services.
ms.assetid: "7de2da30-5f9d-3167-a180-2d01a50c6ea7"
keywords: PlayReady Server SDK
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Server SDK


PlayReady Server Software Development Kit (SDK) is a collection of APIs that make it easier for developers to create PlayReady License delivery, Domain, Metering, Secure Stop, and Secure Delete services.

<a id="ID4ER"></a>



## Features


PlayReady Server SDK:

   *  Provides Licensing support (issuance and acknowledgement).

   *  Provides support for joining and leaving PlayReady Domains.

   *  Updates the Metering certificate acquisition protocols.
 
   *  Provides Metering support.

   *  Provides Secure Stop support.

   *  Provides Secure Delete support.

   *  Includes C# .Net based development.


<a id="ID4EZB"></a>



## Components

PlayReady Server SDK is delivered as two Microsoft MSI files that contain the libraries, samples, and tools required to develop a PlayReady License Server, PlayReady Domain Server, PlayReady Metering Server, PlayReady Secure Stop Server, or PlayReady Secure Delete Server. In addition, you will also be supplied with the PlayReady documentation and any additional current information in the PlayReady Server SDK readme file.


PlayReady Server SDK includes the following components:

   *  Libraries and interfaces for accessing the PlayReady Server SDK features.

   *  Documentation and specifications for related technologies.

   *  Whitepapers for Server builders.

   *  Content packaging tools.



<a id="ID4ETC"></a>



## Architecture


The following figure shows how the PlayReady Server SDK components interact in the PlayReady Server SDK architecture.


![PlayReady Server SDK Architecture](../images/image26_19.png)


As shown in the figure, a PlayReady Client interacts with PlayReady Server SDK by following these steps:

   1. The Client sends a SOAP message to the Server to initiate an operation.

   1. The SOAP message passes through the Internet Information Services (IIS) and ASP.net components to reach a Web service entry point.

   1. The Web service entry point then processes the call, processes the data, and triggers the service plug-in.

   1. The service-specific application logic (implemented by the service provider) is encapsulated in a service developed plug-in.



Service-specific application logic typically is either going to be identification information or business logic. Service information includes the service identifier (service ID) and the license acquisition URL associated with licenses (these settings are service-specific). Also specified in the plug-in is business logic associated with the service such as the policy that is associated with issued licenses.


Service providers can implement their own services by using PlayReady Server SDK and offer individualized, unique license-issuing scenarios. For example, consider two services, Contoso and Fabrikam. Each service provider needs to provide separate identifiers for its services and each supports different policies. The Contoso service could build a license issuance service that issues licenses that point to its <http://contoso.com> License Servers, and the Contoso service could issue licenses that expire after three months. The Fabrikam service can implement its own service that issues licenses that point to its <http://fabrikam.com> License Servers and that expire in one month.


PlayReady Server SDK enables various scenarios that are based on the following protocols:

   *  Domain join

   *  Domain leave

   *  Acquire license

   *  Acknowledge license

   *  Process metering data

   *  Get metering certificate

   *  Process Secure Stop data

   *  Process Secure Delete data


## See also

[PlayReady Servers](servers.md)

[PlayReady License Server](license-Server.md)
