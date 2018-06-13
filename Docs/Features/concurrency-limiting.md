---
author: rolandlefranc
title: Stream concurrency limiting
description:
ms.assetid: "983f2084-d2c6-46d6-875d-c89082c2394a"
keywords: secure, stop, stream concurrency limiting
ms.author: rolefran
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Concurrency Limiting

With PlayReady, a service can limit the number of concurrent playback sessions across devices from a user account. For example, if Mr. Smith pays for a 2-stream maximum plan at Service Contoso, the service needs to keep count of how many clients are currently streaming content.

There are two PlayReady features that you can leverage, to limit the number of concurrent playback sessions:

* Secure Stop
* Limited Duration Licenses

## Using Secure Stop

You can use Secure Stop, supported in PlayReady 3.0 or higher, to limit the number of concurrent playback sessions across devices.
With SecureStop, a player will send a trusted event to the license server when it stops playing a stream or file. You can use this to allow another client to start playback, depending on the number of players the server is aware of that is currently playing, and the service logic. This is the preferred option, and is implemented by several large services. In some cases, a player may disappear from the network before it has sent its SecureStop event, so the logic on the license server must be set in place to handle this case.

For more information, see [Scenario: Subscription Content](scenario-subscription-content.md).

## Using Limited Duration Licenses

Limited Duration Licenses (LDL) are PlayReady licenses with short duration (e.g. expires one minute after delivery) and with the RealTimeExpiration restriction enabled. *RealTimeExpiration restriction enabled* means that the player is required to enforce the expiration not only at the beginning of a playback session, but also at regular intervals during playback. For more info, see the *Definition 1.182* of the [Defined Terms for the Compliance and Robustness Rules](https://www.microsoft.com/playready/licensing/compliance/).

LDLs use short duration licenses that are renewed frequently. When a player plays a stream, let's say that it receives a license for only 1 minute. This license includes the RealTimeExpiration restriction which requires the player to check for expiration in real time during a playback session (applies to PlayReady 3.0 or higher). The license is then renewed 30 seconds later through a proactive license acquisition, triggered by the app. At the end of the first minute, the player binds automatically and seamlessly to the second license, for another minute of playback.

Because licenses expire every minute in this case, it is good practice to manually clean up the data store (HDS) by using the Removal Date Object. It is up to the license server to include this extra policy in the license that is delivered to the client.

We recommend that device makers design their devices to clean up the license store periodically (e.g. every day or at every boot), in order to quickly remove cluttered licenses.

Note that even though LDLs can be persistent or non-persistent, we recommend implementing LDLs as non-persistent. For example, if LDLs expire within one minute of delivery, using LDLs in a persistent way would take up a substantial amount of resources. However, if you do decide to implement LDLs as persistent licenses, we suggest you apply the *Removal Date Object* in order to maintain a clean data store.

## See also

[Secure Stop](secure-stop-pk.md)