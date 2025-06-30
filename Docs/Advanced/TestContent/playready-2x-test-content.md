---
title: PlayReady 2.0+ Test Content
description: Test content collection compatible with PlayReady version 2.0 and higher clients, including various media formats and encryption scenarios.
ms.assetid: "D4F2E681-7B94-4A2C-9F85-3E8D1C5A9B4E"
keywords: playready 2.0, test content, media files, encryption, CENC, smooth streaming, DASH
ms.date: 06/30/2025
ms.topic: article
---

# PlayReady 2.0+ Test Content

The content provided on this page is compatible with PlayReady version 2.0 and higher clients: 2.0, 2.5, 2.11, 3.0, 3.2, and higher.

## Important Notes

Some of the test content listed below was created long ago and includes a default LA_URL in their PlayReady Header which no longer exist. We recommend that you use this test content with a specific LA_URL that you set in your client app, instead of relying on the default value.

**Recommended LA_URL for most content:**

```http
LA_URL = http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,sl:150)
```

## Test Content Collection

### Tears of Steel - 4K Content

**Content Details:**

- **Description:** Source: Tears Of Steel (c) Copyright Blender Foundation | mango.blender.org
- **Tool Chain:** Azure Media Services encoder
- **Creation Date:** August 1, 2011
- **Video Encoding:** H264 1080p fragmented
- **Audio Encoding:** AAC
- **Encryption Settings:** CENC AES 128 CTR - Fixed Key
- **Video KID:** `{6f651ae1-dbe4-4434-bcb4-690d1564c41c}`
- **Audio KID:** `{6f651ae1-dbe4-4434-bcb4-690d1564c41c}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0
- **LA URL:** `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,sl:150)`

**Content URLs:**

- **MPEG-DASH (protected):** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k.ism/manifest.mpd`
- **Smooth Streaming (protected):** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k.ism.smoothstreaming/manifest`

### Super Speedway Trailer - Protected Content

**Content Details:**

- **Description:** Source: Super Speedway Trailer. Hosted on IIS (in a VM on Azure)
- **Tool Chain:** Internal process
- **Creation Date:** August 1, 2010
- **Video Encoding:** H264 720p
- **Audio Encoding:** AAC
- **Encryption Settings:** AES 128 CTR
- **Video KID:** `{09E36702-8F33-436C-A5DD-60FFE6671E70}`
- **Audio KID:** `{09E36702-8F33-436C-A5DD-60FFE6671E70}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Smooth Streaming Manifest:** `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720.ism/Manifest`

**Individual Files:**

- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_230.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_331.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_477.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_688.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_991.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_1427.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_2056.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264PR/SuperSpeedway_720_2962.ismv`

### Super Speedway Trailer - Clear Content

**Content Details:**

- **Description:** Source: Super Speedway Trailer. Hosted on IIS (in a VM on Azure)
- **Tool Chain:** Internal process
- **Creation Date:** August 1, 2010
- **Video Encoding:** H264 720p
- **Audio Encoding:** AAC
- **Encryption Settings:** Not encrypted
- **Multi DRM:** False

**Content URLs:**

- **Smooth Streaming Manifest:** `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720.ism/Manifest`

**Individual Files:**

- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_230.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_331.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_477.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_688.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_991.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_1427.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_2056.ismv`
- `http://test.playready.microsoft.com/smoothstreaming/SSWSS720H264/SuperSpeedway_720_2962.ismv`

### Tears of Steel - Live Content with Key Rotation

**Content Details:**

- **Description:** Source: Tears Of Steel. (c) Copyright Blender Foundation | mango.blender.org. Hosted on IIS
- **Tool Chain:** Internal process
- **Creation Date:** March 1, 2011
- **Video Encoding:** H264 720p
- **Audio Encoding:** AAC
- **Encryption Settings:** CENC AES 128 CTR with Key Rotation and Scalable Licenses
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0
- **LA URL:** `https://playready.directtaps.net/svc/live/root/rightsmanager.asmx`

**Content URLs:**

- **Smooth Streaming Manifest:** `http://playready.directtaps.net/media/live/channel01.isml/Manifest`

## Content Categories

### Protected Content

Content encrypted with PlayReady protection:

- **Standard Encryption:** AES 128 CTR mode
- **CENC Encryption:** Common Encryption standard
- **Key Management:** Fixed keys and key rotation scenarios
- **License Requirements:** Requires valid PlayReady license

### Clear Content

Unencrypted reference content:

- **Comparison Testing:** Compare against protected versions
- **Baseline Performance:** Establish performance baselines
- **Troubleshooting:** Isolate encryption-related issues

## Supported Formats

### Smooth Streaming

Microsoft Smooth Streaming format:

- **Manifest Files:** `.ism/Manifest` files
- **Media Segments:** `.ismv` fragmented MP4 files
- **Adaptive Bitrates:** Multiple quality levels
- **Audio/Video Tracks:** Separate or multiplexed

### MPEG-DASH

Dynamic Adaptive Streaming over HTTP:

- **Manifest Files:** `.mpd` files
- **CENC Support:** Common Encryption integration
- **Cross-Platform:** Industry standard format
- **Adaptive Streaming:** Dynamic quality adjustment

## Usage Guidelines

### Testing Scenarios

1. **Basic Playback:** Verify content plays correctly
2. **License Acquisition:** Test license server integration
3. **Adaptive Streaming:** Validate bitrate switching
4. **Error Handling:** Test failure scenarios

### Client Compatibility

- **PlayReady 2.0+:** All content compatible
- **Older Clients:** May have limited feature support
- **Cross-Platform:** Web, mobile, and desktop clients
- **Device Testing:** Various hardware capabilities

### Performance Considerations

- **Network Bandwidth:** Consider delivery requirements
- **Decode Capabilities:** Match content to device specs
- **License Caching:** Optimize license acquisition
- **Startup Time:** Minimize initial buffering

## Troubleshooting

### Common Issues

1. **License Acquisition Failures**

   - Verify LA_URL accessibility
   - Check client PlayReady version
   - Validate server response

2. **Playback Errors**

   - Confirm content URL accessibility
   - Verify encryption compatibility
   - Check device capabilities

3. **Format Support**

   - Validate client format support
   - Check codec availability
   - Verify container compatibility

### Debug Information

- **Content Headers:** Examine PlayReady headers
- **Network Traffic:** Monitor license requests
- **Client Logs:** Review playback events
- **Server Logs:** Check license server responses

## Support Resources

For technical support and additional information:

- **PlayReady Business Queries:** [playready@microsoft.com](mailto:playready@microsoft.com)
- **PlayReady Operations:** Visit [wmlalicensing.com](http://wmlalicensing.com/) or email [ipla@microsoft.com](mailto:ipla@microsoft.com)
- **PlayReady Technical Support:** [Support Options](https://test.playready.microsoft.com/Support/SupportOptions)
- **PlayReady Training Information:** [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## See Also

- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
- [PlayReady Test Server](https://test.playready.microsoft.com/)
