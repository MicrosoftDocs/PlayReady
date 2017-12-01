---
author:
title: "Embedded Licenses"
description: ""
ms.assetid: "97eab5cb-afc4-fde8-91d2-904213fb3b54"
kindex: licenses, about embedded
kindex: about, embedded licenses
keywords:  about embedded licenses,  embedded licenses about
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Embedded Licenses


PlayReady allows an application to store the license for a DRM-protected content file in the PlayReady Object of the content file itself. Because the license is stored (or "embedded") in the content file, it is immediately available, enabling a player application to decrypt and begin playing the content without first needing to complete the license acquisition process or check the HDS store.


When a domain-bound personal computer or device acquires a license for a DRM-protected content file, it can embed the license into the content file. If the license is flagged to be embedded, the application is required to embed the license. Afterward, if the user copies the content file to another personal computer or device in the domain, the player application on the personal computer or device can play the content without needing to reacquire the license. If the user copies the content file to a personal computer or device outside of the domain, the license will not be valid and the personal computer or device must acquire a valid license before the content can be played, or join the personal computer or device to the domain. For more information on joining domains, see [Domain Management](playreadydomains.md#domain_management).


Using embedded licenses improves the user's media experience in scenarios such as the following:

   *  **Offline content**&mdash;The user acquires a content file and license, copies the content to a domain-bound personal computer or device, and then attempts to play the content later when the personal computer or device does not have access to a license server. Without an embedded license, the personal computer or device attempts and fails to acquire a license, and cannot play the content.

   *  **Content migration**&mdash;The user migrates a media library from one personal computer or device to another. Without embedded licenses, the recipient personal computer or device must reacquire a license for each content file at playback time.

   *  **Content backup and restore**&mdash;The user restores content files from a remote backup storage device. Again, without embedded licenses, the recipient personal computer or device must reacquire a license for each content file at playback time.



A license is embedded into a given content file by one of the personal computers or devices in a domain, typically whichever one acquires the content. An application should embed the license as soon as both the content and license are acquired.
