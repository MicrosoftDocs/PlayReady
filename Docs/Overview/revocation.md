---
title: PlayReady Revocation
description: When Microsoft identifies a Client with compromised security, the device may be revoked and added to a revocation list.
ms.assetid: "09869289-666b-272e-1cc2-97079cb71204"
keywords: playready revocation,  revocation list
ms.date: 02/01/2018
ms.topic: conceptual
---


# PlayReady Revocation

## What is PlayReady Revocation

Revocation is a process to identify clients that have compromised security, and prevent those clients from getting access to additional licenses for decrypting content that has been protected.


When Microsoft identifies a client with compromised security, the device may be revoked and added to a revocation list. The revocation list is periodically downloaded by the License Servers that issue licenses for protected content. License Servers use this revocation list to deny licenses to devices that have been revoked, thereby preventing the device from playing newly protected content.


Revocation lists are refreshed on devices when they are not up to date. The revocation list may also be issued with licenses. The DRM component on the device checks this revocation list before transferring content to other devices. By preventing communication with revoked components, revoked applications no longer work. Once revoked, the only way to fix the situation is to replace the revoked element or remove the revoked component from a newer version of the revocation list.


## Link to the current PlayReady Revocation Lists

Microsoft builds and maintains the revocation list and its versioning structure. PlayReady customers can download this list from the following link:

**PlayReady Revocation List(https): [https://aka.ms/revinfo](https://aka.ms/revinfo)**

**PlayReady Revocation List(http): [http://go.microsoft.com/fwlink/?LinkId=110086](https://go.microsoft.com/fwlink/?LinkId=110086)**

## Requirement for PlayReady Servers

Per the requirements of the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/), companies operating a PlayReady Server "must update the PlayReady Server Software Development Kit certificate revocation lists for each PlayReady Server once a week". This ensures any compromised client gets its license requests declined in a reasonable time frame after its addition by Microsoft to the Revocation List.

## Ignoring Individual Entries in the PlayReady Revocation List

TODO

