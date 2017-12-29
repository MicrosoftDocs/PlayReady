---
author: 
title: "Best Practices for License Policies"
description: ""
ms.assetid: "bfbd5264-5ac4-0359-8a6f-b8bb3db19285"
kindex: best practices, license policies
kindex: policies, best practices for license
kindex: license, best practices for license policies
keywords:  license policies best practices,  best practices for license policies,  best practices for license policies license
ms.author: 
ms.topic: conceptual
ms.prod: xbox
ms.technology: xboxone
---


# Best Practices for License Policies
   
  
This section describes best practices for programming license policies.   

<a id="begindate"></a>

## Using BeginDate with EndDate
   
  
One of the many business models PlayReady supports is content rental&mdash;content that can only be used for a limited period (for example, content may be used until 5pm EST, October 15, 2016). This is accomplished by issuing clients a PlayReady license with the EndDate set to the time and date the license is to expire.   
   
  
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
 
## Time Restrictions in Subscription Licenses
   
  
PlayReady supports a subscription business model in which users pay a monthly fee in return for access to a large content catalog offered by the service.   
   
  
In this scenario, PlayReady license servers issue leaf licenses for each content file, and a single root license. In order for PlayReady to access the content, both its leaf license and the root license (the license chain) are necessary. Both licenses must contain the action being performed on the content (for example, play) and both licenses must be valid (not expired, and so on).   
   
  
Because there is only one root license, and potentially hundreds or thousands of leaf licenses for any particular content catalog, leaf licenses should include very few (if any) restrictions, and the root license should contain time restrictions and be refreshed periodically (for example, monthly). When a subscription is about to lapse, the license server only needs to issue one license and all content will be updated with the new effective expiration date. If policy in the leaf licenses contains time-based policy, all leaf licenses would need to be re-issued to prevent the content from expiring, which would be a large performance requirement for servers.   
   
  
In summary, if content is supposed to expire using license chains, only the root license should contain the time-based policy.   
 
 
