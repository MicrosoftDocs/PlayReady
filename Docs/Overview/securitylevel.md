---
author: 
title: "Security Level"
description: ""
ms.assetid: "352220F0-2566-431E-8CC3-DC649B5E3CF2"
kindex: security, level
kindex: level, security
keywords: security level, security, level
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# Security Level
## Client Security Level
The PlayReady Client Security Level is a property of the client (device or application) that defines how robust the client is against unauthorized use. The higher the Security Level is, the better the client is robust or hardened.

PlayReady currently defines three levels:

|Security Level|Purpose|Client Implementation|Version|
| --- | --- | --- | --- |
|SL150|For clients under development or under test. <p/>Not suitable for commercial content in a commercial scenario.|Any implementation is acceptable. Assets, Client Secrets, or Content Secrets are not protected at all against unauthorized use.|Any|
|SL2000|For devices and applications with the standard security consuming commercial content.|For devices and applications.<p/>Assets, Client Secrets, or Content Secrets are protected through software or hardware means.|Any|
|SL3000|For devices with the highest security consuming the highest quality of commercial content.|For devices only.<p/>Assets, Client Secrets, and Content Secrets are protected through hardware means, using a Trusted Execution Environment (TEE) of the processor. Conformant to a superset of Compliance and Robustness requirements.|PlayReady 3.0 or higher|

<br />
Illustration of a SL2000 device or application. The Final Product is hardened and verified against unauthorized use.

![Illustration of a SL2000 device. The Final Product is hardened against unauthorized use](../images/security_level_2000.png)

Illustration of a SL3000 device. The Intermediate Product is hardened and verified using a TEE, and the Final Product is hardened and verified against unauthorized use.

![Illustration of a SL3000 device.The Intermediate Product is hardened and verified using a TEE, and the Final Product is hardened and verified against unauthorized use](../images/security_level_3000.png)

## Using the Security Level
The Security Level is a property of the client defined during the development cycle. It has implications on the means that are implemented to assure the security of the Content Secrets and Client Secrets against attacks, and on the development and certification plans that the client developer makes.

License Servers can adjust the licenses, or license properties, delivered to clients based on their Security Level, by two methods.

   1. The Security Level is a property of the Client Certificate embedded in the client at manufacturing time. When a client acquires a license from a license server, it provides in the license request a copy of its client certificate. The license server receives this request and can check for the security level of the client before it delivers licenses to them. It can include logic to deliver different licenses for different clients. For example, a SL3000 client will have access to a higher resolution than the SL2000 client, and receive different licenses than than the other client. Or, it will have access to a different catalog, including theatrical releases.

   2. In addition, every license delivered includes a property called MinimumSecurityLevel, which is set to 150, 2000, or 3000 by the license server. A license server delivering a license to a client sets this value in the license. Clients binding a license verify if their own Client Security Level is equal or greater than the MinimumSecurityLevel value of the license. If it isn't, they refuse to bind and play.

![Illustration of the security levels](../images/security_level.png)
