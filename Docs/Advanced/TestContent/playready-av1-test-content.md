---
title: PlayReady AV1 Test Content
description: Test content collection for validating PlayReady with AV1 codec scenarios, supporting both CBC and CTR block cipher modes.
ms.assetid: "E5F6A7B8-C9D0-1234-5678-90ABCDEF1234"
keywords: playready av1, test content, AV1 codec, CBC, CTR, encryption modes
ms.date: 06/30/2025
ms.topic: reference
---

# PlayReady AV1 Test Content

This section contains a collection of test content that can be used to validate PlayReady+AV1 scenarios for both CBC and CTR block cipher modes.

## Test Content Collection

### Big Buck Bunny - AV1 CENC with Audio

**Content Details:**

- **Description:** Big Buck Bunny CENC AV-1 1080p DASH with audio
- **Tool Chain:** FFmpeg and MP4Box
- **Creation Date:** August 1, 2020
- **Video Encoding:** AV-1
- **Audio Encoding:** Not specified
- **Encryption Settings:** Aes128Ctr
- **Video KID:** `{00000000-03fc-eacd-0000-000000000000}`
- **Multi DRM:** True
- **PlayReady WRMHEADER:** 4.3
- **LA URL:** `https://test.playready.microsoft.com/core/rightsmanager.asmx`

**Content URLs:**

- **AV1 DASH Manifest:** `https://test.playready.microsoft.com/media/dash/BBBAV1/manifest.mpd`

### Big Buck Bunny - AV1 CBCS with Audio

**Content Details:**

- **Description:** Big Buck Bunny CBCS AV-1 1080p DASH with audio
- **Tool Chain:** FFmpeg and MP4Box
- **Creation Date:** August 1, 2020
- **Video Encoding:** AV-1
- **Audio Encoding:** Not specified
- **Encryption Settings:** Aes128Cbc
- **Video KID:** `{00000000-03fc-eacd-0000-000000000000}`
- **Multi DRM:** True
- **PlayReady WRMHEADER:** 4.3
- **LA URL:** `https://test.playready.microsoft.com/core/rightsmanager.asmx?cfg=(ckt:AES128BitCBC)`

**Content URLs:**

- **AV1 CBCS DASH Manifest:** `https://test.playready.microsoft.com/media/dash/BBBAV1CBC/manifest.mpd`

## AV1 Codec Overview

### What is AV1?

AV1 (AOMedia Video 1) is a modern, royalty-free video codec developed by the Alliance for Open Media:

- **Open Standard:** Royalty-free and open source
- **High Efficiency:** Superior compression compared to older codecs
- **Wide Adoption:** Supported by major browsers and platforms
- **Future-Proof:** Designed for modern streaming applications

### AV1 with PlayReady

PlayReady support for AV1 enables:

- **Modern Codec Protection:** DRM for next-generation video compression
- **Flexible Encryption:** Support for both CTR and CBC modes
- **Cross-Platform:** Works across devices supporting AV1
- **Standards Compliance:** Follows DASH and CENC specifications

## Encryption Modes

### AES-128-CTR Mode

Counter mode encryption for AV1 content:

- **Mode:** `Aes128Ctr`
- **Characteristics:** Stream cipher mode with counter
- **Performance:** Generally faster encryption/decryption
- **Compatibility:** Widely supported across PlayReady versions

### AES-128-CBC Mode

Cipher Block Chaining mode for AV1 content:

- **Mode:** `Aes128Cbc`
- **Configuration:** `cfg=(ckt:AES128BitCBC)`
- **Characteristics:** Block cipher mode with chaining
- **Security:** Enhanced security through block dependencies
- **Requirements:** PlayReady 4.0+ for CBC support

## Content Delivery

### MPEG-DASH Format

Both AV1 test streams use MPEG-DASH delivery:

- **Adaptive Streaming:** Dynamic quality adjustment
- **Industry Standard:** Cross-platform compatibility
- **Modern Container:** Fragmented MP4 with AV1 tracks
- **Manifest-Driven:** MPD files describe content structure

### Audio Integration

Test content includes audio tracks:

- **Mixed Streams:** Video (AV1) + Audio tracks
- **Synchronized Playback:** Proper A/V synchronization
- **Multi-Track Support:** Separate encryption for audio/video possible

## Tool Chain Information

### FFmpeg

Open-source multimedia framework:

