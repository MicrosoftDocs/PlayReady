---
title: MP4-based Formats Supported by PlayReady Clients
description: This page describes the MP4-based audio/video formats supported by Windows 10, the Xbox, and other PlayReady Clients
ms.assetid: "7158373B-8E90-4CD0-8CAB-85A23BC60ED7"
keywords: Packaging, PlayReady Packaging, PlayReady Encryption, MP4, mpeg 4, CMAF, Supported, Windows 10, Xbox
ms.date: 06/01/2018
ms.topic: article
---

# MP4-based Formats Supported by PlayReady Clients

## Formats

# [DASH Static Keys](#tab/case1)

#### Format
- MP4 based asset. CMAF preferred.
- DASH manifest.
- Same keys along the asset - Keys not changing over time.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates). For example, a different key can be used for all the video tracks above 1080p to restrict access to the 4K resolution for certain clients.

#### Supported

Supported in version 1507 or higher with the `<mspr:pro>` tag for the Live Profile with static manifests (On-Demand content).

Supported in version 1703 or higher with the `<mspr:pro>` tag for the Live Profile with dynamic manifests (Live content).

The DASH manifest contains a PlayReady Object including a PlayReady Header using the `<mspr:pro>` tag in the `<Period>` node. If different keys are used for different tracks or bitrates, the DASH manifest may have multiple PlayReady Objects in the multiple `<AdaptationSet>` or `<Representation>` nodes instead.

> [!NOTE]
> It is possible to insert the PlayReady Objects inside the init segments of the different `<AdaptationSet>` nodes. If PlayReady Objects are found both in the init segments and in the manifest, the ones in the manifest take precedence.

<br />

DASH manifests with a standard `<cenc:pssh>` tag for On-Demand and Live assets are supported in version RS5 or higher. In this case, the entire content of a pssh box armored in base 64 is included in the manifest. It is not just a PlayReady Object.

For increased compatibility, Microsoft recommends you generate DASH manifests that include the PlayReady Objects duplicated in the `<mspr:pro>` and `<cenc:pssh>` tags.

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD ...>
  <Period>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value=”MSPR 2.0”>
      <cenc:pssh>
        <!--base64-encoded PlayReady ‘pssh’ complete box-->
      </cenc:pssh>
      <mspr:pro>
        <!--base64-encoded PlayReady object -->
      </mspr:pro>
    </ContentProtection>
    <AdaptationSet ...>
      <Representation bandwidth="315108" codecs="avc1.64002A" frameRate="25" height="720" id="video/avc1" scanType="progressive" width="1280">
```

#### Sample

DASH Manifest with a `<mspr:pro>` tag, for a 'cenc' encrypted asset

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" profiles="urn:mpeg:dash:profile:isoff-live:2011" type="static" xmlns:cenc="urn:mpeg:cenc:2013" xmlns:mspr="urn:microsoft:playready" mediaPresentationDuration="PT1H58M29.077S" minBufferTime="PT3S">
    <Period>
        <AdaptationSet id="1" group="1" profiles="ccff" bitstreamSwitching="false" segmentAlignment="true" contentType="video" mimeType="video/mp4" codecs="avc1.640028" maxWidth="1920" maxHeight="1080" startWithSAP="1">
            <ContentProtection schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc" cenc:default_KID="80AA1CD0-A71D-4F86-A939-05FAF9B0CDC5"/>
            <ContentProtection schemeIdUri="urn:uuid:9A04F079-9840-4286-AB92-E65BE0885F95" value="2.0" cenc:default_KID="80AA1CD0-A71D-4F86-A939-05FAF9B0CDC5">
                <mspr:pro>TgMAAAEAAQBEAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AMABCAHkAcQBnAEIAMgBuAGgAawArAHAATwBRAFgANgArAGIARABOAHgAUQA9AD0APAAvAEsASQBEAD4APABDAEgARQBDAEsAUwBVAE0APgBJAEkAdgBrAGEATgBOAGIAMwBtAGMAPQA8AC8AQwBIAEUAQwBLAFMAVQBNAD4APABMAEEAXwBVAFIATAA+AGgAdAB0AHAAcwA6AC8ALwB0AHIAYQBpAG4AcAByAC4AawBlAHkAZABlAGwAaQB2AGUAcgB5AC4AYwBlAG4AdAByAGEAbAB1AHMALgBtAGUAZABpAGEALgBhAHoAdQByAGUALgBuAGUAdAAvAFAAbABhAHkAUgBlAGEAZAB5AC8APAAvAEwAQQBfAFUAUgBMAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADgALgAwAC4AMQA4ADAANQAuADMAMwA8AC8ASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA8AC8AQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwALwBEAEEAVABBAD4APAAvAFcAUgBNAEgARQBBAEQARQBSAD4A</mspr:pro>
            </ContentProtection>
            <SegmentTemplate timescale="10000000" media="QualityLevels($Bandwidth$)/Fragments(video=$Time$,format=mpd-time-csf)" initialization="QualityLevels($Bandwidth$)/Fragments(video=i,format=mpd-time-csf)">
                <SegmentTimeline>
                    <S d="20000000" r="3553"/>
                    <S d="10000000"/>
                </SegmentTimeline>
            </SegmentTemplate>
            <Representation id="1_V_video_1" bandwidth="2984405" width="1920" height="1080"/>
            <Representation id="1_V_video_2" bandwidth="2603504" width="1920" height="1080"/>
```

