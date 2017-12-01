---
author:
title: "Specifications"
description: ""
ms.assetid: "d8bbd962-4195-1966-c89b-f38074c1d6d6"
kindex: specifications
keywords: specifications
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Specifications


This section contains a list of public specifications that provide background information on PlayReady content access technology.

The [PlayReady Header Object Specification](https://www.microsoft.com/PlayReady/documents/) describes the PlayReady Header, which is an object that is inserted in protected content and is used by a PlayReady client to locate or acquire a license for that piece of content. It is an XML string encoded using UTF-16. This PlayReady Header includes the KIDs that are used to encrypt the content, as well as any custom attributes. An encoder that packages clear content needs to implement a PlayReady Header generator to build the header, and embed it in encrypted content. The latest version of the PlayReady Header is 4.3.0.0, introduced in 2017 to support AESCBC encrypted content, in addition to AESCTR.

The [PlayReady DRM Plug-in for Android Microsoft Specification](PlayReady_DRM_Plugin_for_Android/playreadydrmpluginforandroidspecification.md) describes the requirements for incorporating PlayReady digital rights management (DRM) in an Android app.
