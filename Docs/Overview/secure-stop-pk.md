---
author: rolandlefranc
title: PlayReady Secure Stop
description: PlayReady Secure Stop is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content.
ms.assetid: "9736c55e-3628-4d93-8d55-48d4be6af137"
keywords: secure, stop, server, license
ms.author: rolefran
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Secure Stop


Introduced in PlayReady version 3.0, *PlayReady Secure Stop* is a feature that provides the means for a PlayReady device to confidently assert to a media streaming service that media playback has stopped for any given piece of content. This capability ensures your media streaming services provide accurate enforcement and reporting of usage limitations on different devices for a given account.

## Secure Stop overview

A Secure Stop event is reported to a Secure Stop Server by the client when media playback stops, either at the end of the media or because the user stopped the media presentation somewhere in the middle. A Secure Stop is also reported when the previous session ends unexpectedly (for example, due to a system or application crash).

> [!NOTE]
> Secure Stop applies only to non-persistent licenses.

![](../images/secure_stop.gif)

There are two primary scenarios for sending a Secure Stop challenge:

   *  When the media playback stops either at the end, or because the user stopped the media presentation somewhere in the middle.
   *  When the previous session ends unexpectedly (for example, due to a system or app crash). The app will need to query, either at startup or shutdown, for any outstanding Secure Stop sessions and send challenge(s) separate from any other media playback.

For information about Secure Stop in the PlayReady Client SDK, see the *[Add secure stop](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-Client-sdk#add-secure-stop)* section in the [PlayReady DRM](https://docs.microsoft.com/en-us/windows/uwp/audio-video-camera/playready-client-sdk) article.

## Secure Stop 2

In PlayReady version 4.2, *PlayReady Secure Stop 2* provides more security by adding a SecureStopAESKey, generated with a new license. That key is used during the SecureStop challenge to stop the playback session in the TEE, and the server checks for signatures upon regeneration of the key.

A service may use the SecureStop feature to enforce playback across multiple clients belonging to a same user account. Depending on the configuration of a particular client in that user account, the service will receive slightly different messages form the client.

The following table shows the Server App logic on different Client Security Level and Secure Stop versions.

| Client SL | SecureStop1 | SecureStop2 | Example | Server view |
| -- | -- | -- | -- | -- |
| 2000 | disabled | disabled | None | Use app logic as fallback |
| 2000 | enabled | disabled | | |
| 2000 | enabled | enabled | None | &mdash; |
| 3000 | disabled | disabled | | Use app logic as fallback |
| 3000 | enabled | disabled | | |
| 3000 | enabled | enabled | | The server knows for sure that the playback sessions received in the SecureStop challenge has been stopped by the TEE, making it more difficult for an attacker. |


## See also

[Secure Stop Sever](https://docs.microsoft.com/en-us/playready/overview/secure-stop-server)
