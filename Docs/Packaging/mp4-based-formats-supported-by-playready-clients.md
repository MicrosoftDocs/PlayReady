---
author: rolandlefranc
title: MP4-based Formats Supported by PlayReady Clients
description: This page describes the MP4-based audio/video formats supported by Windows 10, the Xbox, and other PlayReady Clients
ms.assetid: "7158373B-8E90-4CD0-8CAB-85A23BC60ED7"
keywords: Packaging, PlayReady Packaging, PlayReady Encryption, MP4, mpeg 4, CMAF, Supported, Windows 10, Xbox
ms.author: rolefran
ms.date: 06/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# MP4-based Formats Supported by PlayReady Clients

## Formats

# [DASH Static Keys](#tab/case1)

#### Format
- MP4 based asset. CMAF preferred.
- DASH manifest.
- Same keys along the asset - Keys not changing over time.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates). For example, use a different key can be used for all the video tracks above 1080p, to restrict access to the 4K resolution to certain clients.

#### Supported

The DASH manifest contains a PRO in each AdaptationSet, or in the DASH init segment of each representation

- Supported on Windows 10 Fall Creators Update (released October 2017) and above


#### Sample

DASH Manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD ...>
  <Period>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="2.0" cenc:default_KID="10000000-1000-1000-1000-100000000001">
      <mspr:pro>...</mspr:pro>
    </ContentProtection>
    <AdaptationSet ...>
      <Representation bandwidth="315108" codecs="avc1.64002A" frameRate="25" height="720" id="video/avc1" scanType="progressive" width="1280">
        <SegmentList duration="4000" timescale="1000">
          <Initialization sourceURL="video/avc1/init.mp4"/>
          <SegmentURL media="video/avc1/seg-1.mp4"/>
```

MP4 files

```
[init segment] separate file for a dash stream. Includes only the moov box
  [moov] 
    [pssh] pssh box for PlayReady. Includes a PRO including a PRH with KID and LA_URL
    [pssh] pssh box for other DRM

[any segment]
  [moof] movie fragment header
    [traf] track fragment
      [senc] sample encryption box. Includes Sample Initialization Vectors
  [mdat] movie fragment data
```

#### Test Vectors
See [Test Content on the Test Server](http://test.playready.microsoft.com/Content/Content2X)



# [DASH Changing Keys](#tab/case2)

#### Format
- MP4 based asset.
- DASH manifest.
- Keys changing from time to time over the duration of the asset, by periods.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates).

#### Supported
- Supported on Windows 10 Fall Creators Update (released October 2017) and above
- PlayReady Header in the manifest at the AdaptationSet level, or in the DASH init segment. The single PlayReady Header contains a list of all the KIDs used for all the tracks and representations of the stream.

#### Sample

DASH Manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD ...>
  <Period>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="2.0" cenc:default_KID="10000000-1000-1000-1000-100000000001">
      <mspr:pro>...</mspr:pro>
    </ContentProtection>
    <AdaptationSet ...>
      <Representation bandwidth="315108" codecs="avc1.64002A" frameRate="25" height="720" id="video/avc1" scanType="progressive" width="1280">
        <SegmentList duration="4000" timescale="1000">
          <Initialization sourceURL="video/avc1/init.mp4"/>
          <SegmentURL media="video/avc1/seg-1.mp4"/>
```

MP4 files

```
[init segment] separate file for a dash stream. Includes only the moov box
  [moov] 
    [pssh] pssh box for PlayReady. Includes a PRO including a PRH with KID and LA_URL
    [pssh] pssh box for other DRM

[any segment]
  [moof] movie fragment header
    [traf] track fragment
      [senc] sample encryption box. Includes Sample Initialization Vectors
  [mdat] movie fragment data
```

#### Test Vectors
See [Test Content on the Test Server](http://test.playready.microsoft.com/Content/Content2X)

# [DASH Rotating Keys](#tab/case3)

#### Format
- MP4 based asset.
- DASH manifest.
- Keys changing from time to time or frequently over the duration of the asset, delivered using PlayReady Embedded Licenses inserted in the stream.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates).

#### Supported

...


#### Sample

