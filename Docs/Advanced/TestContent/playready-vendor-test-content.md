---
title: PlayReady Test Content from Encoder Vendors
description: Collection of test content generated using specific encoders for compatibility validation
ms.date: 06/30/2025
ms.topic: reference
---

This page provides a collection of test content that has been generated using specific encoders from various vendors. This content allows client developers and OEMs to verify compatibility with specific encoder implementations and validate their PlayReady integration across different encoding toolchains.

## Overview

The vendor-specific test content collection includes:

- **Spotify-specific content** - Multi-DRM content for dual DRM scenarios
- **Various encoding toolchains** - Different encoder implementations and configurations
- **Multiple streaming formats** - Support for Smooth Streaming, HLS, and MP4

This content helps ensure interoperability across different encoding ecosystems and validates PlayReady implementations with real-world encoder outputs.

## Vendor Test Content Collection

### Spotify Multi-DRM Content

#### Big Buck Bunny Dual DRM

| Property | Value |
|----------|-------|
| **Description** | Source: Big Buck BUNNY ([https://peach.blender.org/](https://peach.blender.org/)) |
| **Tool Chain** | Spotify Specific |
| **Creation Date** | 01 October 2017 |
| **Video Encoding Settings** | N/A |
| **Audio Encoding Settings** | AAC |
| **Encryption Settings** | CENC AES128-CTR |
| **Key ID (KID)** | `{b0498601-8a4a-4418-9fa5-5a326ea2961c}` |
| **Key ID (Base64)** | `AYZJsEqKGESfpVoybqKWHA==` |
| **Key Value (Hex)** | `{0x12, 0x34, 0x56, 0x78, 0x12, 0x34, 0x56, 0x78, 0x12, 0x34, 0x56, 0x78, 0x12, 0x34, 0x56, 0x78}` |
| **Key Value (Base64)** | `EjRWeBI0VngSNFZ4EjRWeA==` |
| **Audio KID** | `{b0498601-8a4a-4418-9fa5-5a326ea2961c}` |
| **Multi DRM** | True |
| **PlayReady WRMHEADER** | 4.0 |
| **Encrypted File** | `https://prtsprodstorage.blob.core.windows.net/media/vendor/Spotify-DualDRM2017-bbb/Spotify-DualDRM2017-bbb.mp4` |

## Technical Details

### Encoder Specifications

#### Anevia ViaDemand

- **Type**: Video-on-Demand encoding solution
- **Video Support**: H.264 AVC1 up to Full HD (1920x1080)
- **Audio Support**: AAC-HE with mono channel support
- **Streaming**: Supports both Smooth Streaming and HLS output
- **Use Case**: VOD content preparation and delivery

#### Anevia NEA LIVE 500

- **Type**: Live encoding solution
- **Video Support**: H.264 AVC1 up to Full HD (1920x1080)
- **Audio Support**: AAC-LC stereo with high-quality encoding
- **Streaming**: Real-time Smooth Streaming and HLS generation
- **Use Case**: Live broadcast and streaming applications

#### Spotify Encoder

- **Type**: Custom encoding toolchain
- **Multi-DRM Support**: Dual DRM implementation
- **Content Source**: High-quality reference content (Big Buck Bunny)
- **Use Case**: Multi-DRM compatibility testing

### Encryption Implementation

#### CENC (Common Encryption)

- **Standard**: ISO/IEC 23001-7
- **Algorithm**: AES128-CTR
- **Key Management**: PlayReady and additional DRM systems
- **Compatibility**: Cross-platform DRM interoperability

#### Key Management

- **Key Rotation**: Support for dynamic key changes
- **Multi-DRM**: Simultaneous support for multiple DRM systems
- **Security**: Industry-standard encryption practices

## Usage Guidelines

### Testing Scenarios

1. **Encoder Compatibility Testing**
   - Validate content from specific encoder implementations
   - Test encoding parameter variations
   - Verify output format compatibility

2. **Multi-DRM Validation**
   - Test dual DRM scenario implementations
   - Validate key sharing between DRM systems
   - Verify license acquisition for multiple DRM providers

3. **Streaming Protocol Testing**
   - Test Smooth Streaming manifest parsing
   - Validate HLS playlist handling
   - Verify adaptive streaming behavior

### Implementation Notes

- **Encoder Integration**: Test with specific encoder outputs to validate compatibility
- **Multi-DRM Support**: Implement proper handling for dual DRM scenarios
- **Streaming Protocols**: Ensure support for both Smooth Streaming and HLS
- **Key Management**: Handle complex key scenarios including multi-DRM keys

## Testing Recommendations

### Encoder-Specific Testing

1. **Anevia Content Testing**
   - Test both VOD and Live encoder outputs
   - Validate different audio encoding configurations
   - Test manifest parsing for Anevia-specific features

2. **Multi-DRM Testing**
   - Implement dual DRM license acquisition
   - Test key sharing scenarios
   - Validate fallback mechanisms

### Advanced Validation

1. **Real-World Scenarios**
   - Test with production-like encoder configurations
   - Validate performance under different encoding settings
   - Test integration with existing encoding workflows

2. **Compatibility Testing**
   - Test across different PlayReady client implementations
   - Validate with various hardware decoder configurations
   - Test streaming protocol switching

## Troubleshooting

### Common Issues

#### Encoder-Specific Compatibility

- **Cause**: Encoder-specific format variations
- **Solution**: Validate content parsing with specific encoder outputs

#### Multi-DRM License Acquisition

- **Cause**: Complex key management in dual DRM scenarios
- **Solution**: Implement proper key resolution for multiple DRM systems

#### Streaming Format Issues

- **Cause**: Encoder-specific manifest variations
- **Solution**: Update manifest parsers for vendor-specific implementations

### Debug Steps

1. **Validate Encoder Output**

   ```text
   Test content parsing with specific encoder implementations
   ```

2. **Check Multi-DRM Configuration**

   ```text
   Verify key management for dual DRM scenarios
   ```

3. **Test Streaming Protocols**

   ```text
   Validate manifest parsing for different streaming formats
   ```

## Vendor Information

### Ateme (formerly Anevia)

- **Website**: [https://www.ateme.com/](https://www.ateme.com/)
- **Products**: ViaDemand (VOD), NEA LIVE 500 (Live Encoding)
- **Specialization**: Professional video encoding and streaming solutions

### Content Sources

- **Big Buck Bunny**: Open source reference content from [Blender Foundation](https://peach.blender.org/)
- **Test Content**: Various encoder-specific test materials

## Support Resources

### Business Queries

- **Email**: [playready@microsoft.com](mailto:playready@microsoft.com)

### Operations Queries

- **Website**: [http://wmlalicensing.com/](http://wmlalicensing.com/)
- **Email**: [ipla@microsoft.com](mailto:ipla@microsoft.com)

### Technical Support

- **Support Portal**: [PlayReady Technical Support](mailto:AskDRM@microsoft.com)

### Training Information

- **Email**: [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## Related Topics

- [PlayReady 2.0+ Test Content](playready-2x-test-content.md)
- [PlayReady 3.0+ Test Content](playready-3x-test-content.md)
- [PlayReady 4.0+ Test Content](playready-4x-test-content.md)
- [PlayReady Audio Only Test Content](playready-audio-only-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
