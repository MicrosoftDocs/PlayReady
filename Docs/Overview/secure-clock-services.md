---
author: rolandlefranc
title: "PlayReady Secure Clock Services for PlayReady Clients"
description: ""
ms.assetid: "27BE5F0E-C171-4091-BACE-A029C6FE53B5"
kindex: SOAP, PlayReady protocols
kindex: protocols, PlayReady communication
kindex: communication, PlayReady SOAP
keywords:
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Secure Clock Services for PlayReady Clients

Microsoft operates a service to which a PlayReady client can connect to acquire the current time and set their trusted clocks. Their trsuted clock is used to enforce PlayReady time-based policies, such as content rental expiration.

Microsoft runs multiple versions of these services depending on the version and security level of the client requesting the time.


<table>
<tr> <th>

Version</th> <th>

Name&mdash;Links</th> <th>

Porting Kit</th> </tr>

<tr> <td>1</td> <td> Secure Clock V1 <br/>  &nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=25812<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=25817<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=88262<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?linkid=830192<br/>forwards to the https url for the clock service:<br/>&nbsp;&nbsp;https://secureclock2.playready.microsoft.com/secureclock/?petition<br/><br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?linkid=861602<br/>forwards to the http url for the clock service:<br/>&nbsp;&nbsp;http://secureclock2.playready.microsoft.com/secureclock/?petition  </td> <td> All WMDRM 7 (2002) <br/>All WMDRM 10.08 (2006) <br/>All PR PK 1.0 (2008) <br/>All PR PK 1.2 (2008) <br/>Some PR PK 2.0 (2011) <br/>Some PR PK 2.5 (2013) </td> </tr>

<tr> <td>2/3</td> <td> SecureClock V2/V3 <br/>(nicknamed Secure Clock VISTA) <br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=130559<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=149408<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=799153   <br/>forwards to the https url for the clock service:<br/>&nbsp;&nbsp;https://secureclock2.playready.microsoft.com/secureclock/vista_rtm/?petition<br/><br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?linkid=861603<br/>forwards to the http url for the clock service:<br/>&nbsp;&nbsp;http://secureclock2.playready.microsoft.com/secureclock/vista_rtm/?petition  </td> <td> Some PR PK 2.0 (2011) <br/>Some PR PK 2.5 (2013) <br/>All PR PK 2.11 (2014) <br/>All PR PK 3.0 (2015) <br/>(REE Only) </td></tr>



<tr> <td>4</td> <td> Secure Clock V4 <br/>(nicknamed Secure Time) <br/>&nbsp;&nbsp;https://go.microsoft.com/fwlink/?LinkID=746341  <br/>forwards to the https url for the clock service:<br/>&nbsp;&nbsp;https://securetime.playready.microsoft.com/SecureTime <br/> <br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=746259<br/>forwards to the http url for the clock service:<br/>&nbsp;&nbsp;http://securetime.playready.microsoft.com/SecureTime  </td> <td> All PR PK 3.2+ (2016) <br/>(REE or TEE) </td>  </tr>
 </table>
