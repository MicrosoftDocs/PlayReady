---
author: rolandlefranc
title: Integrating PlayReady in Devices
description: This topic provides a brief description on the different ways to implement a DRM client in a device and how to develop applications using DRM.
ms.assetid: "B58235E5-3E78-44CA-8BDE-22961773DDF4"
keywords: client, architecture, porting kit, pk, dpk, integration, embedded
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Integrating PlayReady in Devices

This topic provides an overview of the process for a device maker to integrate a PlayReady Client in his device.

The imtegration of a PlayReady Client in a device is great value. It ensures applications will have access to the best content protection on the device and make easier the implementation of all sorts of video and audio services on the device.


## Architecture


The following figure shows the PlayReady PK components and how they fit in a device software stack.

![Porting Kit Architecture](../images/pk_in_device.png)


## Process for development, integration and self-certification

1. License the PlayReady Porting Kit (DPK) from Microsoft

2. Port the DPK onto the platform

    1. Compile the DPK for the platform
    2. Adapt the functionality in the OEM functions of the DPK to the platform, to provide the basic services needed by the DPK (memory, clock, encryption accelerators, video path, etc.)
    3. Integrate the DPK with the video and audio player
    4. Create an application that enables PlayReady operations on the device, or an API exposed in a SDK that will allow multiple application developers to use them.

3. Validate the port with respect to the Compliance and Robustness Rules requirements. 

    1. Test the device towards all applicable requirements.
    2. Fix any non conformance found. Re-test.
    3. Optionally use a third party security house or test house

4. Prepare the device secrets (model-level client certificate and associated private keys, or unit-level client certificate provisioning service)

5. Manufacture and distribute the device to the market

6. Quarterly report volumes to Microsoft and pay royalties


### Integrating a PlayReady-enabled Chip in a Device

If you are designing a device with PlayReady installed in hardware or PlayReady on an integrated circuit, it is up to you to supply any hardware or software required to port the PlayReady Device Porting kit to your hardware. Some integrated circuits designed by [PlayReady Partners](https://www.microsoft.com/playready/partners/) already have PlayReady installed on the chip, and you could use these integrated circuits while designing your device.

For general information about developing hardware-based PlayReady, see [Hardware versus software DRM](security-level.md#hardwarevssoftware).