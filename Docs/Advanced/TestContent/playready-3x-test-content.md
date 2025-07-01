---
title: PlayReady 3.0+ Test Content
description: Test content collection for validating PlayReady 3.X scenarios, including WRMHEADER v4.2 and content with different keys for audio and video tracks.
ms.assetid: "F8A3B521-9C47-4D2E-B185-7E9F1A5D8C3A"
keywords: playready 3.0, test content, WRMHEADER 4.2, CENC, HEVC, H.264, multi-key content
ms.date: 06/30/2025
ms.topic: reference
---

# PlayReady 3.0+ Test Content

This section contains a collection of test content that can be used to validate some PlayReady 3.X scenarios, for example using the [WRMHEADER v4.2](https://download.microsoft.com/download/2/3/8/238F67D9-1B8B-48D3-AB83-9C00112268B2/PlayReady%20Header%20Object%202015-08-13-FINAL-CL.PDF) and with audio and video tracks protected with different content keys.

## Important Notes

Some of the test content listed below was created long ago and includes a default LA_URL in their PlayReady Header which no longer exist. We recommend that you use this test content with a specific LA_URL that you set in your client app, instead of relying on the default value.

**Recommended LA_URL for most content:**

```http
LA_URL = http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,sl:150)
```

## Test Content Collection

### Tears of Steel - 1080p with Separate Keys

**Content Details:**

- **Description:** H264/AAC CENC with video and audio protected using different keys
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 8-bit depth, 1920x1080, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{a2c786d0-f9ef-4cb3-b333-cd323a4284a5}`
- **Audio KID:** `{db06a8fe-ec16-4de2-9228-2c71e9b856ab}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_1080p_60s_24fps.6000kbps.1920x1080.h264-8b.2ch.128kbps.aac.avsep.cenc.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_1080p_60s_24fps.6000kbps.1920x1080.h264-8b.2ch.128kbps.aac.mp4`

### Tears of Steel - 4K with Separate Keys

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 8-bit depth, 3840x2160, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{72633b87-ceed-4cc3-a5bd-0f6da6cfabc7}`
- **Audio KID:** `{f4adf6ee-9d44-4c54-939e-3237de46c665}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-8b.2ch.128kbps.aac.avsep.cenc.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-8b.2ch.128kbps.aac.mp4`

### H.264 8-bit Video Protected, Audio Clear

**Content Details:**

- **Description:** Video protected, audio clear
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 8-bit depth, 3840x2160, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{38c8e685-2de9-47e7-97d5-6554e5c7f284}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.1

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-8b.2ch.128kbps.aac.audioclear.cenc.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-8b.2ch.128kbps.aac.mp4`

### H.264 10-bit Video Protected, Audio Clear

**Content Details:**

- **Description:** Video protected, audio clear
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 10-bit depth, 3840x2160, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{cbc04456-00a7-4702-99cf-f1d6c9234a7a}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.1

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-10b.2ch.128kbps.aac.audioclear.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h264-10b.2ch.128kbps.aac.mp4`

### HEVC 8-bit Video Protected, Audio Clear

**Content Details:**

- **Description:** Video protected, audio clear
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC 8-bit depth, 3840x2160, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{35d16379-39a3-4cc1-aac9-7200ae23b0e5}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.1

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h265-8b.2ch.128kbps.aac.audioclear.cenc.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h265-8b.2ch.128kbps.aac.mp4`

### HEVC 10-bit Video Protected, Audio Clear

**Content Details:**

- **Description:** Video protected, audio clear
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC 10-bit depth, 3840x2160, 24 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{9c9caf7e-d658-4ea3-886a-6f10a2d2df57}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.1

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h265-10b.2ch.128kbps.aac.audioclear.cenc.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/tearsofsteel_4k_60s_24fps.12000kbps.3840x2160.h265-10b.2ch.128kbps.aac.mp4`

### Big Buck Bunny - HEVC 10-bit High Bitrate

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC 10-bit depth, 3840x2160, 60 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{0bac81d8-073b-400f-8473-854e63696251}`
- **Audio KID:** `{7d31ec61-05ef-400f-838f-f27797ddf707}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-cenc-24mbps.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-frag-24mbps.mp4`

### Big Buck Bunny - HEVC 10-bit Medium Bitrate

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC 10-bit depth, 3840x2160, 60 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{0bac81d8-073b-400f-8473-854e63696251}`
- **Audio KID:** `{7d31ec61-05ef-400f-838f-f27797ddf707}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-cenc-12mbps.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-frag-12mbps.mp4`

### Big Buck Bunny - HEVC 10-bit Low Bitrate

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC 10-bit depth, 3840x2160, 60 fps
- **Audio Encoding:** AAC, 128 kbps 2-channels
- **Video KID:** `{0bac81d8-073b-400f-8473-854e63696251}`
- **Audio KID:** `{7d31ec61-05ef-400f-838f-f27797ddf707}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-cenc-6mbps.mp4`
- **Clear File:** `https://test.playready.microsoft.com/media/profficialsite/bbb-3840x2160-cfg02-frag-6mbps.mp4`

### HEVC Main 3.1 - 720p

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC Main 3.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** AAC, 320 kbps 2-channels
- **Video KID:** `{4f08088c-f8ee-4df5-a793-fe61c3dffd5e}`
- **Audio KID:** `{2b766e79-62c9-4578-85dd-afb8874d2d36}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/ms_media_test.main31.30fps.idr2.0slice.2340kbps.1280x720.h265.2ch.320kbps.aac_dashinit.cenc.separateKeys.42header.mp4`

### HEVC Main 4.0 - 1080p

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC Main 4.0 8-bit depth, 1920x1080, 30 fps
- **Audio Encoding:** AAC, 320 kbps 2-channels
- **Video KID:** `{cad3f790-6007-4a12-acbd-f546a67eb1b7}`
- **Audio KID:** `{c93c4ca1-88c2-4207-943c-09035ef624c9}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/ms_media_test.main40.30fps.idr2.0slice.3834kbps.1920x1080.h265.2ch.320kbps.aac_dashinit.cenc.separateKeys.42header.mp4`

### HEVC Main 5.0 - 4K

**Content Details:**

- **Description:** Video and audio protected using different KIDs
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC Main 5.0 8-bit depth, 3840x2160, 60 fps
- **Audio Encoding:** AAC, 320 kbps 2-channels
- **Video KID:** `{c2c9e030-3973-4dd4-9433-1d015f247bee}`
- **Audio KID:** `{6c28c656-a6a8-4d5a-8a71-b4f6e460b581}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.2

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/ms_media_test.main50.60fps.idr2.0slice.7982kbps.3840x2160.h265.2ch.320kbps.aac_dashinit.cenc.separateKeys.42header.mp4`

### HEVC Video Only - No Audio

**Content Details:**

- **Description:** Video only, No Audio
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** HEVC Main 3.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** No Audio
- **Video KID:** `{09e36702-8f33-436c-a5dd-60ffe6671e70}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/ms_media_test.main31.30fps.idr2.0slice.2340kbps.1280x720.h265.cenc.unaligned.sliceheadersclear.mp4`

## CENC Test Content

### CENC v1 - H.264 with Audio

**Content Details:**

- **Description:** CENC v1
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 High 4.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** AAC, 320 kbps 2-channels
- **Encryption Settings:** ISO/IEC 23001-7: 2011 (CENC v1), Clear NAL headers, 0 minimum bytes clear, aligned (16-byte) encrypted region
- **Video KID:** `{09e36702-8f33-436c-a5dd-60ffe6671e70}`
- **Audio KID:** `{09e36702-8f33-436c-a5dd-60ffe6671e70}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tears_of_steel.60s.high41.30fps.idr2.8slice.8000kbps.1920x1080.h264.2ch.320kbps.aac.cenc.align.0clear.uvu`

### CENC v2 - H.264 with Audio

**Content Details:**

- **Description:** CENC v2
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 High 4.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** AAC, 320 kbps 2-channels
- **Encryption Settings:** ISO/IEC FDIS 23001-7:2014, Second Edition (CENC v2), Clear NAL headers, 0 minimum bytes clear, unaligned, Clear Slice Headers
- **Video KID:** `{e8ad0c7a-8a18-418c-b40e-b3c4660fb62e}`
- **Audio KID:** `{e8ad0c7a-8a18-418c-b40e-b3c4660fb62e}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tears_of_steel.60s.high41.30fps.idr2.8slice.8000kbps.1920x1080.h264.2ch.320kbps.aac.cenc.unaligned.sliceheadersclear.uvu`

### CENC v1 - H.264 Video Only

**Content Details:**

- **Description:** CENC v1
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 High 4.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** No Audio
- **Encryption Settings:** ISO/IEC 23001-7: 2011 (CENC v1), Clear NAL headers, 0 minimum bytes clear, aligned (16-byte) encrypted region
- **Video KID:** `{09e36702-8f33-436c-a5dd-60ffe6671e70}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tears_of_steel.60s.high41.30fps.idr2.8slice.8000kbps.1920x1080.h264.cenc.align.0clear.uvu`

### CENC v2 - H.264 Video Only

**Content Details:**

- **Description:** CENC v2
- **Tool Chain:** Internal process
- **Creation Date:** May 1, 2015
- **Video Encoding:** H.264 High 4.1 8-bit depth, 1280x720, 30 fps
- **Audio Encoding:** No Audio
- **Encryption Settings:** ISO/IEC FDIS 23001-7:2014, Second Edition (CENC v2), Clear NAL headers, 0 minimum bytes clear, unaligned, Clear Slice Headers
- **Video KID:** `{e8ad0c7a-8a18-418c-b40e-b3c4660fb62e}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.0

**Content URLs:**

- **Encrypted File:** `https://test.playready.microsoft.com/media/profficialsite/tears_of_steel.60s.high41.30fps.idr2.8slice.8000kbps.1920x1080.h264.cenc.unaligned.sliceheadersclear.uvu`

## Content Features

### Multi-Key Content

PlayReady 3.0+ introduces support for content with separate keys for audio and video tracks:

- **WRMHEADER 4.2:** Supports multiple Key IDs in a single header
- **Separate Encryption:** Video and audio can have different protection levels
- **Advanced Scenarios:** Enables sophisticated rights management

### Video Codec Support

- **H.264:** 8-bit and 10-bit depth encoding
- **HEVC (H.265):** Various profiles including Main 3.1, 4.0, and 5.0
- **Resolution Range:** From 720p to 4K (3840x2160)
- **Frame Rates:** 24 fps, 30 fps, and 60 fps content

### Encryption Standards

- **CENC v1:** ISO/IEC 23001-7: 2011 standard
- **CENC v2:** ISO/IEC FDIS 23001-7:2014 Second Edition
- **Alignment Options:** Aligned and unaligned encryption
- **Clear Headers:** NAL and slice header handling

## Usage Guidelines

### Testing Scenarios

1. **Multi-Key Validation:** Test separate audio/video key handling
2. **HEVC Compatibility:** Verify modern codec support
3. **High Resolution:** Test 4K and high bitrate content
4. **CENC Compliance:** Validate encryption standard support

### Client Requirements

- **PlayReady 3.0+:** Required for multi-key content
- **HEVC Support:** Hardware/software decoder capability
- **High Resolution:** 4K display and decode capabilities
- **CENC v2:** Updated encryption standard support

## Support Resources

For technical support and additional information:

- **PlayReady Business Queries:** [playready@microsoft.com](mailto:playready@microsoft.com)
- **PlayReady Operations:** Visit [wmlalicensing.com](http://wmlalicensing.com/) or email [ipla@microsoft.com](mailto:ipla@microsoft.com)
- **PlayReady Technical Support:** [AskDRM@microsoft.com](mailto:AskDRM@microsoft.com)
- **PlayReady Training Information:** [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## See Also

- [PlayReady 2.0+ Test Content](playready-2x-test-content.md)
- [PlayReady 4.0+ Test Content](playready-4x-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
