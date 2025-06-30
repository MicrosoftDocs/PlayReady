---
title: PlayReady 4.0+ Test Content
description: Test content collection for validating PlayReady 4.X scenarios, including CBCS encryption and advanced modern features.
ms.assetid: "A1B2C3D4-5E6F-7890-ABCD-EF1234567890"
keywords: playready 4.0, test content, CBCS, CENC CTR, VP9, AV1, modern encryption
ms.date: 06/30/2025
ms.topic: reference
---

This section contains a collection of test content that can be used to validate some PlayReady 4.X scenarios, for example using CBCS encryption.

## Important Notes

Some of the test content listed below was created long ago and includes a default LA_URL in their PlayReady Header which no longer exist. We recommend that you use this test content with a specific LA_URL that you set in your client app, instead of relying on the default value.

**Recommended LA_URL for most content:**

```http
LA_URL = http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,sl:150)
```

## Test Content Collection

### Big Buck Bunny - H.264/AAC CENC CBCS

**Content Details:**

- **Description:** H264/AAC CENC CBCS with video and audio protected
- **Tool Chain:** Apple toolset - 16-byte IV (128-bit Initialization Vector)
- **Creation Date:** September 1, 2017
- **Video Encoding:** H.264
- **Audio Encoding:** AAC 2-channels
- **Encryption Settings:** CENC CBCS with 16-byte IV
  - **KID:** `AAAAEAAQABAQABAAAAAAAQ==`
  - **Content Key:** `W31bfVt9W31bfVt9W31bfQ==`
  - **Video Track:** Encrypted with CBCS 1:9 pattern
  - **Audio Track:** Fully encrypted (crypt_byte_block = skip_byte_block = 0)
- **Video KID:** `{10000000-1000-1000-1000-100000000001}`
- **Audio KID:** `{10000000-1000-1000-1000-100000000001}`
- **Multi DRM:** False
- **PlayReady WRMHEADER:** 4.3
- **LA URL:** `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,ck:W31bfVt9W31bfVt9W31bfQ==,ckt:aescbc)`

**Content URLs:**

- **MP4 CENC CBCS (clear):** `https://test.playready.microsoft.com/media/dash/APPLEENC_CBCS_BBB_1080p/clear/bbb_sunflower_1080p_60fps_normal.mp4`
- **MPEG-DASH (protected):** `https://test.playready.microsoft.com/media/dash/APPLEENC_CBCS_BBB_1080p/1080p.mpd`
- **HLS (protected):** `https://test.playready.microsoft.com/media/dash/APPLEENC_CBCS_BBB_1080p/1080p_alternate.m3u8`

**Technical Notes:**

The Apple toolset contains a bug that sets the KID value in the `moov.trak.mdia.minf.stbl.stsd.encv.sinf.tenc` box to 0, where it should be equal to the value set in the manifest according to the DASH CENC specification.

### VP9 - Tears of Steel CENC CTR

**Content Details:**

- **Description:** Fragmented MP4 file with a VP9 video track encrypted with CENC (CTR mode)
- **Tool Chain:** Not specified
- **Creation Date:** October 1, 2017
- **Video Encoding:** VP9
- **Audio Encoding:** None
- **Encryption Settings:** CENC CTR
- **Video KID:** `{00000000-03fc-eacd-0000-000000000000}`
- **Multi DRM:** True
- **PlayReady WRMHEADER:** 4.0
- **LA URL:** `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(contentkey:MeXKilhhoLl25CHFTGEDRg==,kid:00000000-03FC-EACD-0000-000000000000)`

**Content URLs:**

- **MP4 CENC CTR (protected):** `https://test.playready.microsoft.com/media/vp9/VP9_TearsOfSteel_12min_543_repackaged_20170523.mp4.ismv`

## Key Features

### CBCS Encryption

PlayReady 4.0 introduces support for CBC (Cipher Block Chaining) encryption mode:

