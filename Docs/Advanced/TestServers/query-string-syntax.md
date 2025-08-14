---
title: Query String Syntax for PlayReady Test Server
description: Documentation for query string syntax used in PlayReady test server license requests
ms.topic: reference
ms.date: 06/30/2025
---

# Query String Syntax Documentation

Parameters are entered in the query string, separated by commas and brackets. This syntax was introduced in 2017 to fully support PlayReady 3 functionalities:

-   Similar to a JSON syntax (not real JSON though)
-   Easy to read and edit
-   Does not include unsafe characters (like ampersand) and should not require escaping any of them
-   Note: the query string must not include any space characters (' ')
-   Note: '+' characters are acceptable in the base64 encoded arguments
-   Allows to requests for multiple licenses in one license response, and set parameters for each of them.
-   Example: video track encrypted with one key set at SL3000, and audio track encrypted with another key set at SL2000.
-   New date time format yyyymmdd (example: 20171231) and allows set hours, minutes and seconds: yyyymmdd[hhmmss] (example: 20171231235959)

Note: the parameters need to include persist:true if you want to receive persistent licenses.

## Examples

| LAURL (https://test.playready.microsoft.com/service/) | Description |
| --- | --- |
| `rightsmanager.asmx` | Return one non-persistent license with a PLAY right and a Security Level of 150 for the kid found in the WRMHEADER, using the Test Key Seed |
| `rightsmanager.asmx?cfg=(ckt:aescbc)` | NEW IN PLAYREADY 4.0. Return one non-persistent license with a PLAY right for the kid found in the WRMHEADER, with a content key type set for AESCBC encryption (as opposed to AESCTR) |
| `rightsmanager.asmx?cfg=(begindate:20170101,expiration:20170101010000)` | Return one non-persistent license with a PLAY right for the kid found in the WRMHEADER, using the Test Key Seed, with a begin date of January 1st, 2017 0:00, and a fixed expiration of January 1st, 2017 1:00am |
| `rightsmanager.asmx?cfg=(persist:true,begindate:20170101,expiration:20170201,firstexp:60)` | Return one persistent license with fixed begin and end dates, and a relative expiration of 60 seconds after first play. Note: you have to explicitely call out persist:true to receive persistent licenses. |
| `rightsmanager.asmx?cfg=(kid:B6E39626-1CFB-4AA1-BCBD-4EF1ABA7843A,sl:3000),(kid:7C9484BA-C238-467A-869C-CDD8C7167712,sl:2000)` | Return two non-persistent licenses with PLAY rights, one with a Security Level of 3000, one with a Security Level of 2000. Note: these two KIDs must match the KIDs in the WRMHEADER |

## Parameters

| Parameter | Meaning | Values | Comments, Examples, Default Value |
| --- | --- | --- | --- |
| sl | Set the Minimum Security Level for a license | 150, 2000, 3000 | Example: sl:3000<BR/>Default value is 150.<BR/>Note: the video key may be set to sl:3000, but in general, clients only support audio keys to be set to sl:2000 maximum |
| keyseed | Use the key seed provided to generate the content key in the licenses | base64 byte array | Example: keyseed:Wdkg2jsl3djgqSFer26XVBoVVRPzVEggUOSKSQaz<BR/>Default value is the Test Key Seed provided [here](https://web.archive.org/web/20240527193825/https://testweb.playready.microsoft.com/Server/Service) |
| kid | Used in a group of properties to associate these properties to one KID | 'header', or Guid in registry format or base64 string | Example 1: kid:header<BR/>Example 2: kid:e13a7861-d8cc-4284-9245-7c835ebde9f0<BR/>Example 3: kid:YXg64czYhEKSRXyDXr3p8A==<BR/>In the case of kid:header, the license server uses the KID found in the WRMHEADER coming along with the license request. In this case, the WRMHEADER has to include only one KID |
| contentkey | Set the content key | base64 byte array | Example: contentkey:eNqVnXrElmo2NSsn7IXeEA==<BR/>Default value is key(TestKeySeed, kid) |
| ckt | Specifies the Content Key Encryption Type (CTR or CBC) | aesctr , aescbc | Example: ckt:aescbc<BR/>Default value is aesctr<BR/>The license will include a content key set for AESCBC encryption<BR/>NEW IN PLAYREADY 4.0 |
| tid | Set a TransactionId in the license response | guid (arbitrary) | Example: tid:3033E8F0-FB1B-4170-AD5C-60549AAB2C79<BR/>Adds the provided value to the LicenseResponse.TransactionId property, which will require the client to post a license acknowledgement challenge using the specified transaction identifier back to the license server |
|   |  |  |  |
| playright | Add a Play Right | false, true | Example: playright:true<BR/>Default value is true<BR/>Note: a license returned with no right will not allow the client to consume the content |
| readright | Add a Read Right | false, true | Example: readright:true<BR/>Default value is false |
| executeright | Add an Execute Right | false, true | Example: executeright:true<BR/>Default value is false |
| extendedright | Add an Extended Right | Integer. See the example | Example: (extendedright:(type:500,extended:((type:400, mustunderstand:true,besteffort:false,data:Ah==))) |
| persist | Set the License as Persistent or Not | false, true | Example: persist:true<BR/>Default value is false.<BR/>If the license is set non persistent, it is stored on the client in RAM only, in the context of the media player. |
| simple | Use a SimpleNonPersistentLicense | false, true | Example: simple:true<BR/>Default value is false.<BR/>Uses a specific SimpleNonPersistentLicense class to issue the license response. This class was supported in older versions of Silverlight. |
|   |  |  |  |
| begindate | Set a Date and Time before which the license is disabled | yyyymmdd[hhmmss] (GMT) | Example: begindate:20170101<BR/>The license will not allow play back before Jan 1st, 2017 00:00:00 GMT |
| enddate or expiration | Set a Date and Time after which the license is disabled | yyyymmdd[hhmmss] (GMT) | Example 1: enddate:20170131<BR/>Example 2: enddate:20170131235959 - The license will not allow play back after Jan 31st, 2017 23:59:59 GMT |
| firstplayexpiration or firstexp | Set a relative expiration after first play | seconds in integer | Example: firstexp:60<BR/>The license will not allow start a play back exactly 60 seconds after a first playback has been started with that same license. |
| realtime | Add a Real Time expiration restriction | false, true | Example: realtime:true<BR/>Default value is false<BR/>If this property is set, it is required by the client to enforce expirations during a playback session in real time.<BR/>Note: this is only supported by PlayReady 3 clients |
| removaldate | Set a date when the license may be deleted on client (GMT) | yyyymmdd[hhmmss] | Example: removaldate:20170228<BR/>Note that it is optional for clients to remove licenses based on this property. Windows runs this removal process at every license acquisition though.<BR/>See the Server SDK documentation for additional constraints on setting this property. |
|   |  |  |  |
| isroot | Requires the requested license to be a root license with the defined root KID | false, true | Example: cfg=(isroot:true,kid:3C6F3C13-6207-4916-867C-8252B3993638) |
| rootid | Set the root KID for a leaf license | guid | Example: cfg=(rootid:3C6F3C13-6207-4916-867C-8252B3993638,kid:header),(isroot:true,kid:3C6F3C13-6207-4916-867C-8252B3993638) |
|   |  |  |  |
| sourceid | Set the SourceID or Restricted Source ID restriction | int | Example: sourceid:267<BR/>Check the allowed values in the [CRs section 6.12](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance) |
|   |  |  |  |
| caopl | Set a Compressed Digital Audio Output Protection Level restriction | integer | Example: caopl:200<BR/>Default value is 0<BR/>Typically to require Secure Audio Drivers for compressed audio.<BR/>Check the allowed values in the [CRs section 6.7 and 3.6.2](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance)<BR/>Server SDK code:<BR/>`right.CompressedDigitalAudioOPL = 200;` |
| ucaopl | Set an Uncompressed Digital Audio Output Protection Level restriction | integer | Example: ucaopl:300<BR/>Default value is 0<BR/>Typically to require HDCP or DTCP for uncompressed audio.<BR/>Check the allowed values in the [CRs section 6.7 and 3.6.3](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance)<BR/>Server SDK code:<BR/>`right.UncompressedDigitalAudioOPL = 300;` |
| cvopl | Set a Compressed Digital Video Output Protection Level restriction | integer | Example: cvopl:500<BR/>All the allowed values have the same meaning that a PlayReady Product must not Pass the video portion of compressed decrypted Content to any video output.<BR/>Check the allowed values in the [CRs section 6.7 and 3.6.4](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance)<BR/>Server SDK code:<BR/>`right.CompressedDigitalVideoOPL = 500;` |
| ucvopl | Set an Uncompressed Digital Video Output Protection Level restriction | integer | Example: ucvopl:300<BR/>Default value is 0<BR/>Typically to require HDCP on HDMI for uncompressed video.<BR/>Check the allowed values in the [CRs section 6.7 and 3.6.5](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance)<BR/>Server SDK code:<BR/>`right.UncompressedDigitalVideoOPL = 300;` |
| avopl | Set an Analog Video Output Protection Level restriction | integer | Example: avopl:200 to require CGMS-A copy never<BR/>Check the allowed values in the [CRs section 6.7 and 3.6.6](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance)<BR/>Server SDK code:<BR/>`right.AnalogVideoOPL = 200;` |
| dvop | Add an Explicit Digital Video Output Protection | guid and optional data encoded in base 64 string | Example: dvop:(guid:ABB2C6F1-E663-4625-A945-972D17B231E7,data:AAAAAQ==) to require HDCP Type 1.<BR/>See the [CRs section 3.6.5.7](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddDigitalVideoOutputProtection(new Guid("", 1))` |
| daop | Add an Explicit Digital Audio Output Protection | guid and optional data encoded in base 64 string | Example: daop:(guid:6D5CFA59-C250-4426-930E-FAC72C8FCFA6,data:AAAAAQ==) to require SCMS.<BR/>See the [CRs section 3.6.3.8](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddDigitalAudioOutputProtection(new Guid("{6D5CFA59-C250-4426-930E-FAC72C8FCFA6}", 1))` |
| avop | Add an Explicit Analog Video Output Protection | guid and data encoded in base 64 string | Example: avop:(guid:760AE755-682A-41E0-B1B3-DCDF836A7306,data:AAAAAQ==) to<BR/>Check the allowed values in the [CRs section 6.5](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddAnalogVideoOutputProtection(new Guid("{760AE755-682A-41E0-B1B3-DCDF836A7306}", 1)` |
|   |  |  |  |
| extendedrestrictions | Add one or multiple Extended Restrictions to the right | integer and properties, see example | Example: (extendedrestrictions:((type:400, mustunderstand:true,besteffort:false,data:Ah==),(type:401, mustunderstand:true,besteffort:false,data:Ah==)))<BR/>Assumes applicable to the Play right if no other right is set. |
| playenablers | Add one or multiple Play Enablers to the license | guid or group of guids | Example 1: playenablers:(786627D8-C2A6-44BE-8F88-08AE255B01A7) (allow Unknown Outputs).<BR/>Example 2: playenablers:(786627D8-C2A6-44BE-8F88-08AE255B01A7,5ABF0F0D-DC29-4B82-9982-FD8E57525BFC) (allow Unknown Outputs and AirPlay).<BR/>See the [CRs](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance) for all the Play Enablers. |
|   |  |  |  |
|   |  |  |  |
|   |  |  | The parameters below are shorthands for certain combinations of restrictions and play enablers described above |
|   |  |  |  |
| explicitacp | Set an Automatic Gain Control and Color Stripe restriction for Analog Video | integer 0,1,2,3 | Example: explicitacp:2<BR/>Equivalent to: avop(guid:C3FD11C6-F8B7-4D20-B008-1DB17D61F2DA,data:AgAAAA==)<BR/>See the [CRs section 6.5.1 and 3.6.7.2](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddAnalogVideoOutputProtection(new ExplicitOutputProtection(new Guid("C3FD11C6-F8B7-4D20-B008-1DB17D61F2DA"), HeightBytes.Concat(WidthBytes).ToArray()))` |
| maxres | Set a Maximum Effective Resolution Decode Size restriction | integer x integer | Example: maxres:1920x1080<BR/>Equivalent to: dvop:(guid:9645E831-E01D-4FFF-8342-0A720E3E028F,data:AAAEOAAAB4A=)<BR/>See the [CRs section 6.5 and 3.6.5.7.1](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddDigitalVideoOutputProtection(new ExplicitOutputProtection(new Guid("9645E831-E01D-4FFF-8342-0A720E3E028F"), BitConverter.GetBytes((int)value))` |
| allowunknownsd | Add an Output Control for Unknown Output for constrained resolution | false, true | Example: allowunknownsd:true<BR/>Equivalent to: playenablers:(B621D91F-EDCC-4035-8D4B-DC71760D43E9)<BR/>See the [CRs section 3.9.2](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddPlayEnabler(new PlayEnabler(new Guid("B621D91F-EDCC-4035-8D4B-DC71760D43E9")))` |
| allowunknownhd | Add an Output Control for Unknown Output for any resolution | false, true | Example: allowunknownhd:true<BR/>Equivalent to: playenablers:(786627D8-C2A6-44BE-8F88-08AE255B01A7)<BR/>See the [CRs section 3.9.1](https://web.archive.org/web/20240527193825/http://www.microsoft.com/playReady/licensing/compliance).<BR/>Server SDK code:<BR/>`right.AddPlayEnabler(new PlayEnabler(new Guid("786627D8-C2A6-44BE-8F88-08AE255B01A7")))` |
|   |  |  |  |
| clientinfo |  |  | Special reflection feature. See [this page](https://web.archive.org/web/20240527193825/https://testweb.playready.microsoft.com/Doc/TestingClientInfo) for more details. |