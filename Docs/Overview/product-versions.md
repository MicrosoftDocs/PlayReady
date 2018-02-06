---
author: rolandlefranc
title: PlayReady Product Versions
description: Feature availability for each version of the PlayReady products.
ms.assetid: "b1fe306d-2ef3-565a-ae60-cea1592ce0e8"
keywords: PlayReady product versions
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Product Versions

The following table shows the feature availability for each version of the PlayReady products. Click a version number in the table for more details on the specific features available for that release.

&nbsp;
>[!div class="mx-tdBreakAll"]
>|Release date| Version |What's new| PlayReady Server SDK| PlayReady Device Porting Kit| PlayReady Certificate Generation Kit| PlayReady PC SDK for Windows 7 Desktop Apps | PlayReady Client SDK for iOS |PlayReady Client SDK for Android|
>|:--- |:---|:---|:---|:---|:---|:---|:---|:---|
>|Jun'08|**1.0** | Initial version | 1.0.1105| 1.0.1130|1.0.1130|1.1| Not yet available | Not yet available |
>|Oct'08|**1.2** | [Embedded Licenses](embedded-licenses.md) | 1.2.1404 | 1.2.1404|1.2.1404|1.2| &mdash; | &mdash; |
>|May'09|**1.3** | [Specifications section](../Specifications/specifications.md) | &mdash; |&mdash;| &mdash; |1.3| &mdash; | &mdash; |
>|Apr'10|**1.5** | Common Encryption Smooth Streaming | 1.5.4018| &mdash; | 1.5| No further enhancements | &mdash; | &mdash; |
>|Sep'10|**1.5.2** | Security improvements | 1.5.4094| &mdash;| &mdash; | &mdash; | &mdash; | &mdash; |
>|Sep'11|**2.0** | - Live TV with Key Rotation through Scalable Embedded Licenses<br/>- Silverlight Client Verification | 2.0.1402 | 2.0.1402 | 2.0.1402| &mdash; | &mdash; | &mdash; |
>|Apr'12|**2.1** | - Play Enablers for additional policies<br/>- License Template Handler| 2.1.1444| &mdash;| &mdash; | &mdash; | &mdash; | &mdash; |
>|Dec'12|**2.5** | - PlayReady-Network Device (PlayReady-ND)| &mdash; | 2.5.1789 | 2.5.1778| &mdash; | &mdash; | &mdash; |
>|Nov'13|**2.9** | - LicenseTemplateHandlerChaining sample<br/>- Support for iOS and Android| 2.9.1995| &mdash;| &mdash; | &mdash; | 1.0<br/>Initial version | 1.0<br/>Initial version|
>|May'14|**2.11** | - MPEG-DASH<br/>- Updated PlayReady-ND test transmitter<br/>- Updates to PlayReady Client SDK for iOS<br/>- Updates to PlayReady Client SDK for Android| &mdash; | 2.11.2155| &mdash; | &mdash; |2.1 Sep'14 <br/>2.3 Oct'14 <br/>2.4 Aug'15 |  3.0 Dec'14<br/>3.2 Aug'15 |
>|Mar'15|**3.0** | - SL3000<br/>- Multiple Keys<br/>- [Secure Stop](secure-stop-server.md)<br/>- Improvements for non-persistent licenses|3.0|  3.0.4019 | 3.0.2726 | &mdash; | &mdash; | &mdash;  |
>|Sep'16|**3.2** | [Secure Time](trusted-clocks.md) (Secure Clock Service in the TEE)|&mdash;|3.2.4242| 3.2.4242 | Deprecated | No further enhancements | Deprecated |
>|Apr'17|**3.3** | - New CDMi module<br/>- Fix for vulnerabilities in the PK header parser |&mdash;|3.3.4474| 3.3.4475 | &mdash;| &mdash;| &mdash;|
>|Oct'17|**4.0**| - Expanded support for multiple Common Encryption Modes, including CBC1, CBCS, and CENS.<br/>- [Secure Delete](secure-delete-server.md) support | 4.0.5117 | 4.0.5102 | 4.0| No longer distributed (see [PlayReady on Windows](products-and-deliverables.md#prwindows))| &mdash;| No longer distributed|


&nbsp;

## Porting Kit Version Compatibility with Server SDK Versions


The following table lists the compatibility between the various PlayReady Device Porting Kit and PlayReady Server SDK versions:

| &nbsp;| Server SDK v1.5.2| Server SDK v2.1 and Server SDK v2.9| Server SDK v3.0| Server SDK v4.0 |
| --- | --- | --- | --- | --- |
| PK v4.x| No| Yes | Yes | Yes |
| PK v3.x| No| Yes| Yes| Yes |
| PK v2.5 and v2.11| Yes| Yes| Yes| Yes |


&nbsp;

Even though PlayReady v3.X/4.X based clients work against a server running Server SDK v2.1 or v2.9, Microsoft recommends that customers running Server SDK v1.5.2 upgrade to the latest version of the Server SDK instead of upgrading to Server SDK v2.1 or v2.9. This will ensure that you are on a much more supportable path. The latest version available as of January 2018 is Server SDK 4.0


For more information on PlayReady Device Porting Kit and PlayReady Server SDK compatibility and migration considerations, see the *Compatibility and Migration Considerations for PlayReady 3.0/4.0* white paper on the [PlayReady Documents](https://www.microsoft.com/playready/documents/) website.


