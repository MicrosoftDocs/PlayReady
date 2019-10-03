---
title: "How to Determine What Features a Client Supports"
description: Describes how a server application can determine whether a client supports a given feature or not
ms.assetid: "345F02F1-4233-4D60-81CB-7403702CFEF6"
keywords: playready server client feature support
ms.date: 10/02/2019
ms.topic: conceptual
---

# How to Determine What Features a Client Supports

Starting with PlayReady Device Porting Kit Version 4.3, the client sends information about what features it supports to the License Server as part of its license acquisition challenge.  Starting with PlayReady Server SDK Version 4.3, this information is made publically available to an application via the LicenseChallenge class.  (Previous versions of the PlayReady Server SDK will ignore this information if present in the license acquisition challenge.)  This page describes how to use this feature to make decisions in a server application based on what functionality the client has implemented.

TODO

<br/><br/>

