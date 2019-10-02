---
title: "What's New"
description: An overview of changes from PlayReady version 4.0 to PlayReady version 4.3
ms.assetid: "D9B3FE09-931E-4B28-8A7A-5D422C86AB12"
keywords: playready overview version changes 4.0 4.3
ms.date: 10/02/2019
ms.topic: conceptual
---

# What's New in PlayReady Version 4.3

This page contains an overview of the most significant changes between PlayReady version 4.0 and PlayReady version 4.3.


## PlayReady Changes in Version 4.3 across Server and Device Porting Kit

The SecureStop2 feature is added. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).


## PlayReady Server SDK Changes in Version 4.3

The server can now process SecureStop2 messages. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).


## PlayReady Device Porting Kit Changes in Version 4.3

The client now sends SecureStop2 messages to the server. For more information, see [PlayReady Secure Stop](../../Features/secure-stop-pk.md).
The client can now choose to reject individual licenses during Drm_Reader_Bind.  For more information, refer to enum and structure documentation in the PlayReady Device Porting Kit source code file source/inc/drmcallbacktypes.h