DASH Manifest with a `<mspr:pro>` and a `<cenc:pssh>` tag

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" profiles="urn:mpeg:dash:profile:isoff-live:2011" type="static" xmlns:cenc="urn:mpeg:cenc:2013" xmlns:mspr="urn:microsoft:playready" mediaPresentationDuration="PT52.208S" minBufferTime="PT3S">
<Period>
  <AdaptationSet id="1" group="1" profiles="ccff" bitstreamSwitching="true" segmentAlignment="true" contentType="video" mimeType="video/mp4" codecs="avc1.640028" maxWidth="1920" maxHeight="1080" startWithSAP="1">
    <ContentProtection schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc" cenc:default_KID="10000000-1000-1000-1000-100000000001"/>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="cenc" cenc:default_KID="10000000-1000-1000-1000-100000000001">
        <cenc:pssh>AAADvnBzc2gAAAAAmgTweZhAQoarkuZb4IhflQAAA56eAwAAAQABAJQDPABXAFIATQBIAEUAQQBEAEUAUgAgAHgAbQBsAG4AcwA9ACIAaAB0AHQAcAA6AC8ALwBzAGMAaABlAG0AYQBzAC4AbQBpAGMAcgBvAHMAbwBmAHQALgBjAG8AbQAvAEQAUgBNAC8AMgAwADAANwAvADAAMwAvAFAAbABhAHkAUgBlAGEAZAB5AEgAZQBhAGQAZQByACIAIAB2AGUAcgBzAGkAbwBuAD0AIgA0AC4AMAAuADAALgAwACIAPgA8AEQAQQBUAEEAPgA8AFAAUgBPAFQARQBDAFQASQBOAEYATwA+ADwASwBFAFkATABFAE4APgAxADYAPAAvAEsARQBZAEwARQBOAD4APABBAEwARwBJAEQAPgBBAEUAUwBDAFQAUgA8AC8AQQBMAEcASQBEAD4APAAvAFAAUgBPAFQARQBDAFQASQBOAEYATwA+ADwASwBJAEQAPgBBAEEAQQBBAEUAQQBBAFEAQQBCAEEAUQBBAEIAQQBBAEEAQQBBAEEAQQBRAD0APQA8AC8ASwBJAEQAPgA8AEMASABFAEMASwBTAFUATQA+ADUAVAB6AEkAWQBRADIAaAByAE8AWQA9ADwALwBDAEgARQBDAEsAUwBVAE0APgA8AEwAQQBfAFUAUgBMAD4AaAB0AHQAcAA6AC8ALwBwAGwAYQB5AHIAZQBhAGQAeQAuAGQAaQByAGUAYwB0AHQAYQBwAHMALgBuAGUAdAAvAHAAcgAvAHMAdgBjAC8AcgBpAGcAaAB0AHMAbQBhAG4AYQBnAGUAcgAuAGEAcwBtAHgAPwBQAGwAYQB5AFIAaQBnAGgAdAA9ADEAJgBhAG0AcAA7AFUAcwBlAFMAaQBtAHAAbABlAE4AbwBuAFAAZQByAHMAaQBzAHQAZQBuAHQATABpAGMAZQBuAHMAZQA9ADEAPAAvAEwAQQBfAFUAUgBMAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADcALgAxAC4AMQA1ADYANQAuADQAPAAvAEkASQBTAF8ARABSAE0AXwBWAEUAUgBTAEkATwBOAD4APAAvAEMAVQBTAFQATwBNAEEAVABUAFIASQBCAFUAVABFAFMAPgA8AC8ARABBAFQAQQA+ADwALwBXAFIATQBIAEUAQQBEAEUAUgA+AA==</cenc:pssh>
    </ContentProtection>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="2.0" cenc:default_KID="10000000-1000-1000-1000-100000000001">
      <mspr:pro>ngMAAAEAAQCUAzwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADAALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsARQBZAEwARQBOAD4AMQA2ADwALwBLAEUAWQBMAEUATgA+ADwAQQBMAEcASQBEAD4AQQBFAFMAQwBUAFIAPAAvAEEATABHAEkARAA+ADwALwBQAFIATwBUAEUAQwBUAEkATgBGAE8APgA8AEsASQBEAD4AQQBBAEEAQQBFAEEAQQBRAEEAQgBBAFEAQQBCAEEAQQBBAEEAQQBBAEEAUQA9AD0APAAvAEsASQBEAD4APABDAEgARQBDAEsAUwBVAE0APgA1AFQAegBJAFkAUQAyAGgAcgBPAFkAPQA8AC8AQwBIAEUAQwBLAFMAVQBNAD4APABMAEEAXwBVAFIATAA+AGgAdAB0AHAAOgAvAC8AcABsAGEAeQByAGUAYQBkAHkALgBkAGkAcgBlAGMAdAB0AGEAcABzAC4AbgBlAHQALwBwAHIALwBzAHYAYwAvAHIAaQBnAGgAdABzAG0AYQBuAGEAZwBlAHIALgBhAHMAbQB4AD8AUABsAGEAeQBSAGkAZwBoAHQAPQAxACYAYQBtAHAAOwBVAHMAZQBTAGkAbQBwAGwAZQBOAG8AbgBQAGUAcgBzAGkAcwB0AGUAbgB0AEwAaQBjAGUAbgBzAGUAPQAxADwALwBMAEEAXwBVAFIATAA+ADwAQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA3AC4AMQAuADEANQA2ADUALgA0ADwALwBJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADwALwBDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APAAvAEQAQQBUAEEAPgA8AC8AVwBSAE0ASABFAEEARABFAFIAPgA=</mspr:pro>
    </ContentProtection>

    <SegmentTemplate timescale="10000000" media="$Bandwidth$/Fragments(video=$Time$,format=mpd-time-csf).mp4" initialization="$Bandwidth$/Fragments(video=i,format=mpd-time-csf)_no_pro.mp4">
      <SegmentTimeline>
        <S d="19999967"/><S d="19999969"/><S d="19999967"/><S d="19999968"/><S d="19999970"/><S d="19999967" r="1"/><S d="19999968" r="1"/><S d="19999969"/><S d="19999967"/><S d="19999968" r="2"/><S d="19999969"/><S d="19999968"/><S d="19999967"/><S d="19999969" r="1"/><S d="19999967" r="1"/><S d="19999970"/><S d="19999968" r="1"/><S d="19999967" r="1"/><S d="1249999"/>
      </SegmentTimeline>
    </SegmentTemplate>

    <Representation id="1_V_video_1" bandwidth="6000000" width="1920" height="1080"/>
