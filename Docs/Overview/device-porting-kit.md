---
title: PlayReady Device Porting Kit
description: PlayReady Device Porting Kit contains ANSI C source code designed to help developers create portable devices for use with digital content protected with PlayReady technology.
ms.assetid: "a480bc16-79f3-a8b5-c63a-c07cba4ed963"
keywords: PlayReady Device Porting Kit overview
ms.date: 02/01/2018
ms.topic: conceptual
---


# PlayReady Device Porting Kit


PlayReady Device Porting Kit (Device PK, PK, or DPK) contains ANSI C source code designed to help developers create portable devices for use with digital content that was protected with PlayReady technology. With this porting kit, PlayReady technology can then be translated to a wide variety of system architectures using different operating system environments and various device classes such as mobile phones, set-top boxes, and portable media players.


PlayReady Device Porting Kit provides features you can use to enable your hardware devices to render protected digital content. The porting kit is a non-optimized, platform-independent, source-code implementation of a PlayReady Client.


The porting kit supports license acquisition from a License Server. The porting kit also supports metering, PlayReady domains, non-A/V content protection and extraction, secure stop, and a secure clock.


PlayReady Device Porting Kit is for integrated circuit (IC) vendors and original equipment manufacturers (OEMs) who want to implement PlayReady on operating systems other than Windows, on various processors, and in consumer electronics devices. The PlayReady API is written in C (not C++) and conforms to the ANSI C standards to maintain compatibility with most platform compilers.

<a id="ID4EX"></a>



## Features


The porting kit provides the following features:

   *  License acquisition.

   *  License management and binding for decryption.

   *  Metering.

   *  Domain join, leave, and management for groups of devices.

   *  Secure Stop.

   *  Secure Delete.

   *  Secure clock and Anti-Rollback clock.

   *  Chained licenses.

   *  Scalable licenses (for live linear TV with key rotation).

   *  ANSI C code simplifies integration on embedded devices.


<a id="ID4EZB"></a>



## Components

The Porting Kit is delivered as a Microsoft MSI file that contains the libraries, samples, tools, and source code required to create devices for use with digital content that was protected with PlayReady technology.

The Porting Kit includes the following components:

   *  The source code form of PlayReady.

   *  Applicable test certificate.

   *  Specifications and associated documentation and libraries in object code form.

   *  Test media.


## See also

 [Integrating PlayReady in Devices](integrating-in-devices.md)
