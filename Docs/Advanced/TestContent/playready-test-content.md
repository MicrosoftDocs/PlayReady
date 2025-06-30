---
title: PlayReady Test Content
description: Comprehensive collection of PlayReady test content for validation and compatibility testing across different versions and scenarios
ms.date: 6/30/2025
ms.topic: reference
---

This page provides access to a comprehensive collection of PlayReady test content designed to help developers validate their PlayReady implementations across different versions, codecs, and scenarios. The test content is organized by PlayReady version and specific use cases to facilitate targeted testing.

## Overview

The PlayReady test content collection includes content for:

- **Multiple PlayReady versions** - 2.0, 3.0, 4.0, and newer
- **Various codecs** - H.264, HEVC, AV1, VP9
- **Different encryption modes** - CENC, CBCS, PIFF
- **Streaming formats** - DASH, Smooth Streaming, HLS
- **Specialized scenarios** - Audio-only content, vendor-specific encoders

All test content is hosted on Microsoft's test servers and is freely available for PlayReady development and testing purposes.

## Test Content by PlayReady Version

### PlayReady 2.0+ Test Content

Content compatible with PlayReady version 2.0 and higher clients, including basic CENC encryption scenarios and traditional streaming formats.

- **[PlayReady 2.0+ Test Content](playready-2x-test-content.md)**
  - Tears of Steel 4K content
  - Super Speedway Trailer (protected and clear)
  - Live content with key rotation
  - Smooth Streaming and MPEG-DASH formats
  - Compatible with PlayReady 2.0, 2.5, 2.11, 3.0, 3.2, and higher

### PlayReady 3.0+ Test Content

Advanced test content featuring WRMHEADER v4.2 and content with separate keys for audio and video tracks.

- **[PlayReady 3.0+ Test Content](playready-3x-test-content.md)**
  - Multi-key content scenarios
  - H.264 and HEVC encoding
  - 4K and 1080p content
  - CENC v1 and v2 encryption
  - Separate audio/video key management
  - WRMHEADER v4.2 support

### PlayReady 4.0+ Test Content

Modern test content featuring CBCS encryption and support for next-generation codecs.

- **[PlayReady 4.0+ Test Content](playready-4x-test-content.md)**
  - CBCS (CBC with pattern) encryption
  - VP9 codec support
  - Advanced encryption patterns
  - Modern streaming scenarios
  - HLS and DASH integration

## Test Content by Codec and Format

### AV1 Test Content

Specialized content for testing PlayReady with the AV1 codec, supporting both CBC and CTR encryption modes.

- **[PlayReady AV1 Test Content](playready-av1-test-content.md)**
  - AV1 codec with PlayReady DRM
  - CENC and CBCS encryption modes
  - Big Buck Bunny reference content
  - DASH streaming format
  - Multi-DRM scenarios

### Audio-Only Test Content

Dedicated audio-only test content for validating PlayReady audio scenarios.

- **[PlayReady Audio Only Test Content](playready-audio-only-test-content.md)**
  - AAC-LC and AAC-HE audio formats
  - PIFF encryption
  - Smooth Streaming audio manifests
  - Audio-only DRM scenarios
  - Various bitrate configurations

## Specialized Test Content

### Vendor Encoder Test Content

Test content generated using specific encoder implementations from various vendors.

- **[PlayReady Vendor Test Content](playready-vendor-test-content.md)**
  - Anevia encoder content (ViaDemand, NEA LIVE 500)
  - Spotify multi-DRM content
  - Real-world encoder compatibility
  - Various streaming formats
  - Multi-DRM validation scenarios

## Quick Reference Guide

### By Use Case

| Use Case | Recommended Test Content |
|----------|-------------------------|
| **Basic PlayReady Integration** | [PlayReady 2.0+ Test Content](playready-2x-test-content.md) |
| **Multi-Key Scenarios** | [PlayReady 3.0+ Test Content](playready-3x-test-content.md) |
| **Modern Encryption (CBCS)** | [PlayReady 4.0+ Test Content](playready-4x-test-content.md) |
| **AV1 Codec Testing** | [PlayReady AV1 Test Content](playready-av1-test-content.md) |
| **Audio-Only Applications** | [PlayReady Audio Only Test Content](playready-audio-only-test-content.md) |
| **Encoder Compatibility** | [PlayReady Vendor Test Content](playready-vendor-test-content.md) |

### By Streaming Format

| Format | Available In |
|--------|-------------|
| **MPEG-DASH** | 2.0+, 3.0+, 4.0+, AV1 |
| **Smooth Streaming** | 2.0+, 3.0+, Audio-Only, Vendor |
| **HLS** | 4.0+, Vendor |
| **MP4 Files** | 3.0+, 4.0+, AV1, Vendor |

### By Codec

| Codec | Available In |
|-------|-------------|
| **H.264** | 2.0+, 3.0+, 4.0+, Vendor |
| **HEVC/H.265** | 3.0+, 4.0+ |
| **AV1** | AV1 Test Content |
| **VP9** | 4.0+ |
| **AAC Audio** | All content collections |

## Getting Started

### For New Developers

1. **Start with [PlayReady 2.0+ Test Content](playready-2x-test-content.md)** for basic integration testing
2. **Use clear content first** to validate basic playback functionality
3. **Test protected content** to verify DRM integration
4. **Progress to advanced scenarios** using 3.0+ and 4.0+ content

### For Advanced Testing

1. **Multi-key scenarios**: Use [PlayReady 3.0+ Test Content](playready-3x-test-content.md)
2. **Modern encryption**: Test with [PlayReady 4.0+ Test Content](playready-4x-test-content.md)
3. **Codec-specific**: Validate with [AV1](playready-av1-test-content.md) or vendor-specific content
4. **Specialized use cases**: Audio-only or encoder-specific scenarios

## Common License Server Configuration

Most test content can use the following license server configuration:

```http
LA_URL = http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(persist:false,sl:150)
```

**Note**: Some older test content includes default LA_URLs that may no longer be active. It's recommended to configure your client with the above URL instead of relying on embedded defaults.

## Technical Support

For technical support and additional information:

- **PlayReady Business Queries**: [playready@microsoft.com](mailto:playready@microsoft.com)
- **PlayReady Operations**: Visit [wmlalicensing.com](http://wmlalicensing.com/) or email [ipla@microsoft.com](mailto:ipla@microsoft.com)
- **PlayReady Technical Support**: [AskDRM@microsoft.com](mailto:AskDRM@microsoft.com)  
- **PlayReady Training Information**: [plyrdyev@microsoft.com](mailto:plyrdyev@microsoft.com)

## Related Topics

- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
- [How to Determine Client Features](../how-to-determine-client-features.md)
- [PlayReady Test Server](https://test.playready.microsoft.com/)
