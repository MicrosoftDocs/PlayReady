---
author: 
title: "Working with PlayReady"
description: ""
ms.assetid: "53B49621-E528-43FA-B054-BB38442DF666"
kindex: working with PlayReady
kindex: PlayReady, working with
keywords:  to Microsoft PlayReady content access technology introduction,  introduction to Microsoft PlayReady content access technology
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Working with PlayReady

This topic discusses the parts of PlayReady that are supplied to client and server developers and the parts that must be supplied by you (depending on what parts of PlayReady you are going to develop).

If you are an original equipment manufacturer (OEM), a PlayReady client developer, or a PlayReady service provider, you must first obtain a PlayReady license from Microsoft before you can begin developing your product. This will entitle you to receive from Microsoft all of the material you will need to create your product, whether it is an integrated circuit with built-in PlayReady functionality, a PlayReady app running on Windows, iOS, or Android, or a PlayReady server supplying licenses for specific content.

Content providers are not required to develop either a PlayReady client or a PlayReady server to supply licenses for your content. Instead, you could obtain these services from third-party developers. In addition, if you are developing an encoder, you only need to add a PlayReady header object to your encryptor. However, you should read through the next sections to help understand the services that are available to you. 

## PlayReady parts supplied by Microsoft

The following sections describe the parts of PlayReady that are supplied by Microsoft.

### License to use PlayReady

If you are an original equipment manufacturer (OEM), a PlayReady client developer, or a PlayReady service provider, you must first obtain a PlayReady license from Microsoft before you can begin developing your product. This will entitle you to receive from Microsoft all of the material you will need to create your product, whether it is an integrated circuit with built-in PlayReady functionality, a PlayReady app running on Windows, iOS, or Android, or a PlayReady server supplying licenses for specific content.