```xml
<?xml version="1.0" encoding="utf-8"?>
  <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" TimeScale="10000000" IsLive="TRUE" Duration="7200000000" LookAheadFragmentCount="2" DVRWindowLength="7200000000">
  <Protection>
    <ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">
    8AEAAAEAAQDmATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADEALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADcALgAxAC4AMQA1ADcAMgAuADEAOAA8AC8ASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA8AC8AQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwARABFAEMAUgBZAFAAVABPAFIAUwBFAFQAVQBQAD4ATwBOAEQARQBNAEEATgBEADwALwBEAEUAQwBSAFkAUABUAE8AUgBTAEUAVABVAFAAPgA8AC8ARABBAFQAQQA+ADwALwBXAFIATQBIAEUAQQBEAEUAUgA+AA==</ProtectionHeader>
  </Protection>
  <StreamIndex ...
```



# [HLS Static Keys](#tab/case4)

#### Format
- MP4 based asset. CMAF preferred.
- HLS master playlist (m3u8) and individual playlists (m3u8) for the different tracks and bitrates.
- Same keys along the asset - Keys not changing over time.
- Same single key for all tracks and bitrates, or different keys for different tracks and bitrates.

#### Supported
- 'cbcs' encryption mode, with keys delivered by PlayReady: supported on the Xbox One, One S, One X since the update of January 2018
  - Each individual playlist must include a PRO that contains a PRH that contains the KID of the playlist, using the `EXT-X-KEY:METHOD=SAMPLE-AES` tag.
  - The master playlist must include a PRO that contains a PRH that contains all the KIDs used in all the playlists, using the `EXT-X-SESSION-KEY:METHOD=SAMPLE-AES` tag. Although this tag is not required by the standard, it is required for Windows 10 and the Xbox One/One S/One X to play.

- 'cenc' encryption mode, with keys delivered by PlayReady: supported on Windows 10 and the Xbox One, One S, One X since the update of April 2018 ("April 2018 Update")
  - Each individual playlist must include a PRO that contains a PRH that contains the KID of the playlist, using the `EXT-X-KEY:METHOD=SAMPLE-AES-CTR` tag.
  - The master playlist must include a PRO that contains a PRH that contains all the KIDs used in all the playlists, using the `EXT-X-SESSION-KEY:METHOD=SAMPLE-AES-CTR` tag. Although this tag is not required by the standard, it is required for Windows 10 and the Xbox One/One S/One X to play.

Note: the HLS tag `EXT-X-PLAYREADYHEADER` is supported in version 1803 and higher for legacy purposes. Microsoft still recommends to use the standard `EXT-X-KEY` tag in HLS playlists.

#### Sample

Master playlist

```M
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-SESSION-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="
```

Individual playlist
```M
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="
```

#### EXT-X-PLAYREADYHEADER syntax for MP4-based content

Because the non-standard `EXT-X-PLAYREADYHEADER` tag has been used in HLS playlists to carry the PlayReady Header for some time, Windows 10 and the Xbox support this tag in HLS playlists in version 1803 or higher.

#### EXT-X-PLAYREADYHEADER syntax for MPEG2-TS-based content

Some developers have used the `EXT-X-PLAYREADYHEADER` tag in HLS playlists since 2010 to develop MPEG2-TS based PlayReady systems before MP4 file based HLS became prevalent. This format is not supported in Windows 10 or the Xbox in any version. It might be possible though to develop a player application that does the playlist and container parsing and can play these assets in a Windows or Xbox app.

