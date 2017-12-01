---
author:
title: "PlayReady and Silverlight"
description: ""
ms.assetid: "cfce96cc-41c3-cd90-f872-66a503fcfb13"
kindex: PlayReady and Silverlight
keywords:
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady and Silverlight


The commercial media industry is undergoing a major transition as content providers move away from proprietary
web plug-in based delivery mechanisms (such as Flash or Silverlight), and replace them with unified plug-in free
video players that are based on HTML5 specifications and commercial media encoding capabilities. Browsers are
moving away from plug-ins as well, as Microsoft Edge is with ActiveX, and toward more secure extension models.

The transition to plug-in free media has been enabled through the recent development of new specifications:

  * From W3C: Media Source Extensions for adaptive streaming and Encrypted Media Extensions for content protection.

  * From the Moving Picture Experts Group (MPEG): DASH and Common Encryption (CENC).

These specifications were designed and developed to enable interoperable streaming to a variety of media platforms
and devices. By focusing on interoperable solutions, content providers are able to reduce costs and at the same
time users are able to access the content they want on the device they prefer using the application or web browser of their
choice. Microsoft believes that this is a huge benefit to both content producers and consumers, and is committed
to supporting companies that make this transition.

With these changes in mind, support for ActiveX has been discontinued in Microsoft Edge, and that includes removing
support for Silverlight. Microsoft continues to support Silverlight, and Silverlight out-of-browser applications can continue
to use it.  Silverlight will also continue to be supported in Internet Explorer 11, so sites continue to have
Silverlight options in Windows 10. At the same time, Microsoft encourages companies that are using Silverlight for
media to begin the transition to DASH/MSE/CENC/EME based designs and to follow a single encoding work flow enabled
by CENC. This represents the most broadly interoperable solution across browsers, platforms, content,
and devices going forward.

To continue to support Windows 7, Microsoft recommends that you develop a Silverlight out-of-browser application. To do this:

  * If the service already has one in-browser application, then the conversion is trivial. If not, it should be developed
  in C# so that it can share most of its code with Universal Windows Platform (UWP) applications designed for other Microsoft platforms, like Windows 10 or
  XBox.

  * Optionally add a standalone installer. This helps users get through the hurdle of installing the application on supported browsers and browser versions.

To continue to support Silverlight on the Mac:

  * Do the same as described for Windows 7 above.

  * Or, use a PlayReady SDK provided by a PlayReady partner. The SDK may be an Electron SDK, or any other type for
  Mac native applications. For more information, see the [list of PlayReady partners](https://www.microsoft.com/playready/partners/).

