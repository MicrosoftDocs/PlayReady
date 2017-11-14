---
author:
title: "PlayReady Communication Protocols"
description: ""
ms.assetid: "27BE5F0E-C171-4091-BACE-A029C6FE53B5"
kindex: SOAP, PlayReady protocols
kindex: protocols, PlayReady communication
kindex: communication, PlayReady SOAP
keywords:
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# PlayReady Communication Protocols

PlayReady clients communicate with PlayReady servers to acquire licenses and perform additional operations related to the management of rights set by services for clients. Clients also communicate with other services that allow them to function according to the [PlayReady Compliance and Robustness Rules](https://www.microsoft.com/playready/licensing/compliance/){:target="_blank"} (for example, to a secure clock service, which provides the trusted time and allows the client to enforce time restrictions).

![](comm_protocol.png)

## PlayReady Server&mdash;PlayReady Client Communication

Most communication between a PlayReady client and a PlayReady server are managed through the use of Simple Object Access Protocol (SOAP) messages. This communication begins when the client sends a SOAP message containing a challenge. The server responds with a SOAP message that contains a response. Both the challenge and the response contain information in XML format that signifies the type of challenge or response, and the various elements needed to process and identify the specific transaction that needs to take place.

{::comment}
The following tables lists the type SOAP messages sent between the PlayReady client and server, and includes the location of sample operations for each type.

<table>
  <tr>
    <th>Protocol</th>
    <th>API</th>
    <th>SOAP Example</th>
  </tr>
  <tr>
    <td>License acquisition</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p  style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-licenseacq-generatechallenge.html">Drm_LicenseAcq_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p  style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/LicenseResponse/licenseresponseclass.html">LicenseResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=AcquireLicense" target="_blank">AcquireLicense</a>
    </td>
  </tr>
  <tr>
    <td>License acknowledgement</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-licenseacq-generateack.html">Drm_LicenseAcq_GenerateAck</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/LicenseAcknowledgementResponse/licenseacknowledgementresponseclass.html">LicenseAcknowledgementResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=AcknowledgeLicense" target="_blank">AcknowledgeLicense</a>
    </td>
  </tr>
  <tr>
    <td>Domain join (aka domain registration)</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-joindomain-generatechallenge.html">Drm_JoinDomain_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/JoinDomainResponse/joindomainresponseclass.html">JoinDomainResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=JoinDomain" target="_blank">JoinDomain</a>
    </td>
  </tr>
  <tr>
    <td>Domain leave</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-leavedomain-generatechallenge.html">Drm_LeaveDomain_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/LeaveDomainResponse/leavedomainresponseclass.html">LeaveDomainResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=LeaveDomain" target="_blank">LeaveDomain</a>
    </td>
  </tr>
  <tr>
    <td>PlayReady metering certificate acquisition</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-metercert-generatechallenge.html">Drm_MeterCert_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/MeteringCertificateResponse/meteringcertificateresponseclass.html">MeteringCertificateResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=GetMeteringCertificate" target="_blank">GetMeteringCertificate</a>
    </td>
  </tr>
  <tr>
    <td>Metering</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-metering-generatechallenge.html">Drm_Metering_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/ProcessMeteringDataResponse/processmeteringdataresponseclass.html">ProcessMeteringDataResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=ProcessMeteringData" target="_blank">ProcessMeteringData</a>
    </td>
  </tr>
  <tr>
    <td>Process secure stop data</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-securestop-generatechallenge.html">Drm_SecureStop_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/SecureStopDataResponse/securestopdataresponseclass.html">SecureStopDataResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=ProcessSecureStopData" target="_blank">ProcessSecureStopData</a>
    </td>
  </tr>
  <tr>
    <td>Process delete license data</td>
    <td>
      <p style="margin: 0; padding: 0">Client action:</p>
      <p style="margin-left: 20px"><a href="../PK_SDK/Programming_Reference/Functions/DRM_Functions/drm-securedelete-generatechallenge.html">Drm_SecureDelete_GenerateChallenge</a></p>
      <p style="margin: 0; padding: 0">Server action:</p>
      <p style="margin-left: 20px"><a href="../Server_SDK/Programming_Reference/Classes/DeleteLicenseDataResponse/deletelicensedataresponseclass.html">DeleteLicenseDataResponse</a></p>
    </td>
    <td><a href="http://test.playready.microsoft.com/service/rightsmanager.asmx?op=ProcessDeleteLicenseData" target="_blank">ProcessDeleteLicenseData</a>
    </td>
  </tr>
</table>

&nbsp;
{:/comment}
Examples of the challenge and response SOAP messages can also be found on a PlayReady server after installing and configuring IIS for PlayReady{::comment} (see [Installing IIS on Windows Server 2008 R2](installingiis7.md) or [Installing IIS on Windows Server 2012 and 2016](installingiis2016.md), and [Configuring IIS](configuringiis7.md)){:/comment}. {::comment}To view the examples, enter **http://***yourservername***/playready/RightsManager.asmx** in a browser, then select one of the operations listed on the Web page. (Be sure to replace *yourservername* with the address of your server, or with **localhost** if you are running the browser on the PlayReady server machine.){:/comment}

{::comment}
### See Also

[Extensibility Using SOAP Headers](extensibilityusingsoapheaders.md)

[AcquirePackagingData Web Method](acquirepackagingdatawebmethod.md)
{:/comment}

## Microsoft Services for PlayReady Clients

Microsoft operates a service to which a PlayReady client can connect to acquire the current time and set their secure clocks. The following table lists information about the existing versions of the secure clock services provided by Microsoft. The Porting Kit column describes which porting kits support each of the secure clock service versions.

<table>
<tr> <th>

Version</th> <th>

Name&mdash;Links</th> <th>

Porting Kit</th> </tr>

<tr> <td>1</td> <td> Secure Clock V1 <br/>(nicknamed Secure Clock Legacy) <br/>Set up in 2002, on Microsoft premises<br/>  &nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=25812<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=25817<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=88262<br/>forwards to:<br/>&nbsp;&nbsp;https://services.wmdrm.windowsmedia.com/SecureClock/?petition  </td> <td> All WMDRM 7 (2002) <br/>All WMDRM 10.08 (2006) <br/>All PR PK 1.0 (2008) <br/>All PR PK 1.2 (2008) <br/>Some PR PK 2.0 (2011) <br/>Some PR PK 2.5 (2013) </td> </tr>

<tr> <td>2</td> <td> SecureClock V2 <br/>(nicknamed Secure Clock VISTA) <br/>Set up in 2010, on Microsoft premises<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=130559<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=149408  <br/>forwards to:<br/>&nbsp;&nbsp;https://services.wmdrm.windowsmedia.com/SecureClock/VISTA_RTM/?Petition  </td> <td> Some PR PK 2.0 (2011) <br/>Some PR PK 2.5 (2013) <br/>All PR PK 2.11 (2014) <br/>All PR PK 3.0 (2015) <br/>(REE Only) </td></tr>

<tr> <td>3</td> <td> Secure Clock V3 <br/>Set up in 2016, in Microsoft Azure<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=799153  <br/>forwards to:<br/>&nbsp;&nbsp;https://secureclock2.playready.microsoft.com/secureclock/vista_rtm/?petition  </td> <td>Compatible with all PR PK 1.0 to 3.0 included </td>  </tr>

<tr> <td>4</td> <td> Secure Clock V4 <br/>(nicknamed Secure Time) <br/>Set up in 2016 in Microsoft Azure<br/>&nbsp;&nbsp;http://go.microsoft.com/fwlink/?LinkID=746259<br/>&nbsp;&nbsp;https://go.microsoft.com/fwlink/?LinkID=746341  <br/>forwards to:<br/>&nbsp;&nbsp;http://securetime.playready.microsoft.com/SecureTime<br/>&nbsp;&nbsp;https://securetime.playready.microsoft.com/SecureTime  </td> <td> All PR PK 3.2+ (2016) <br/>(REE or TEE) </td>  </tr>
 </table>

{::comment}
&nbsp;

For more information about how SecureTime communicates between the PlayReady client and PlayReady server, see [SecureTime](secure-time.md).
{:/comment}

## Client Owner Services

Final Product Licensees may design their device or application so as to contact a service when they perform PlayReady operations. A very common scenario is the remote provisioning service, which delivers a unique device certificate to a client the first time it performs a PlayReady operation.

These services are specific to the client owner, and use ad-hoc protocols.

Microsoft operates some of these services for the clients that it develops, for example Windows 10 PlayReady, Windows 8.1 PlayReady, Xbox PlayReady, Silverlight, and so on.