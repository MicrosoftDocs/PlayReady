---
author: rolandlefranc
title: Best Practices for License Policies
description: This section describes best practices for programming license policies in PlayReady.
ms.assetid: "bfbd5264-5ac4-0359-8a6f-b8bb3db19285"
keywords: playready license policies best practices
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# Best Practices for License Policies


This section describes best practices for programming license policies when using PlayReady technologies.

<a id="begindate"></a>

## Using BeginDate with EndDate


One of the many business models PlayReady supports is content rental &mdash; content that can only be used for a limited period (for example, content may be used until 5pm EST, October 15, 2016). This is accomplished by issuing clients a PlayReady license with the EndDate set to the time and date the license is to expire.


An EndDate is sufficient to create a rental license; however it is a better practice to also include a BeginDate in the license. A BeginDate specifies that the associated content cannot be used before the specified date. The combination of a BeginDate with the EndDate is a natural impedance to clock rollback attacks, where users backup and restore the entire PlayReady data store to avoid clock rollback events.


Consider the following example:

   *  The date is 08/01/16 - User acquires License1 for Content1. License1 has EndDate=08/30/16.

   *  The date is 09/01/16 - User acquires License2 for Content2. License2 has EndDate=09/30/16.

   *  The user makes a copy of the PlayReady data store.

   *  Before playing Content1 or Content2, the user sets back the clock to 08/01/16, restores the copy of the PlayReady data store. Both pieces of content can be played.



Now consider the same basic example, but with BeginDates in the licenses:

   *  The date is 08/01/16 - The user acquires License1 for Content1. License1 has BeginDate=08/01/16, EndDate=08/30/16.

   *  The date is 09/01/16 - The user acquires License2 for Content2. License2 has BeginDate=09/01/16, EndDate=09/30/16.

   *  The user makes a copy of the PlayReady data store.

   *  Before playing Content1 or Content2, The user sets back the clock to a date before 08/01/16, restores the copy of the PlayReady data store. Only Content1 will play.



This example shows how BeginDate naturally helps reduce the feasibility of the data store being restored to circumvent license policy. A user can make more copies of the data store to work around BeginDate, but as the number of content files grows large, the management of all the data stores necessary to work around the license policy grows in proportion, making an attack far less feasible.


In summary, when specifying an EndDate in a PlayReady license, it is best practice to also include a BeginDate.

## Setting a BeginDate value that works for the Client

When adding a BeginDate to a license, it is good practice to set it a little bit in the past, for PlayReady Clients version 1 or 2. The reason is that there might be a minor clock difference between the Server generating this license and the client receiving it, and the intend of the Server is that the client can use the license as soon as it receives it.

For PlayReady Clients 3 and higher, client sends its clock value to the License Server along the license request, and the Server can set BeginDate and other time restrictions with respect to that value, under the condition that it is close to the time value known to the License Server.

<br/>
A typical example with a PlayReady Client version 2 would be:

   1. A user rents content on Friday, January 5, 2018 around 8 PM, on an Android phone running an app built on PlayReady 2.5.

   2. The Android app initiates a license request to the License Server. The phone clock indicates 7:56PM and the License Server clock is on 8:00PM.

   3. The License Server receives the license request, detects that the client is version 2, and generates the license with:

      *  Play Right

      *  Begin Time = local Server time minus 5 minutes = January 5, 2018 at 7:55 PM

      *  Expiration Time, Expiration After First Play, other right restrictions like Output Protections

    4. The License Server sends the license back to the client.

    5. The client starts playback. The phone clock is still 7:56PM and is past the license's BeginDate which is 7:55PM, so playback can actually start now.

<br/><br/>
A typical example with a PlayReady Client version 3 would be:

   1. A user rents content on Friday, January 5, 2018 around 8 PM, on an Windows 10 computer running an UWP app.

   2. The UWP app initiates a license request to the License Server. The PC clock indicates 7:56PM and the License Server clock is on 8:00PM.

   3. The License Server receives the license request, detects that the PlayReady Client is version 3, and checks for the value of the client clock:

      *  if the client clock value is no further than the License Server clock value than 1 hour, proceed and generate the license

      *  if not, deny the license request and send a message to the client app to request that clock is set to the right value

   4. The License Server generates the license with:

      *  Play Right

      *  Begin Time = Client time contained in the license request = January 5, 2018 at 7:56 PM

      *  Expiration Time, Expiration After First Play, other right restrictions like Output Protections

    4. The License Server sends the license back to the client.

    5. The client starts playback. The PC clock is still 7:56PM and equal or past the license's BeginDate which is 7:56PM, so playback can actually start now.
<br/>
<br/>


## Time Restrictions in Subscription Licenses


PlayReady supports a subscription business model in which users pay a monthly fee in return for access to a large content catalog offered by the service.


In this scenario, PlayReady License Servers issue leaf licenses for each content file, and a single root license. In order for PlayReady to access the content, both its leaf license and the root license (the license chain) are necessary. Both licenses must contain the action being performed on the content (for example, play) and both licenses must be valid (not expired, and so on).


Because there is only one root license, and potentially hundreds or thousands of leaf licenses for any particular content catalog, leaf licenses should include very few (if any) restrictions, and the root license should contain time restrictions and be refreshed periodically (for example, monthly). When a subscription is about to lapse, the License Server only needs to issue one license and all content will be updated with the new effective expiration date. If policy in the leaf licenses contains time-based policy, all leaf licenses would need to be re-issued to prevent the content from expiring, which would be a large performance requirement for Servers.


In summary, if content is supposed to expire using license chains, only the root license should contain the time-based policy.


