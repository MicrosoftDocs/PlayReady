---
author:
title: "Porting Kit Version Compatibility with Server SDK Versions"
description: ""
ms.assetid: "e8840970-b510-dd44-9481-0d670775daf9"
kindex: porting kit, version compatibility with Server SDK
kindex: Server SDK, version compatibility with porting kit
keywords:  version compatibility with Server SDK porting kit,  version compatibility with porting kit Server SDK
ms.author:
ms.topic: conceptual
ms.prod: xbox
ms.technology: xboxone
---


# Porting Kit Version Compatibility with Server SDK Versions


The following table lists the compatibility between the various PlayReady Device Porting Kit and PlayReady Server SDK versions:

| &nbsp;| Server SDK v1.5.2| Server SDK v2.1 and Server SDK v2.9| Server SDK v3.0| Server SDK v4.0 |
| --- | --- | --- | --- | --- |
| PK v4.x| No| Yes | Yes | Yes |
| PK v3.x| No| Yes| Yes| Yes |
| PK v2.5 and v2.11| Yes| Yes| Yes| Yes |


&nbsp;

Even though PlayReady v3.x based clients should work against a server running Server SDK v2.1 or v2.9, Microsoft recommends that customers running Server SDK v1.5.2 upgrade to Server SDK v3.0 instead of upgrading to Server SDK v2.1 or v2.9. This will ensure that you are on a much more supportable path.


For more information on PlayReady Device Porting Kit and PlayReady Server SDK compatibility and migration considerations, see the *Compatibility and Migration Considerations for PlayReady 3.0* white paper on the [PlayReady Documents](https://www.microsoft.com/playready/documents/) website.