- **Pattern Encryption:** Supports subsample encryption patterns (e.g., 1:9 pattern)
- **Enhanced Security:** CBC mode provides additional security features
- **Apple Compatibility:** Works with Apple's encryption toolchain
- **16-byte IV:** Uses 128-bit Initialization Vectors

### AESCBC Content Key Type

New in PlayReady 4.0:

- **Content Key Type:** `aescbc` parameter in license acquisition
- **Enhanced Encryption:** AES-CBC mode instead of AES-CTR
- **Backward Compatibility:** Maintains compatibility with existing content

### VP9 Codec Support

PlayReady 4.0 extends codec support:

- **VP9 Video:** Modern video codec support
- **Multi-DRM:** Cross-platform DRM compatibility
- **Fragmented MP4:** Modern container format support

## Content Formats

### MPEG-DASH

- **Modern Standard:** Industry-standard adaptive streaming
- **CBCS Support:** Common Encryption with CBC mode
- **Cross-Platform:** Works across multiple devices and platforms

### HLS (HTTP Live Streaming)

- **Apple Standard:** Native support for Apple devices
- **CBCS Integration:** Works with Apple's encryption toolchain
- **Alternative Renditions:** Multiple quality levels

### Fragmented MP4

- **Modern Container:** Optimized for streaming
- **VP9 Support:** Advanced video codec compatibility
- **Efficient Delivery:** Reduced latency and improved performance

## Encryption Specifications

### CENC CBCS Details

According to ISO/IEC 23001-7:2015(E):

- **Video Pattern:** 1:9 encryption pattern (1 encrypted block, 9 clear blocks)
- **Audio Encryption:** Full encryption with `crypt_byte_block = skip_byte_block = 0`
- **IV Length:** 16-byte (128-bit) Initialization Vectors
- **Block Cipher:** AES-128-CBC mode

### Content Key Management

- **Fixed Keys:** Predetermined content keys for testing
- **Key Rotation:** Not applicable for test content
- **Multi-Key:** Support for separate audio/video keys

## Usage Guidelines

### Testing Scenarios

1. **CBCS Validation:** Test CBC encryption mode support
2. **VP9 Compatibility:** Verify modern codec handling
3. **Multi-DRM:** Test cross-platform DRM scenarios
4. **Pattern Encryption:** Validate subsample encryption

### Client Requirements

- **PlayReady 4.0+:** Required for CBCS and VP9 support
- **VP9 Decoder:** Hardware or software VP9 capability
- **CBCS Support:** CBC encryption mode handling
- **Modern Containers:** Fragmented MP4 and DASH support

### Performance Considerations

- **Decode Performance:** VP9 requires significant processing power
- **Pattern Encryption:** May impact decode performance
- **Network Efficiency:** Modern formats optimize bandwidth usage

## Troubleshooting

### Common Issues

1. **CBCS Compatibility**

   - Verify client supports CBC encryption mode
   - Check for proper pattern encryption handling
   - Validate IV handling for 16-byte vectors

2. **VP9 Playback**

   - Confirm VP9 decoder availability
   - Check hardware acceleration support
   - Verify container format compatibility

3. **Apple Toolchain Issues**

   - Be aware of KID handling bug in Apple tools
   - Use manifest KID values instead of container values
   - Test with different Apple toolchain versions

### Debug Information

- **Encryption Mode:** Verify CBCS vs CENC CTR handling
- **Pattern Information:** Check encryption pattern compliance
- **Codec Support:** Validate VP9 decoder capability
- **Container Parsing:** Verify fragmented MP4 handling

## Support Resources

For technical support and additional information:

- **PlayReady Business Queries:** [playready@microsoft.com](mailto:playready@microsoft.com)
- **PlayReady Operations:** Visit [wmlalicensing.com](http://wmlalicensing.com/) or email [ipla@microsoft.com](mailto:ipla@microsoft.com)
- **PlayReady Technical Support:** [AskDRM@microsoft.com](mailto:AskDRM@microsoft.com)
- **PlayReady Training Information:** [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## See Also

- [PlayReady 3.0+ Test Content](playready-3x-test-content.md)
- [PlayReady AV1 Test Content](playready-av1-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