There are separate licenses depending on what type of PlayReady product you intend to produce. For example, there are licenses for distributing a device, developing a downloadable software application, or developing server applications or deploying a PlayReady service to end-users. For more information about all of the licensing options for the various parts of PlayReady, see [PlayReady Licensing Options](https://www.microsoft.com/playready/licensing/).

If you are a content provider using third party PlayReady clients and PlayReady servers, you do not need a license from Microsoft to encrypt your content with a PlayReady header. In addition, if you are an encryptor developer, you do not need a license from Microsoft to include a PlayReady header insertion function in your encryptor code. See [What you supply](workingwithplayready.md#whatyousupply) for more information.

### Compliance and Robustness Rules

All Microsoft PlayReady final products you develop must satisfy the requirements set out in the Compliance Rules and Robustness Rules as specified in your PlayReady license agreement(s). Compliance Rules specify the required behaviors of your PlayReady implementations and software accessing your implementations, and describe how content may be accessed and passed using specific policy rules. Robustness Rules specify different PlayReady assets and the levels of robustness required to protect each asset type. For more information, see the [PlayReady Compliance and Robustness Rules](https://www.microsoft.com/playready/licensing/compliance/).

### Certificates

A certificate is a digitally-signed binary document used to grant and revoke privileges to devices to perform specific operations. You can request several different types of certificates depending on your needs.

Certificates generally fall into two main categories: server certificates and client certificates. Server certificates allow you to run the PlayReady Server SDK; client or device certificates allow groups of devices (domains) to play content. There are also test certificates, which are only used for test devices and can be revoked at any time.

Complete information about certificates and how to obtain different types of certificates is contained in the PlayReady Documentation Help file that is supplied to PlayReady licensees.

### PlayReady root CA certificate service

All certificates Microsoft provides to you are signed with a PlayReady root certificate authority (CA) certificate to ensure the security of the certificate. The company certificate you use when creating client model-level and unit-level certificates ultimately rely on the PlayReady root CA certificate to ensure authenticity of each of these certificates. In addition, all PlayReady server certificates (deployment, domain CA, and metering certificate) are signed with a PlayReady root CA certificate.

### PlayReady Server SDK

PlayReady Server SDK is delivered as two Microsoft MSI files that contain the libraries, samples, and tools required to develop a PlayReady license server, PlayReady domain server, PlayReady metering server, PlayReady secure stop server, or PlayReady secure delete server. In addition, you will also be supplied with the PlayReady documentation and any additional current information in the PlayReady Server SDK readme file.

For more information on PlayReady Server SDK, see [PlayReady Server SDK](playreadyserversdk.md).

### PlayReady Device Porting Kit

PlayReady Device Porting Kit is delivered as a Microsoft MSI file that contains the libraries, samples, tools, and source code required to create portable devices for use with digital content that was protected with PlayReady technology.

For more information on PlayReady Device Porting Kit, see [PlayReady Device Porting Kit](playreadyportingkit.md).

### PlayReady on Windows

You can create Universal Windows Platform (UWP) applications capable of providing PlayReady content to the user while enforcing the access rules defined by the content provider. Windows 10 PlayReady documentation can be found at [PlayReady for Windows 10](https://msdn.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk). Samples of PlayReady Windows 10 applications can be found at [PlayReady sample Universal Windows Apps for Windows 10 (Javascript/C#/EME)](https://code.msdn.microsoft.com/windowsapps/PlayReady-samples-for-124a3738).

You can also create PlayReady Windows Store and Web applications for Windows 8.1. Windows 8.1 PlayReady documentation can be found at [Developing PlayReady Windows Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx). Samples of PlayReady Windows 8.1 applications can be found at [PlayReady sample for Windows 8.1 Store apps](https://code.msdn.microsoft.com/windowsapps/PlayReady-sample-for-bb3065e7).

### PlayReady on Azure

Microsoft Azure Media Services provides a service for delivering PlayReady DRM licenses. Media Services also provides APIs that let you configure the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user plays back protected content. When a user requests PlayReady protected content, the player application will request a license from the AMS license service. The AMS license service will issue a license to the player if it is authorized. A PlayReady license contains the decryption key that can be used by the client player to decrypt and stream the content.

For more information about PlayReady on Azure, see [Announcing Azure Media Services Live Streaming With PlayReady encryption capability](https://azure.microsoft.com/en-us/blog/announcing-azure-media-services-live-streaming-with-playready-encryption-capability/) and the Azure [Protecting Content Overview](https://docs.microsoft.com/en-us/azure/media-services/media-services-content-protection-overview).

### PlayReady on iOS and Android

You can use the PlayReady Client SDK for iOS to create apps capable of providing PlayReady content to the user while enforcing the access rules defined by the content provider. Information about how to develop PlayReady capable applications can be found in the PlayReady Client SDK for iOS in the PlayReady documentation supplied to licensees.

You also map digital rights management plug-ins on Android to PlayReady calls. For more information on how to use these PlayReady calls, see [PlayReady DRM Plug-in for Android Microsoft Specification](playreadydrmpluginforandroidspecification.md).

### PlayReady documentation

Microsoft supplies all of the documentation that describes how to develop and deploy many types of PlayReady clients and servers. The following list contains the various sources for PlayReady documentation. Some of these sources are public, whereas others can only be observed by PlayReady licensees.

   *  [PlayReady Public Documents](https://www.microsoft.com/playready/documents/)

      Contains white papers and public technical specifications for PlayReady. This website is public and can be viewed by anyone.

   *  [PlayReady for Windows 10](https://msdn.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk)

      Describes how to implement a PlayReady client on Windows 10. This website location is public and can be viewed by anyone.

   *  [Developing PlayReady Windows 8.1 Store and Web Apps](https://msdn.microsoft.com/en-us/library/windows/apps/xaml/dn468834.aspx)

      Describes how to implement a PlayReady client on Window 8.1. This website location is public and can be viewed by anyone.

   *  PlayReady Documentation

      Describes how to implement PlayReady servers and client, including all of the API documentation associated with both. This Help file is provided to you after you have signed a licensing agreement with Microsoft.

   *  [PlayReady Training Slides](http://wmlalicensing.com)

      Provides training slides that describe how to implement PlayReady clients and servers. This website is restricted to licensees. 

   *  [PlayReady Training Video Recording](http://test.playready.microsoft.com/Home/Trainings)

      Provides video training and PlayReady conference videos that describe in detail aspects of PlayReady implementation. This website is restricted to licensees and requires an authorization token.

### PlayReady Test Server

The PlayReady Test Server website includes documentation and test tools for PlayReady developers to test your products. Whether you are a PlayReady licensee or a non-licensee, an OEM, SOC vendor, a client developer, and application developer, an encoder vendor, or a service developer, this website provides you with the following tools:

   *  A test license service
   *  Test video content (audio and video)
   *  Test audio content
   *  Test applications (HTML/JS, Silverlight)

> ![](../images/note.gif)**Note** Content and licenses delivered from this website are public and do not provide the level of security required for a production service.

The PlayReady Test Server is provided as an optional service to PlayReady developers. You do not need to use this service to test or certify your PlayReady implementations. For more information, see the [PlayReady Test Server](http://test.playready.microsoft.com/) website.

### SecureTime service

SecureTime is an optional Microsoft-provided service that allows OEMs (Original Equipment Manufacturers) to build such clocks that securely synchronize time information from the server in the TEE (Trusted Execution Environment), reaching SL3000 (Security Level 3000). It uses functions in the PlayReady Device Porting Kit (PK), HTTPS protocols, and Azure Web Services.

SecureTime is provided as an optional service by PlayReady.

<a id="whatyousupply"></a>
## What you supply

What you supply to implement PlayReady depends entirely on what you are trying to develop. Basically, you can develop PlayReady functionality for clients or servers. However, you don't actually have to develop either one if you are a content provider; instead, you could obtain both from a third-party developer. In addition, you don't need to develop either one if you are adding PlayReady functionality to your encoder; you only have to add a PlayReady header during the encoding process. This section will try to clarify all of the different ways you can use PlayReady, and provide guidance on what you will need to supply for each type of product.

### PlayReady client

If you are going to develop a PlayReady client

#### Device on which to install the PlayReady Device Porting Kit

#### Application using the PlayReady Device Porting Kit

#### Windows or Xbox application

#### Hardware versus software DRM

### PlayReady server

If you are going develop a PlayReady server, 

#### PlayReady license server

#### PlayReady domain server

#### PlayReady metering server

#### PlayReady secure stop server

#### PlayReady secure delete server


Software as a Service (SaaS). The capability provided to the consumer is to use the provider's applications running on a cloud infrastructure. The applications are accessible from various client devices through either a thin client interface, such as a web browser (e.g., web-based email), or a program interface. The consumer does not manage or control the underlying cloud infrastructure including network, servers, operating systems, storage, or even individual application capabilities, with the possible exception of limited user-specific application configuration settings.

Platform as a Service (PaaS). The capability provided to the consumer is to deploy onto the cloud infrastructure consumer-created or acquired applications created using programming languages, libraries, services, and tools supported by the provider. The consumer does not manage or control the underlying cloud infrastructure including network, servers, operating systems, or storage, but has control over the deployed applications and possibly configuration settings for the application-hosting environment.

Infrastructure as a Service (IaaS). The capability provided to the consumer is to provision processing, storage, networks, and other fundamental computing resources where the consumer is able to deploy and run arbitrary software, which can include operating systems and applications. The consumer does not manage or control the underlying cloud infrastructure but has control over operating systems, storage, and deployed applications; and possibly limited control of select networking components (e.g., host firewalls).

ASP - Application Service Provider


 