```M
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-PLAYREADYHEADER:XAMAAAEAAQBSAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4ANABSAHAAbABiACsAVABiAE4ARQBTADgAdABHAGsATgBGAFcAVABFAEgAQQA9AD0APAAvAEsASQBEAD4APABDAEgARQBDAEsAUwBVAE0APgBLAEwAagAzAFEAegBRAFAALwBOAEEAPQA8AC8AQwBIAEUAQwBLAFMAVQBNAD4APABMAEEAXwBVAFIATAA+AGgAdAB0AHAAcwA6AC8ALwBwAHIAbwBmAGYAaQBjAGkAYQBsAHMAaQB0AGUALgBrAGUAeQBkAGUAbABpAHYAZQByAHkALgBtAGUAZABpAGEAcwBlAHIAdgBpAGMAZQBzAC4AdwBpAG4AZABvAHcAcwAuAG4AZQB0AC8AUABsAGEAeQBSAGUAYQBkAHkALwA8AC8ATABBAF8AVQBSAEwAPgA8AEMAVQBTAFQATwBNAEEAVABUAFIASQBCAFUAVABFAFMAPgA8AEkASQBTAF8ARABSAE0AXwBWAEUAUgBTAEkATwBOAD4AOAAuADAALgAxADcAMQAzAC4AMQAzADwALwBJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADwALwBDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=
#EXT-X-MEDIA:TYPE=AUDIO,GROUP-ID="audio",NAME="aac_UND_2_128",DEFAULT=YES,URI="QualityLevels(128003)/Manifest(aac_UND_2_128,format=m3u8-aapl)"
#EXT-X-STREAM-INF:BANDWIDTH=1138489,RESOLUTION=640x288,CODECS="avc1.640015,mp4a.40.2",AUDIO="audio"
QualityLevels(970010)/Manifest(video,format=m3u8-aapl)
#EXT-X-I-FRAME-STREAM-INF:BANDWIDTH=1138489,RESOLUTION=640x288,CODECS="avc1.640015",URI="QualityLevels(970010)/Manifest(video,format=m3u8-aapl,type=keyframes)"
#EXT-X-STREAM-INF:BANDWIDTH=2376263,RESOLUTION=960x428,CODECS="avc1.64001e,mp4a.40.2",AUDIO="audio"
QualityLevels(2181139)/Manifest(video,format=m3u8-aapl)
#EXT-X-I-FRAME-STREAM-INF:BANDWIDTH=2376263,RESOLUTION=960x428,CODECS="avc1.64001e",URI="QualityLevels(2181139)/Manifest(video,format=m3u8-aapl,type=keyframes)"
#EXT-X-STREAM-INF:BANDWIDTH=3513624,RESOLUTION=1280x572,CODECS="avc1.64001f,mp4a.40.2",AUDIO="audio"
QualityLevels(128003)/Manifest(aac_UND_2_128,format=m3u8-aapl)
```