```

DASH Manifest with a `<mspr:pro>` tag, for a 'cbcs' encrypted asset

```xml
<?xml version="1.0" encoding="utf-8"?>
<MPD xmlns="urn:mpeg:dash:schema:mpd:2011" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" profiles="urn:mpeg:dash:profile:isoff-live:2011" type="static" xmlns:cenc="urn:mpeg:cenc:2013" xmlns:mspr="urn:microsoft:playready" mediaPresentationDuration="PT10M56.907S" minBufferTime="PT4S">
  <Period>
    <AdaptationSet id="1" group="1" profiles="ccff" bitstreamSwitching="true" segmentAlignment="true" contentType="video" mimeType="video/mp4" codecs="avc1.640028" maxWidth="1920" maxHeight="1080" startWithSAP="1">
        <ContentProtection schemeIdUri="urn:mpeg:dash:mp4protection:2011" value="cenc" cenc:default_KID="10000000-1000-1000-1000-100000000001"/>
        <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="2.0" cenc:default_KID="10000000-1000-1000-1000-100000000001">
            <mspr:pro>uAIAAAEAAQCuAjwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADMALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABMAEEAXwBVAFIATAA+AGgAdAB0AHAAOgAvAC8AZQB4AHAAZQByAGkAbQBlAG4AdABhAGwAMQAuAGEAegB1AHIAZQB3AGUAYgBzAGkAdABlAHMALgBuAGUAdAAvAHIAaQBnAGgAdABzAG0AYQBuAGEAZwBlAHIALgBhAHMAbQB4AD8AYwBmAGcAPQAoAGMAawA6AFcAMwAxAGIAZgBWAHQAOQBXADMAMQBiAGYAVgB0ADkAVwAzADEAYgBmAFEAPQA9ACwAYwBrAHQAOgBBAEUAUwAxADIAOABCAGkAdABDAEIAQwApADwALwBMAEEAXwBVAFIATAA+ADwAUABSAE8AVABFAEMAVABJAE4ARgBPAD4APABLAEkARABTAD4APABLAEkARAAgAEEATABHAEkARAA9ACIAQQBFAFMAQwBCAEMAIgAgAFYAQQBMAFUARQA9ACIAQQBBAEEAQQBFAEEAQQBRAEEAQgBBAFEAQQBCAEEAQQBBAEEAQQBBAEEAUQA9AD0AIgA+ADwALwBLAEkARAA+ADwALwBLAEkARABTAD4APAAvAFAAUgBPAFQARQBDAFQASQBOAEYATwA+ADwALwBEAEEAVABBAD4APAAvAFcAUgBNAEgARQBBAEQARQBSAD4A</mspr:pro>
        </ContentProtection>
        <SegmentTemplate timescale="10000000" media="video/bbb_sunflower_1080p_60fps_normal_VIDEO$Number$.mp4"  initialization="video/bbb_sunflower_1080p_60fps_normal_VIDEO0.mp4">
          <SegmentTimeline>
            <S d="83166700" />
            <S d="79166700" />
            <S d="80333300" />
