---
title: PlayReady Audio Only Test Content
description: Collection of audio-only test content for PlayReady validation and compatibility testing
author: Microsoft
ms.author: Microsoft
ms.date: 2024-01-15
ms.service: playready
ms.topic: reference
---

# Audio Only Test Content

This page provides a collection of audio-only test content that can be used to validate PlayReady functionality with audio streams. These test files are designed to help developers and integrators test their PlayReady implementations with various audio encoding formats.

## Overview

The audio-only test content collection includes:

- **AAC-LC encoded audio** - Standard AAC Low Complexity audio files
- **AAC-HE encoded audio** - High Efficiency AAC audio files
- **PIFF encryption** - Protected Interoperable File Format with AES128-CTR encryption
- **Smooth Streaming manifests** - Both protected and clear versions

All content uses PlayReady WRMHEADER version 4.0 and is encrypted using PIFF (Protected Interoperable File Format) with AES128-CTR encryption.

## Audio Test Content Collection

### AAC-LC Audio Content

#### Taxi3 AAC-LC Audio (Smooth Streaming)

| Property | Value |
|----------|-------|
| **Tool Chain** | Smooth Protect (IIS Media Transform) |
| **Creation Date** | 01 February 2010 |
| **Video Encoding Settings** | None |
| **Audio Encoding Settings** | AAC-LC |
| **Encryption Settings** | PIFF Encryption AES128-CTR |
| **Multi DRM** | False |
| **PlayReady WRMHEADER** | 4.0 |
| **Smooth Streaming Manifest (Protected)** | `https://test.playready.microsoft.com/media/profficialsite/Taxi3_AACLCPR.ism/manifest` |
| **Smooth Streaming Manifest (Clear)** | `https://test.playready.microsoft.com/media/profficialsite/Taxi3_AACLC.ism/manifest` |

### AAC-HE Audio Content

#### Taxi3 AAC-HE Audio (Smooth Streaming)

| Property | Value |
|----------|-------|
| **Tool Chain** | Smooth Protect (IIS Media Transform) |
| **Creation Date** | 01 February 2010 |
| **Video Encoding Settings** | None |
| **Audio Encoding Settings** | AAC-HE |
| **Encryption Settings** | PIFF Encryption AES128-CTR |
| **Multi DRM** | False |
| **PlayReady WRMHEADER** | 4.0 |
| **Smooth Streaming Manifest (Protected)** | `https://test.playready.microsoft.com/media/profficialsite/Taxi3_AACHEPR.ism/manifest` |
| **Smooth Streaming Manifest (Clear)** | `https://test.playready.microsoft.com/media/profficialsite/Taxi3_AACHE.ism/manifest` |

## Technical Details

### Audio Encoding Specifications

#### AAC-LC (Advanced Audio Coding - Low Complexity)

- **Format**: AAC Low Complexity profile
- **Use Case**: General purpose audio compression
- **Compatibility**: Widely supported across devices and platforms
- **Efficiency**: Good compression ratio with moderate computational requirements

#### AAC-HE (Advanced Audio Coding - High Efficiency)

- **Format**: AAC High Efficiency profile
- **Use Case**: Low bitrate audio streaming
- **Compatibility**: Supported by most modern audio decoders
- **Efficiency**: Excellent compression for low bitrate scenarios

### Encryption Details

#### PIFF (Protected Interoperable File Format)

- **Encryption Algorithm**: AES128-CTR
- **Key Management**: PlayReady DRM system
- **Compatibility**: ISO/IEC 23001-7 compliant
- **Interoperability**: Works with DASH and Smooth Streaming

## Usage Guidelines

### Testing Scenarios

1. **Audio-Only Playback Testing**
   - Verify PlayReady license acquisition for audio content
   - Test audio decryption and playback
   - Validate audio quality and synchronization

2. **Format Compatibility Testing**
   - Test AAC-LC decoding capabilities
   - Verify AAC-HE playback support
   - Validate PIFF container handling

3. **Streaming Protocol Testing**
   - Test Smooth Streaming manifest parsing
   - Verify adaptive bitrate switching for audio
   - Test protected vs. clear content handling

### Implementation Notes

- **License Acquisition**: Ensure your PlayReady client can handle audio-only content licenses
- **Decoder Support**: Verify AAC-LC and AAC-HE decoder availability
- **Container Parsing**: Implement proper PIFF container parsing for encrypted audio
- **Error Handling**: Test with both protected and clear versions for comparison

## Testing Recommendations

### Basic Audio Playback

1. Start with clear content to verify basic audio playback
2. Test protected content to validate DRM integration
3. Compare audio quality between protected and clear versions

### Advanced Testing

1. Test with different audio output configurations
2. Verify playback across various sample rates
3. Test interrupt handling during audio playback

### Compatibility Testing

1. Test on different audio hardware configurations
2. Verify performance with various AAC decoder implementations
3. Test integration with audio processing pipelines

## Troubleshooting

### Common Issues

#### Audio Playback Failures

- **Cause**: Missing AAC decoder support
- **Solution**: Ensure proper AAC-LC and AAC-HE decoder installation

#### License Acquisition Errors

- **Cause**: Incorrect PlayReady client configuration
- **Solution**: Verify license server URLs and client certificates

#### Format Compatibility Issues

- **Cause**: Unsupported PIFF container features
- **Solution**: Update container parsing libraries

### Debug Steps

1. **Verify Clear Content Playback**

   ```text
   Test with clear audio files first to isolate DRM issues
   ```

2. **Check License Acquisition**

   ```text
   Monitor PlayReady license requests and responses
   ```

3. **Validate Audio Decoding**

   ```text
   Test AAC decoder functionality independently
   ```

## Support Resources

### Business Queries

- **Email**: [playready@microsoft.com](mailto:playready@microsoft.com)

### Operations Queries

- **Website**: [http://wmlalicensing.com/](http://wmlalicensing.com/)
- **Email**: [ipla@microsoft.com](mailto:ipla@microsoft.com)

### Technical Support

- **Support Portal**: [PlayReady Technical Support](https://test.playready.microsoft.com/Support/SupportOptions)

### Training Information

- **Email**: [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## Related Topics

- [PlayReady 2.0+ Test Content](playready-2x-test-content.md)
- [PlayReady 3.0+ Test Content](playready-3x-test-content.md)
- [PlayReady 4.0+ Test Content](playready-4x-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
