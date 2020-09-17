---
title: PlayReady Secure Delete Server
description: The PlayReady Secure Delete feature allows service providers to receive secure acknowledgement when a persistent license is deleted by the app on the Client.
ms.assetid: "012a9779-4bc0-450f-a1ec-ef93c9d25a8e"
keywords: secure, delete, server, license, deletion, remove
ms.date: 02/01/2018
ms.topic: conceptual
---


# PlayReady Secure Delete Server

Introduced in PlayReady version 4.0, *PlayReady Secure Delete* is a feature that allows service providers to receive secure acknowledgement when a persistent license is deleted by the application on the client. Previously, when a license was deleted, service providers were not notified when deletion was completed. With PlayReady Secure Delete, the following operations are possible.

* Service providers can track which licenses are currently stored and which licenses have been deleted, on a given client machine.
* Service providers can issue a specific number of persistent licenses to a client, and track the count of licenses on that client’s machine.
* The Secure Delete feature also satisfies the [Encrypted Media Extensions (EME) specification](http://www.w3.org/TR/encrypted-media/) requirement for a "record of license destruction" as defined in September 2017, which specifies that such a record must be sent to the Server upon license deletion.



## See also

[PlayReady Secure Delete](../Features/secure-delete-pk.md)