```

MP4 files

```
[init segment] separate file for a dash stream. Includes only the moov box
  [moov]
    [pssh] pssh box for PlayReady. Includes a PRO including a PRH with KID and LA_URL (optional)
    [pssh] pssh box for other DRM

[any segment]
  [moof] movie fragment header
    [traf] track fragment
      [senc] sample encryption box. Includes Sample Initialization Vectors
  [mdat] movie fragment data
```

#### Test Vectors
See [Test Content on the Test Server](https://test.playready.microsoft.com/Content/Content2X)



# [DASH Changing Keys](#tab/case2)

#### Format
- MP4 based asset.
- DASH manifest.
- Keys changing from time to time over the duration of the asset, by periods.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates).

#### Supported
Constrained Multi Period DASH is supported in version 1803 and higher.

The DASH manifest contains multiple `<Period>` nodes, which are constrained (for example, have all the same characteristics like the number of tracks, and so on). In each of these `<Period>` nodes, there are PlayReady Objects inserted at the `<Period>`, `<AdaptationSet>` or `<Representation>` level as different encryption keys are used.

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
    ...
  </Period>
  <Period>
    <ContentProtection schemeIdUri="urn:uuid:9a04f079-9840-4286-ab92-e65be0885f95" value="2.0" cenc:default_KID="10000000-1000-1000-1000-100000000001">
      <mspr:pro>...</mspr:pro>
    </ContentProtection>
    <AdaptationSet ...>

```

MP4 files

```
[init segment] separate file for a dash stream. Includes only the moov box
  [moov]
    [pssh] pssh box for PlayReady. Includes a PRO including a PRH with KID and LA_URL (optional)
    [pssh] pssh box for other DRM

[any segment]
  [moof] movie fragment header
    [traf] track fragment
      [senc] sample encryption box. Includes Sample Initialization Vectors
  [mdat] movie fragment data
```