#### Test Vectors
See [Test Content on the Test Server](http://test.playready.microsoft.com/Content/Content2X)



# [HLS Changing Keys](#tab/case5)

#### Format
- MP4 based asset. CMAF preferred.
- HLS master playlist (m3u8) and individual playlists (m3u8) for the different tracks and bitrates.
- Keys changing from time to time over the duration of the asset, by periods.
- Same single key for all tracks and bitrates, or different keys for different tracks and bitrates.

#### Supported

**On-Demand:** HLS assets with keys changing from time to time is supported for On-Demand content as HLS Static Keys. The master playlist and the individual playlists must contain `#EXT-X-SESSION-KEY` and `#EXT-X-KEY` tags.
The indivual playlists contain one `#EXT-X-KEY` tag every time the encryption keys change.

**Live:** HLS assets with keys changing is not supported for Live content where the encryption keys are not *all* present in the playlists when playback starts. It is possible to build an application that supports it though. The application has logic to sniff the playlists while they're refreshed, and to request the licenses for the encryption keys needed after rotation.


#### Sample

Master playlist

```M
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-SESSION-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="
```

Individual playlist
```M
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="

#EXT-X-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="

#EXT-X-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,xAEAAAEAAQC6ATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AdgBHAFYAagBOAEsAZwBZAE0ARQBxAHAATwBMAGgAMQBWAGQAUgBUADAAQQA9AD0APAAvAEsASQBEAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA="
```



# [HLS Rotating Keys](#tab/case6)

#### Format
- MP4 based asset. CMAF preferred.
- HLS master playlist (m3u8) and individual playlists (m3u8) for the different tracks and bitrates.
- Keys changing from time to time or frequently over the duration of the asset, delivered using PlayReady Embedded Licenses inserted in the stream.
- Same single key for all tracks and bitrates, or different keys for different tracks and bitrates.

#### Supported

HLS assets with rotating keys using Embedded Licenses is supported for On-Demand and Live content in version 1803 and higher.

The master playlist and the individual playlists contain `#EXT-X-SESSION-KEY` and `#EXT-X-KEY` tags, which include the special `<DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>` PlayReady Header.

The MP4 segments contain in the fragment header `moof/uuid/pssh` a PlayReady Leaf License embedded in the content, whenever the content key rotates. These PlayReady Leaf Licenses are bound to the PlayReady Root Licenses of the asset.

The application must include logic to proactively request the Root Licenses.

#### Sample

```M
TBD 
```

PlayReady Header in the master playlist and the individual playlists:

```xml
<WRMHEADER version="4.2.0.0" xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader">
  <DATA>
    <DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>
  </DATA>
</WRMHEADER>
```

# [Smooth Static Keys](#tab/case7)

#### Format
- MP4 based asset. PIFF format.
- Smooth Streaming manifest.
- Same keys along the asset - Keys not changing over time.
- Same single key for all tracks (`<StreamIndex>`)and bitrates  (`<QualityLevel>`), or different keys for the different tracks (`<StreamIndex>`) and the different bitrates (`<QualityLevel>`).

#### Supported
Smooth Streaming with PlayReady playback is supported in version 1803 and higher. In earlier versions, it is possible to build an application that plays them, by parsing the manifest and the segments programmatically. SDKs like the [Smooth Streaming SDK](https://marketplace.visualstudio.com/items?itemName=Cenkd.MicrosoftUniversalSmoothStreamingClientSDK), or the [HASplayer](https://github.com/Orange-OpenSource/hasplayer.js/wiki) can be used to implement this parsing and logic.

A PlayReady Object containing all the KIDs used for the entire asset is inserted in the manifest in the top level node (`<SmoothStreamingMedia>`) using this syntax:
`<Protection><ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">...</ProtectionHeader><Protection>`

When different keys are used for the different tracks (`<StreamIndex>`) or the different bitrates (`<QualityLevel>`), the PlayReady Object is still inserted in the top level node of the manifest (`SmoothStreamingMedia`); the PlayReady Object contains a PlayReady Header version 4.2.0.0 minimum, listing multiple KIDs.

Note: Smooth Streaming assets don't include an init segment like DASH assets.

#### Sample

Smooth Streaming manifest

```xml
<?xml version="1.0" encoding="UTF-8"?>
<SmoothStreamingMedia MajorVersion="2" MinorVersion="1" Duration="1209510000">
  <StreamIndex Chunks="61" DisplayWidth="1280" Type="video" MaxWidth="1280" Url="QualityLevels({bitrate})/Fragments(video={start time})" MaxHeight="720" QualityLevels="8" Name="video" DisplayHeight="720">
    <QualityLevel Index="1" Bitrate="331000" FourCC="H264" MaxWidth="284" MaxHeight="160" />
    <QualityLevel Index="2" Bitrate="230000" FourCC="H264" MaxWidth="224" MaxHeight="128" />
    <c d="20020000" />
    <c d="20020000" />
    <c d="20020000" />
  </StreamIndex>
  <StreamIndex Chunks="61" Index="0" Type="audio" Url="QualityLevels({bitrate})/Fragments(audio={start time})" QualityLevels="1" Name="audio">
    <QualityLevel AudioTag="255" BitsPerSample="16" Bitrate="128000" FourCC="AACL" CodecPrivateData="1210" Channels="2" PacketSize="4" SamplingRate="44100" />
    <c d="20201360" />
    <c d="19969161" />
    <c d="19969161" />
  </StreamIndex>
  <Protection>
    <ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">XAMAAAEAAQBSAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4ANABSAHAAbABiACsAVABiAE4ARQBTADgAdABHAGsATgBGAFcAVABFAEgAQQA9AD0APAAvAEsASQBEAD4APABDAEgARQBDAEsAUwBVAE0APgBLAEwAagAzAFEAegBRAFAALwBOAEEAPQA8AC8AQwBIAEUAQwBLAFMAVQBNAD4APABMAEEAXwBVAFIATAA+AGgAdAB0AHAAcwA6AC8ALwBwAHIAbwBmAGYAaQBjAGkAYQBsAHMAaQB0AGUALgBrAGUAeQBkAGUAbABpAHYAZQByAHkALgBtAGUAZABpAGEAcwBlAHIAdgBpAGMAZQBzAC4AdwBpAG4AZABvAHcAcwAuAG4AZQB0AC8AUABsAGEAeQBSAGUAYQBkAHkALwA8AC8ATABBAF8AVQBSAEwAPgA8AEMAVQBTAFQATwBNAEEAVABUAFIASQBCAFUAVABFAFMAPgA8AEkASQBTAF8ARABSAE0AXwBWAEUAUgBTAEkATwBOAD4AOAAuADAALgAxADgAMAA1AC4AMwAzADwALwBJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADwALwBDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=</ProtectionHeader>
  </Protection>
</SmoothStreamingMedia>
```

### Asset Files

```
[representation] MP4 file for each track or bitrate
  [moof] movie fragment header
    [traf] track fragment
      [uuid]
        [senc] sample encryption box. Includes Sample Initialization Vectors
  [mdat] movie fragment data
```
#### Test Vectors
See [Test Content on the Test Server](http://test.playready.microsoft.com/Content/Content2X)

# [Smooth Rotating Keys](#tab/case9)

#### Format
- MP4 based asset. PIFF format.
- Smooth Streaming manifest.
- Keys changing from time to time or frequently over the duration of the asset, delivered using PlayReady Leaf Licenses embedded in the stream, bound to PlayReady Root Licenses.
- Same single key for all tracks (`<StreamIndex>`)and bitrates  (`<QualityLevel>`), or different keys for the different tracks (`<StreamIndex>`) and the different bitrates (`<QualityLevel>`).

#### Supported
Smooth Streaming with PlayReady playback with Embedded Licenses is supported in version 1803 and higher.

The manifest includes the special `<DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>` PlayReady Header, using this syntax: `<Protection><ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">...</ProtectionHeader><Protection>`.

The MP4 files include Embedded Licenses included in `pssh` boxes. The application must implement the logic to proactively acquire the PlayReady Root Licenses needed for the Embedded Leaf Licenses.

#### Sample

Here is the Smooth Streaming Manifest extracted from the test stream `http://playready.directtaps.net/media/live/channel01.isml/Manifest`

```xml
<?xml version="1.0" encoding="utf-8"?>
  <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" TimeScale="10000000" IsLive="TRUE" Duration="7200000000" LookAheadFragmentCount="2" DVRWindowLength="7200000000">
  <Protection>
    <ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">
    8AEAAAEAAQDmATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADEALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADcALgAxAC4AMQA1ADcAMgAuADEAOAA8AC8ASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA8AC8AQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwARABFAEMAUgBZAFAAVABPAFIAUwBFAFQAVQBQAD4ATwBOAEQARQBNAEEATgBEADwALwBEAEUAQwBSAFkAUABUAE8AUgBTAEUAVABVAFAAPgA8AC8ARABBAFQAQQA+ADwALwBXAFIATQBIAEUAQQBEAEUAUgA+AA==</ProtectionHeader>
  </Protection>
  <StreamIndex ...
```

The manifest includes the PlayReady Header:
```xml
<WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.1.0.0">
<DATA>
  <CUSTOMATTRIBUTES>
    <IIS_DRM_VERSION>7.1.1572.18</IIS_DRM_VERSION>
  </CUSTOMATTRIBUTES>
  <DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>
</DATA>
</WRMHEADER>
```
---

## Quick Media Support history for Windows 10 and the Xbox One, One S, One X

|Release Date|Version, Build Number and Codename|New features|
| --- | --- | --- | --- | --- |
|July 2015|1507 (v10.0.10240.0) TH1|DASH playback for On-Demand content using the `<mspr:pro>` tag.<br/>|
|November 2015|1511 (v10.0.1586.0) TH2||
|August 2016|1607 (v10.0.14393.0) RS1|DASH playback for Live content with refreshed manifests.|
|April 2017|1703 (v10.0.15063.0) RS2||
|October 2017|1709 (v10.0.16299.0) RS3|HLS playback using the `EXT-X-KEY` tag for 'cbcs' (only Xbox).|
|April 2018|1803 (v10.0.17134.0) RS4|DASH playback for constrained multi-period content.<br/> HLS playback using the `EXT-X-KEY` tag for 'cenc'.<br/> HLS playback using the `EXT-X-PLAYREADYHEADER` tag in m3u8 (for legacy).<br/> Smooth Streaming playback.|
|-|RS5|DASH playback using the `<cenc:pssh>` tag.|

## See also

[PlayReady Test Server Content](http://test.playready.microsoft.com/)

