---
author: 
title: "Scenario: Live TV"
description: ""
ms.assetid: "9c919b0f-c860-9d89-1297-16922e8de0e4"
kindex: scenarios, Live TV
kindex: Live TV, scenario
keywords:  Live TV scenarios,  scenario Live TV
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Scenario: Live TV
   
  
In the live TV scenario, a service sends live streams to users and users' clients on the Internet (Over The Top, OTP) or in a closed network (IPTV for operators).   
   
  
The client may be a TV set, a phone application, a tablet, a PC, or any PlayReady embedded device.   
   
  
Standard PlayReady licenses may be used. In this case, a channel in a bundle will have its own KID and encryption key, and clients willing to consume this channel request a PlayReady license for this KID.   
   
  
In many cases, the service may want to change (that is, rotate) the encryption key of each channel sometimes, typically every 24 hours, every week, or every month. Simple PlayReady licenses can manage this scenario; however the client will have to reacquire a license for a channel every time the channel's key rotates, which might not be seamless (the user will experience a short drop out).   
   
  
In addition, the service may have dozens, hundreds, or thousands or channels available, and hundreds of different combinations (bundles) available to users depending on the level that they pay, and their geography.   
   
  
A more sophisticated and scalable way of implementing a large scale TV protection system is to leverage PlayReady scalable licenses with key rotation. In this model, the license of each channel is chained, and a scalable root license and leaf license are needed to consume the content. A scalable root license gives access to the TV bundle that a user has registered. The root license can also contain the region information to which the client belongs; the region information is used when clients in a specific region need to be blacked out for a specific TV service. A scalable leaf license is embedded in the content itself (typically in a pssh box of a MP4 stream, or in a ECM segment of a TS stream), and it contains an encrypted version of the channel key. 
   
  
Both the root and leaf keys in a live TV scenario should be rotated to ensure maximum robustness, to optimize the head end, and monetize a pay channel through pay-per-view.   
   
  
Note that PlayReady scalable licenses with key rotation also allows you to implement the following optimized backend architecture for both Live TV and pay per view:   
 
   *  A live channel is encrypted using scalable leaf licenses, and the key is rotated at each program boundary. The channel is archived and encrypted, and each program is delivered to non-subscribers as a single piece of video, in a pay-per-view model.   

   *  A live subscriber of the service gets a scalable license that gives access to all the leaf licenses of this channel. This user pays a subscription fee per month.   

   *  A non subscriber downloads a particular program and acquires a simple license for this particular program. This user pays a single fee per program downloaded, which may vary depending on the rights he paid for (such as download to own, rent for 48 hours, rent in 4K quality for 48 hours, and so on).   

 
<a id="ID4EMB"></a>

   
  
