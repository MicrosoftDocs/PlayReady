---
author: dougklopfenstein
title: Preparing a Packager for PlayReady
description: Discusses the requirements and time required to prepare a packager for PlayReady functionality
ms.assetid: "FE42F0CE-754B-43C4-B661-EF4DC16B0294"
keywords:  PlayReady, packager, encryptor, preparing packager
ms.author: v-doklo
ms.date: 05/11/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Preparing a Packager for PlayReady

Companies developing an encoder or a packager (also known as encryptor) utilizing PlayReady technologies need to integrate two functionalities in their product:

* One that encrypts content in a PlayReady compatible encryption format.

* Another that generates a PlayReady Header and inserts it in the encrypted content.

>[!NOTE]
>A PlayReady licensing agreement is not necessary to build a PlayReady encoder or packager. In addition, there is no royalty applicable to PlayReady encoders or packagers.

## Outline

Do you need a PlayReady license - no

Are there any fees to insert PlayReady in content - no

Are there any royalty payments - no

Encrypt using more than one DRM - yes

Need to store keys - key management system (yes), Key Seed (no)

Need to generate keys - yes (key generator)

Need PlayReady Server - yes (your own or partner's)

    Used to supply the key value for your content

    If your own, you need a PlayReady deployment certificate

    Are there any fees for the PlayReady Server SDK - no

    Are there any royalty payments - no

    Describe how to get the deployment certificate and how long it takes

Development time

	Packager

	Key Generator

	Key Management System

	Server (optional)

    Testing