#### Test Vectors
See [Test Content on the Test Server](https://test.playready.microsoft.com/Content/Content2X)

# [DASH Rotating Keys](#tab/case3)

#### Format
- MP4 based asset.
- DASH manifest.
- Keys changing from time to time or frequently over the duration of the asset, delivered using PlayReady Embedded Licenses inserted in the stream.
- Same single key for all tracks and representations (bitrates), or different keys for different tracks and representations (bitrates).

#### Supported
DASH with Key Rotation using Embedded Licenses is supported in version 1803 or higher.

The manifest or the init segment includes the special `<DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>` PlayReady Header.

The init segment optionally contains the default KID(s) used in the box Track Encryption box `tenc` (`moov/trak/mdia/minf/stbl/stsd/sinf/schi/tenc`).

Whenever the content key rotates, the MP4 segment contains the new KID(s) used by the segment in the Sample Group Description Box `sgpd` box (`moof/traf/sgpd/seig`). And it also contains in the fragment header `moof/pssh` a PlayReady Leaf License embedded in the content. These PlayReady Leaf Licenses are bound to the PlayReady Root Licenses of the asset.

The application must include logic to proactively request the Root Licenses.

#### Sample

DASH manifest

```xml
<?xml version="1.0" encoding="utf-8"?>
  <SmoothStreamingMedia MajorVersion="2" MinorVersion="2" TimeScale="10000000" IsLive="TRUE" Duration="7200000000" LookAheadFragmentCount="2" DVRWindowLength="7200000000">
  <Protection>
    <ProtectionHeader SystemID="9a04f079-9840-4286-ab92-e65be0885f95">
    8AEAAAEAAQDmATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADEALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADcALgAxAC4AMQA1ADcAMgAuADEAOAA8AC8ASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA8AC8AQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwARABFAEMAUgBZAFAAVABPAFIAUwBFAFQAVQBQAD4ATwBOAEQARQBNAEEATgBEADwALwBEAEUAQwBSAFkAUABUAE8AUgBTAEUAVABVAFAAPgA8AC8ARABBAFQAQQA+ADwALwBXAFIATQBIAEUAQQBEAEUAUgA+AA==</ProtectionHeader>
  </Protection>
  <StreamIndex ...
```

MP4 files

```
[any segment where the key(s) rotate(s)]
  [moof] movie fragment header
    [traf] track fragment
      [sgpd] Sample Group Description box
        [seig] List of the KID(s) for this fragment and beyond
  [mdat] movie fragment data
```

Example of a MP4 segment file when the key rotates

```
  [moof]
    [traf]
      [sgpd] 00 00 00 2C 73 67 70 64 01 00 00 00 73 65 69 67          ...,sgpd....seig
             00 00 00 14 00 00 00 01 00 00 01 08 57 48 35 6D          ............WH5m
             82 C0 40 54 81 BC FD 89 45 2E FF ED                      ..@T....E...
  [mdat]
```


# [HLS Static Keys](#tab/case4)

#### Format
- MP4 based asset. CMAF preferred.
- HLS master playlist (m3u8) and individual playlists (m3u8) for the different tracks and bitrates.
- Same keys along the asset - Keys not changing over time.
- Same single key for all tracks and bitrates, or different keys for different tracks and bitrates.

#### Supported
- 'cbcs' encryption mode, with keys delivered by PlayReady: supported on Xbox One, One S, One X since the update of January 2018
  - Each individual playlist must include a PRO that contains a PRH that contains the KID of the playlist, using the `#EXT-X-KEY:METHOD=SAMPLE-AES` tag.
  - The master playlist must include a PRO that contains a PRH that contains all the KIDs used in all the playlists, using the `#EXT-X-SESSION-KEY:METHOD=SAMPLE-AES` tag. Although this tag is not required by the standard, it is required for Windows 10 and Xbox One/One S/One X to play.

- 'cenc' encryption mode, with keys delivered by PlayReady: supported on Windows 10 and Xbox One, One S, One X in version 1803 or higher.
  - Each individual playlist must include a PRO that contains a PRH that contains the KID of the playlist, using the `#EXT-X-KEY:METHOD=SAMPLE-AES-CTR` tag.
  - The master playlist must include a PRO that contains a PRH that contains all the KIDs used in all the playlists, using the `#EXT-X-SESSION-KEY:METHOD=SAMPLE-AES-CTR` tag. Although this tag is not required by the standard, it is required for Windows 10 and Xbox One/One S/One X to play.

Note: the HLS tag `#EXT-X-PLAYREADYHEADER` is supported in version 1803 and higher for legacy purposes. Microsoft still recommends to use the standard `#EXT-X-KEY` tag in HLS playlists.

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

#### #EXT-X-PLAYREADYHEADER syntax for MP4-based content

Because the non-standard `#EXT-X-PLAYREADYHEADER` tag has been used in HLS playlists to carry the PlayReady Header for some time, Windows 10 and Xbox support this tag in HLS playlists in version 1803 or higher.

#### #EXT-X-PLAYREADYHEADER syntax for MPEG2-TS-based content

Some developers have used the `#EXT-X-PLAYREADYHEADER` tag in HLS playlists since 2010 to develop MPEG2-TS based PlayReady systems before MP4 file based HLS became prevalent. This format is not supported in Windows 10 or Xbox in any version. However, it might be possible to develop a player application that does the playlist and container parsing and can play these assets in a Windows or Xbox app.

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
See [Test Content on the Test Server](https://test.playready.microsoft.com/Content/Content2X)



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
#EXTM3U
#EXT-X-VERSION:4
#EXT-X-KEY:METHOD=SAMPLE-AES,KEYFORMAT="com.microsoft.playready",KEYFORMATVERSIONS="1",URI="data:text/plain;charset=UTF-16;base64,8AEAAAEAAQDmATwAVwBSAE0ASABFAEEARABFAFIAIAB4AG0AbABuAHMAPQAiAGgAdAB0AHAAOgAvAC8AcwBjAGgAZQBtAGEAcwAuAG0AaQBjAHIAbwBzAG8AZgB0AC4AYwBvAG0ALwBEAFIATQAvADIAMAAwADcALwAwADMALwBQAGwAYQB5AFIAZQBhAGQAeQBIAGUAYQBkAGUAcgAiACAAdgBlAHIAcwBpAG8AbgA9ACIANAAuADEALgAwAC4AMAAiAD4APABEAEEAVABBAD4APABDAFUAUwBUAE8ATQBBAFQAVABSAEkAQgBVAFQARQBTAD4APABJAEkAUwBfAEQAUgBNAF8AVgBFAFIAUwBJAE8ATgA+ADcALgAxAC4AMQA1ADcAMgAuADEAOAA8AC8ASQBJAFMAXwBEAFIATQBfAFYARQBSAFMASQBPAE4APgA8AC8AQwBVAFMAVABPAE0AQQBUAFQAUgBJAEIAVQBUAEUAUwA+ADwARABFAEMAUgBZAFAAVABPAFIAUwBFAFQAVQBQAD4ATwBOAEQARQBNAEEATgBEADwALwBEAEUAQwBSAFkAUABUAE8AUgBTAEUAVABVAFAAPgA8AC8ARABBAFQAQQA+ADwALwBXAFIATQBIAEUAQQBEAEUAUgA+AA=="
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

When different keys are used for different tracks (`<StreamIndex>`) or different bitrates (`<QualityLevel>`), the PlayReady Object is still inserted in the top level node of the manifest (`SmoothStreamingMedia`); the PlayReady Object contains a PlayReady Header version 4.2.0.0 minimum, listing multiple KIDs.

> [!NOTE]
> Smooth Streaming assets don't include an init segment like DASH assets.

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
See [Test Content on the Test Server](https://test.playready.microsoft.com/Content/Content2X)

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
  <DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>
</DATA>
</WRMHEADER>
```

PIFF file

```
[any fragment where the key(s) rotate(s)]
  [moof] movie fragment header
    [traf] track fragment
      [sgpd] Sample Group Description box
        [seig] List of the KID(s) for this fragment and beyond
  [mdat] movie fragment data
```

Example of a MP4 fragment header when the key rotates

```
  [moof]
    [traf]
      [sgpd] 00 00 00 2C 73 67 70 64 01 00 00 00 73 65 69 67          ...,sgpd....seig
             00 00 00 14 00 00 00 01 00 00 01 08 57 48 35 6D          ............WH5m
             82 C0 40 54 81 BC FD 89 45 2E FF ED                      ..@T....E...
  [mdat]
```

---

## Quick Media Format Support history for Windows 10 and Xbox One

|Release Date|Version, Build Number and Codename|New features|
| --- | --- | --- | --- | --- |
|July 2015|1507 (v10.0.10240.0) TH1|DASH playback for Live Profile with static manifests using the `<mspr:pro>` tag.<br/>|
|November 2015|1511 (v10.0.1586.0) TH2||
|August 2016|1607 (v10.0.14393.0) RS1||
|April 2017|1703 (v10.0.15063.0) RS2|DASH playback for Live Profile with dynamic manifests.|
|October 2017|1709 (v10.0.16299.0) RS3|HLS playback using the `#EXT-X-KEY` tag for 'cbcs' (only Xbox).|
|April 2018|1803 (v10.0.17134.0) RS4|DASH playback for constrained multi-period content.<br/> HLS playback using the `#EXT-X-KEY` tag for 'cenc'.<br/> HLS playback using the `#EXT-X-PLAYREADYHEADER` tag in m3u8 (for legacy).<br/> Smooth Streaming playback.|
|-|RS5|DASH playback using the `<cenc:pssh>` tag.|

## See also

[PlayReady Test Server Content](https://test.playready.microsoft.com/)

