---
author:
title: "PlayReady Interoperability With Other Protection Technologies"
description: ""
ms.assetid: "4bd6d175-18c2-1014-3762-73379579bbc5"
kindex: content, about moving PlayReady
kindex: moving, about PlayReady content
kindex: about, moving PlayReady content
kindex: PlayEnabler, moving PlayReady content
keywords:  about moving PlayReady content,  about PlayReady content moving,  moving PlayReady content about
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Interoperability With Other Protection Technologies


PlayReady systems are able to interoperate with other content protection systems through the following features discussed in this topic:  

   *  Common Encryption

   *  Play Enablers

   *  Copy Enablers (depracated)

   *  Move Enablers (depracated)

   *  Import and Export


## Common Encryption



## Play enablers  

A **PlayEnabler** object represents a technology that content from a PlayReady client is allowed to flow through for play.

For example, a PlayReady client playing protected content and passing the audio and video to a AirPlay receivers, using the AirPlay link protection. Other examples are passing audio and video to Unknown Outputs or passing audio and video to a network protected using DTCP-IP.

These Play Enablers are optional rights that a license may contain. If they are present, the client is allowed to play and pass the audio/video signal to the corresponding output. Note that a Play Enabler involves a Export operation if passing to the corresponding output requires transcription.


## Copy Enablers

A **CopyEnabler** object represents a technology that content from a PlayReady client is allowed to copy to.

For example, a PlayReady client may decrypt PlayReady content to re-encrypt it using CSS and burn a video DVD. This operation makes a copy of the content and involves transcription.

These Copy Enablers are optional rights that a license may contain. If they are present, the client is allowed to copy the content to the corresponding output. Note that a Copy Enabler involves an Export operation if passing to the corresponding output requires transcription.

> ![](note.gif)**Note** Copy Enablers were supported up to PlayReady 2.X. They are no longer supported by clients 3.0 and above.


## Move Enablers

A **MoveEnabler** object represents a technology that content from a PlayReady client is allowed to move to.

For example, move to CPRM.

> ![](note.gif)**Note** Move Enablers were supported up to PlayReady 2.X. They are no longer supported by clients 3.0 and above.


## Import and Export

PlayReady Import designates an operation where content is initially protected using another content protection technology (for example, from company A) and then protected using PlayReady, typically in a transcryptor. What this means is the encryption keys of the protected content are protected in the other content protection license from company A when they get in the device, and are protected in a PlayReady license when they get out of that device. It can involve transcrypting the content (decrypting the content, and re-encrypting the content using different keys), or simply by repackaging the encryption keys. It may also involve transcribing the rights and right restrictions from the content protection technology from company A to PlayReady extensible media rights (XMR).

A device (such as a portable device) must acquire content. If the content contains an extensible policy that enables content to be copied to another device, then the device may copy the content to another device.

When copying protected content to another device, the device needs to repackage the content. The content is protected on the device containing the data. The data, once repackaged, is copied to another device. The transmitting device will then create a new license (that may have different restrictions than the content�s original license) and will then transfer the license to the receiving device.

Once the receiving device has both the protected content and the license to unpackage the content, it can decrypt the content and play it back. If the license created on the transmitting device requires time-based expiration, the receiving device must support a secure clock. If the receiving device is revoked, the transmitting device will not transfer its content. If the license restricts content transfer to a domain, the device must be registered to the domain pertaining to that license.

PlayReady Export designate an operation where content is initially protected using PlayReady and then protected using another content protection technology (for example, from company A), typically in a transcryptor. What this means is the encryption keys of the protected content are protected in a PlayReady license when they get in the device, and are protected in a the other content protection license from company A when they get out of that device. It can involve transcrypting the content (decrypting the content, and re-encrypting the content using different keys), or simply by repackaging the encryption keys. It may also involve transcribing the rights and right restrictions from the content protection technology from company A to PlayReady extensible media rights (XMR).

Certain end-to-end scenarios may require protected content to be exported, from one content protection system to another, to play or copy the same content on multiple platforms and devices. For example, a consumer uses a computer to acquire subscription content that was protected with PlayReady content access technology and then wants to stream that content to a playback device on a network that only supports DTCP-IP. To play the content protected with PlayReady on that device, the protected content must be exported to DTCP-IP.

To enable this scenario, PlayReady Server SDK allows developers to specify additional content protection formats for export in an inclusive list. This inclusive list is created per license by adding GUIDs that correspond to the permitted content protection formats (adding GUIDs to the inclusive list is accomplished with the PlayEnabler class). These GUIDs and their associated rights mappings are defined in the PlayReady Server SDK Compliance Rules that accompanied your license agreement from Microsoft. The client sending content may only export the content to those content protection systems specified in the license inclusive list.
