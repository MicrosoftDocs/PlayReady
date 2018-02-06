---
author: rolandlefranc
title: PlayReady Products and Deliverables
description: PlayReady is a very versatile technology that is designed to allow the development of clients on virtually any processor, any platform, any operating system (OS), and any environment.
ms.assetid: "53B49621-E528-43FA-B054-BB38442DF666"
kindex: PlayReady, products and deliverables
kindex: products, PlayReady
kindex: deliverables, PlayReady
keywords:  products, deliverables, license, certificates, Azure, Windows, documentation, test server, secure clock
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Products and Deliverables

PlayReady is a very versatile technology that is designed to allow the development of clients on virtually any processor, any platform, any operating system (OS), and any environment, and develop and deploy clients by the licensees or their partners, whether they are "System on a Chip" (SOC) vendors, third party developers, original design manufacturers (ODMs), or original equipment manufacturers (OEMs). A common scenario is an SOC vendor preparing the PlayReady library for their processor XYZ, and the OEMs passing this library from the SOC vendor and the certificates they received from Microsoft to their ODM, to manufacture and distribute a device that includes an operational PlayReady client.

Likewise, on the server side, PlayReady is very flexible to allow the development and deployment of servers in different types of environments (native Windows Server system, private cloud, public cloud, hybrid cloud), different types of architecture (combined with the service logic, distant from the service logic), and using partnerships. A service provider may use the PlayReady Server SDK received from Microsoft to prototype, but use a third party company to develop their license server logic, and use another company to operate it, in a public cloud infrastructure.

PlayReady Customers, whether they are service providers, device makers, or application developers, are not required to develop either their PlayReady client or server themselves. Instead, they may obtain these services or products from third-party developers, that we refer to as PlayReady partners.

This topic discusses the parts of PlayReady that are supplied by Microsoft and the parts that can be developed and deployed by the customers themselves, or their third party partners.

Here is a figurative view of these levels of product integration, and its translation to a PlayReady Client Product:

![Levels of Product Integration](../images/product_integration.png)


## PlayReady parts supplied by Microsoft

The following sections describe the parts of PlayReady that are supplied by Microsoft.


### PlayReady Server SDK

PlayReady Server SDK is delivered as two Microsoft MSI files that contain the libraries, samples, and tools required to develop a PlayReady license server, PlayReady domain server, PlayReady metering server, PlayReady secure stop server, or PlayReady secure delete server. In addition, you will also be supplied with the PlayReady documentation and any additional current information in the PlayReady Server SDK readme file.

For more information on PlayReady Server SDK, see [PlayReady Server SDK](server-sdk.md).



### PlayReady Device Porting Kit

PlayReady Device Porting Kit is delivered as a Microsoft MSI file that contains the libraries, samples, tools, and source code required to create portable devices for use with digital content that was protected with PlayReady technology.

For more information on PlayReady Device Porting Kit, see [PlayReady Device Porting Kit](device-porting-kit.md).


<a id="whatyousupply"></a>

## Developing and operating a PlayReady server

A company, typically a service provider, with an active PlayReady Server agreement can access the PlayReady Server SDK and use it to develop and operate a PlayReady server (license server, domain controller, metering server, secure stop server, or secure delete server).

This company can, however, share roles with third parties:

  *  PlayReady Server Development partners&mdash;these partners can develop the logic of a PlayReady server on behalf of the customer.
  *  PlayReady application service provider (ASP) partners&mdash;these partners can develop and operate, or operate a PlayReady server on behalf of the customer. This server may be connected to the customer’s backend logic and Key Management System in different ways to provide a complete DRM system.

See the [PlayReady Partners](https://www.microsoft.com/playready/partners) page for more information.


## Developing and operating a PlayReady Client

A PlayReady Client can be any device or application that provides PlayReady protection for media content and includes the PlayReady Client functionality. A PlayReady Client can be embedded in hardware, can be supplied as part of the operating system, or can be included in an application. This excludes applications that are developed to use an existing underlying PlayReady Client integrated in the platform, for example UWP apps for Windows using the PlayReady Client integrated in Windows 10 and not containing any PlayReady code per se.

The basic level of security that must be provided for each of these types of clients is documented in the [PlayReady Compliance and Robustness Rules](https://www.microsoft.com/playready/licensing/compliance/).

The following table clarifies whether a PlayReady Client needs to be developed or not.

| Example| PlayReady Client or not|
| --- | --- |
| Set top box containing PlayReady PK Code and a PlayReady Client Certificate on the hardware or OS| Yes|
| Android Phone containing PlayReady PK Code and a PlayReady Client Certificate in the OS| Yes|
| Application running on that Android phone using the high level APIs to trigger operations from that OS integrated PlayReady Client| No, the application just uses an existing PlayReady Client|
| Application running on an Android phone and containing PlayReady PK Code and a PlayReady Client Certificate in the application, to be device independent| Yes, the application is a PlayReady Client|
| Application running on an iOS phone and containing PlayReady PK Code and a PlayReady Client Certificate in the application| Yes, the application is a PlayReady Client|
| UWP application running on Windows 10| No, the application just uses an existing PlayReady Client|

### Device on which to install the PlayReady Device Porting Kit

If you are designing a device with PlayReady installed in hardware or PlayReady on an integrated circuit, it is up to you to supply any hardware or software required to port the PlayReady Device Porting kit to your hardware. Some integrated circuits designed by [PlayReady Partners](https://www.microsoft.com/playready/partners/) already have PlayReady installed on the chip, and you could use these integrated circuits while designing your device.

For general information about developing hardware-based PlayReady, see [Hardware versus software DRM](security-level.md#hardwarevssoftware).

## In this section

[PlayReady Server SDK](server-sdk.md)

[PlayReady Server on Azure](server-on-azure.md)

[PlayReady Device Porting Kit](device-porting-kit.md)

[PlayReady on Windows](playready-on-windows.md)

[PlayReady on Xbox](playready-on-xbox.md)

[PlayReady and Silverlight](silverlight.md)

[PlayReady Product Versions](product-versions.md)

[License to Use Playready](license-to-use-playready.md)

[PlayReady Compliance and Robustness Rules](compliance-and-robustness-rules.md)

[PlayReady Certificates and Certificate Authority](certificates.md)

[PlayReady Secure Clock Services](secure-clock-services.md)

[PlayReady Test Server](test-server.md)
