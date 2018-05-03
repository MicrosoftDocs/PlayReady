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


# Concurrency Limiting Playback

Two PlayReady functionalities can be used by a service to limit the number of concurrent playback across devices from a user account.

For example, Mr Smith pays a 2-stream maximum plan at Service Contoso.
Mr Smith, Ms Smith, their daughter. Explain the scenario with an example.

## Using SecureStop

The first option uses SecureStop (supported on PlayReady 3.0 or higher).
With SecureStop, a player will send a trusted event to the license server when it stops playing a stream or file. You can use this to allow another client to start playback depending on the number of players the server knows are currently playing and the service logic. This is the preferred option, it is implemented by several large services. You have the issue that a player may disappear from the network before it has sent its SecureStop event. So the logic on the license server must allow some margin.

Here, include a lot more on how it works, from the CHM

## Using Limited Duration Licenses

Limited Duration Licenses (LDL) is a nickname for PlayReady licenses with a short duration (e.g. expire one minute after delivery) and with the RealTimeExpiration restriction enabled (means the player is required to enforce the expiration whenever it occurs during a playback session, not only at the beginning of a playback session - see the Compliance Rules section xxx)

Use short duration licenses that are renewed frequently. When a player plays a stream, it receives a license for only 1 minute, and this license includes the RealTimeExpiration restriction which requires the player to check for expiration in real time during a playback session (PlayReady 3.0 or higher). That license is renewed 30 seconds later through a proactive license acquisition triggered by the app. At the end of the first minute, the player binds automatically and seamlessly to the second license, for another minute of playback. We have a demo app that shows it works on Windows 10, but I don’t think it’s ever been deployed in a production service.

Tell more
Also, recommend to have a Delete restriction in the licenses to have them flushed out of the client sometimes
Also, tell if the licenses should be persistent or non persistent
