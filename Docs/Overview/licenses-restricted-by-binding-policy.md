---
author: rolandlefranc
title: Licenses Restricted by Binding Policy
description: Licenses may be bound to entities such as a Client or a domain.
ms.assetid: "02874cfb-f124-7be2-0319-6a8c15197f99"
keywords:  restricted licenses, licenses restricted by binding, machine binding, domain binding
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Licenses Restricted by Binding Policy


Licenses may be bound to entities such as a client or a domain. Client binding&mdash;that is, machine-binding, binding a license to a personal computer, a smartTV, a mobile phone, or any other connected device&mdash;is the simplest form of license binding.

<a id="ID4E5"></a>



## Client binding


Each PlayReady Client is uniquely identified to the License Server by a machine or application certificate, generically called a PlayReady Client Certificate. This certificate contains an ID number and one or several asymmetric key pairs. License Servers receive this certificate as part of each license request. During the generation of the license to be returned to the client, the License Server will bind and encrypt the license information towards the client public key found in the client Certificate, so that the client can use its private key to decrypt and access the license information. This license information includes the content encryption key, which allows the client to decrypt content using that license.


The simplest form of license binding is when a License Server binds the license to the machine itself.

<a id="ID4EHB"></a>



## Domain binding


Alternatively, License Servers can bind the license to an abstract group of clients, named a PlayReady domain (PlayReady domains are not the same as NTFS domains). This domain also has the same type of certificate, including an ID, and an asymmetric key pair.


If a client (device or application) receives a domain-bound license, it needs to join the related domain (for example, acquire from the service a domain certificate) to be able to access the license information. A client joining a domain requires a HTTP transaction similar to a license acquisition, called a domain join operation.

<a id="ID4EQB"></a>



## Note on XMR


Microsoft PlayReady systems describe content usage policies in licenses based on extensible media rights (XMR). The framework established by XMR allows new objects to be introduced in a backwards-compatible fashion, as well as adding new extended XMR objects without breaking backwards compatibility. For example, an extension could be added that allows content to be copied from a device without breaking backwards compatibility with parsers that do not understand that policy.