- **AV1 Encoding:** Software-based AV1 compression
- **Format Support:** Multiple container and codec support
- **Encryption:** CENC encryption preparation
- **Cross-Platform:** Available on multiple operating systems

### MP4Box

GPAC multimedia packager:

- **DASH Packaging:** Creates DASH-compliant streams
- **Fragmentation:** Segments content for streaming
- **Encryption Integration:** Applies CENC protection
- **Manifest Generation:** Creates MPD files

## Client Requirements

### AV1 Decoder Support

- **Hardware Acceleration:** Preferred for performance
- **Software Decoding:** Fallback option for older hardware
- **Browser Support:** Modern browsers include AV1 decoders
- **Device Capability:** Check for AV1 decode capability

### PlayReady Version

- **Minimum Version:** PlayReady 4.3 for full AV1 support
- **CBC Support:** PlayReady 4.0+ for CBC encryption mode
- **Modern Features:** Latest features require recent versions

### Platform Support

- **Operating Systems:** Windows, Android, iOS, etc.
- **Browsers:** Chrome, Firefox, Edge, Safari (with support)
- **Devices:** Smart TVs, streaming devices, mobile devices
- **Applications:** Media players with AV1 support

## Testing Scenarios

### Basic AV1 Playback

1. **Decoder Verification:** Confirm AV1 decode capability
2. **Stream Selection:** Verify proper AV1 track selection
3. **Quality Adaptation:** Test adaptive bitrate switching
4. **Performance:** Monitor decode performance and battery usage

### Encryption Mode Testing

1. **CTR Mode Validation:** Test AES-128-CTR encryption
2. **CBC Mode Validation:** Test AES-128-CBC encryption
3. **Mode Comparison:** Compare performance between modes
4. **Compatibility:** Verify mode support across devices

### Multi-DRM Scenarios

1. **Cross-Platform:** Test on different platforms
2. **Interoperability:** Verify with other DRM systems
3. **License Exchange:** Test license acquisition flow
4. **Fallback Handling:** Test when AV1 not supported

## Performance Considerations

### Decode Performance

- **Hardware Acceleration:** Significantly improves performance
- **Software Fallback:** May impact battery life and performance
- **Resolution Impact:** Higher resolutions require more processing
- **Frame Rate:** Higher frame rates increase decode requirements

### Network Efficiency

- **Compression Gains:** AV1 typically 20-30% more efficient than H.264
- **Bandwidth Savings:** Reduced data usage for same quality
- **Startup Time:** May be slightly higher due to complexity
- **Seeking Performance:** Generally good with proper segmentation

## Troubleshooting

### Common Issues

1. **AV1 Not Supported**

   - Check device AV1 decode capability
   - Verify browser AV1 support
   - Test with software decoder if available
   - Consider fallback to H.264/H.265

2. **CBC Mode Issues**

   - Verify PlayReady 4.0+ support
   - Check CBC encryption support
   - Validate license acquisition URL
   - Test with CTR mode for comparison

3. **Performance Problems**

   - Enable hardware acceleration if available
   - Lower resolution/bitrate for testing
   - Monitor CPU and memory usage
   - Consider device capabilities

### Debug Information

- **Codec Support:** Query AV1 decoder availability
- **Encryption Mode:** Verify CTR vs CBC handling
- **Network Analysis:** Monitor manifest and segment requests
- **Decode Statistics:** Track decode performance metrics

## Best Practices

### Content Preparation

- **Multiple Renditions:** Provide various quality levels
- **Fallback Codecs:** Include H.264/H.265 alternatives
- **Proper Packaging:** Use appropriate tools and settings
- **Testing:** Validate across target devices

### Client Implementation

- **Capability Detection:** Check AV1 support before selection
- **Graceful Fallback:** Handle unsupported scenarios
- **Performance Monitoring:** Track decode performance
- **User Experience:** Optimize for target devices

## Support Resources

For technical support and additional information:

- **PlayReady Business Queries:** [playready@microsoft.com](mailto:playready@microsoft.com)
- **PlayReady Operations:** Visit [wmlalicensing.com](http://wmlalicensing.com/) or email [ipla@microsoft.com](mailto:ipla@microsoft.com)
- **PlayReady Technical Support:** [AskDRM@microsoft.com](mailto:AskDRM@microsoft.com)
- **PlayReady Training Information:** [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## See Also

- [PlayReady 4.0+ Test Content](playready-4x-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
- [AV1 Codec Information](https://aomedia.org/av1/)
