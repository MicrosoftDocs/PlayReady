---
title: Testing Output Protections
description: Documentation for testing PlayReady output protection policies and restrictions using test server
ms.topic: reference
ms.date: 06/30/2025
---

# Testing Output Protections

## Overview

PlayReady output protections ensure that protected content maintains its security requirements across different output types and quality levels. This documentation provides a complete mapping of output protection policies defined in the Compliance Rules and their corresponding test server parameter syntax.

## Output Protection Categories

### Audio Output Protections

#### Compressed Digital Audio Content

**Compliance Reference**: CRs section 3.6.2

**Parameter Syntax**: `caopl:200`

**Description**: Controls output protection level for compressed digital audio content such as MP3, AAC, or other compressed audio formats.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(caopl:200)
```

#### Explicit Digital Audio Output Restriction

**Compliance Reference**: CRs section 3.6.2.8

**Parameter Syntax**: `avop:(guid:6D5CFA59-C250-4426-930E-FAC72C8FCFA6)`

**Description**: Provides explicit restrictions on digital audio outputs using specific GUID identifiers.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(avop:(guid:6D5CFA59-C250-4426-930E-FAC72C8FCFA6))
```

#### Uncompressed Digital Audio Content

**Compliance Reference**: CRs section 3.6.3

**Parameter Syntax**: `ucaopl:200`

**Description**: Controls output protection level for uncompressed digital audio content such as PCM or other uncompressed audio formats.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(ucaopl:200)
```

### Video Output Protections

#### Compressed Digital Video Content

**Compliance Reference**: CRs section 3.6.4

**Parameter Syntax**: `cvopl:500`

**Description**: Controls output protection level for compressed digital video content such as H.264, H.265, or other compressed video formats.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(cvopl:500)
```

#### Uncompressed Digital Video Content

**Compliance Reference**: CRs section 3.6.5

**Parameter Syntax**: `ucvopl:200`

**Description**: Controls output protection level for uncompressed digital video content.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(ucvopl:200)
```

### Advanced Video Protection Features

#### Maximum Decode Resolution

**Compliance Reference**: CRs section 3.6.5.7.1

**Parameter Syntax Options**:
- Simple: `maxres:1920x1080`
- Advanced: `dvop:(guid:9645E831-E01D-4FFF-8342-0A720E3E028F,data:AAAEOAAAB4A=)`

**Description**: Restricts the maximum resolution at which content can be decoded and displayed.

**Examples**:
```url
# Simple resolution restriction
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(maxres:1920x1080)

# Advanced resolution restriction using GUID
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(dvop:(guid:9645E831-E01D-4FFF-8342-0A720E3E028F,data:AAAEOAAAB4A=))
```

#### HDCP Type Restriction

**Compliance Reference**: CRs section 3.6.5.7.2

**Parameter Syntax**: `dvop:(guid:ABB2C6F1-E663-4625-A945-972D17B231E7,data:AAAAAQ==)`

**Description**: Specifies High-bandwidth Digital Content Protection (HDCP) requirements for digital video outputs.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(dvop:(guid:ABB2C6F1-E663-4625-A945-972D17B231E7,data:AAAAAQ==))
```

### Analog Output Protections

#### Analog Television Outputs

**Compliance Reference**: CRs section 3.6.6

**Parameter Syntax**: `avopl:200`

**Description**: Controls output protection level for analog television outputs.

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(avopl:200)
```

#### Extended Analog TV Controls - CGMS-A

**Compliance Reference**: CRs section 3.6.7.1

**Parameter Syntax**: `avop:(guid:225CD36F-F132-49EF-BA8C-C91EA28E4369,data:AAAAAQ==)`

**Server SDK Code**:
```csharp
right.AddAnalogVideoOutputProtection(
    new Guid("{225CD36F-F132-49EF-BA8C-C91EA28E4369}"), 
    BitConverter.GetBytes((int)1)
);
```

**Description**: Implements Copy Generation Management System - Analog (CGMS-A) protection for analog television outputs.

#### Extended Analog TV Controls - AGCCS

**Compliance Reference**: CRs section 3.6.7.2

**Parameter Syntax**: `avop:(guid:C3FD11C6-F8B7-4D20-B008-1DB17D61F2DA,data:AgAAAA==)`

**Server SDK Code**:
```csharp
right.AddAnalogVideoOutputProtection(
    new Guid("C3FD11C6-F8B7-4D20-B008-1DB17D61F2DA"), 
    BitConverter.GetBytes((int)2)
);
```

**Description**: Implements Automatic Gain Control Copy System (AGCCS) protection for analog television outputs.

#### Analog Computer Monitor Output

**Compliance Reference**: CRs section 3.6.8

**Parameter Syntax**: `avop:(guid:D783A191-E083-4BAF-B2DA-E69F910B3772)`

**Description**: Controls output protection for analog computer monitor connections (VGA, etc.).

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(avop:(guid:D783A191-E083-4BAF-B2DA-E69F910B3772))
```

#### Analog Component Video Output

**Compliance Reference**: CRs section 3.6.9

**Parameter Syntax**: `avop:(guid:811C5110-46C8-4C6E-8163-C0482A15D47E)`

**Description**: Controls output protection for analog component video outputs (YPbPr).

**Example**:
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(avop:(guid:811C5110-46C8-4C6E-8163-C0482A15D47E))
```

#### Digital Video Only Content

**Compliance Reference**: CRs section 3.6.11

**Parameter Syntax**: `avop:(guid:760AE755-682A-41E0-B1B3-DCDF836A7306,data:AAAAAQ==)`

**Server SDK Code**:
```csharp
right.AddAnalogVideoOutputProtection(
    new Guid("{760AE755-682A-41E0-B1B3-DCDF836A7306}"), 
    BitConverter.GetBytes((int)1)
);
```

**Description**: Restricts content to digital video outputs only, preventing analog video output.

### Unknown Output Handling

#### Passing to Unknown Output

**Compliance Reference**: CRs section 3.9.1

**Parameter Syntax Options**:
- `allowunknownhd:true`
- `playenablers:(786627D8-C2A6-44BE-8F88-08AE255B01A7)`

**Description**: Controls whether content can be passed to unknown or unrecognized outputs at high definition quality.

**Examples**:
```url
# Allow unknown HD outputs
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(allowunknownhd:true)

# Using play enabler GUID
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(playenablers:(786627D8-C2A6-44BE-8F88-08AE255B01A7))
```

#### Passing Constrained Resolution to Unknown Output

**Compliance Reference**: CRs section 3.9.2

**Parameter Syntax Options**:
- `allowunknownsd:true`
- `playenablers:(B621D91F-EDCC-4035-8D4B-DC71760D43E9)`

**Description**: Controls whether content can be passed to unknown outputs at standard definition quality.

**Examples**:
```url
# Allow unknown SD outputs
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(allowunknownsd:true)

# Using play enabler GUID
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(playenablers:(B621D91F-EDCC-4035-8D4B-DC71760D43E9))
```

## Protection Level Values

### Common Protection Levels

| Level | Description | Usage |
|-------|-------------|-------|
| 100   | Minimal protection | Basic content, low security requirements |
| 150   | Low protection | Standard definition content |
| 200   | Medium protection | High definition content |
| 270   | High protection | Premium content |
| 300   | Maximum protection | Ultra-high value content |

### Audio-Specific Levels

| Level | Description | Audio Quality |
|-------|-------------|---------------|
| 100   | Basic audio protection | Compressed, low bitrate |
| 150   | Standard audio protection | CD quality |
| 200   | High audio protection | High-resolution audio |
| 250   | Premium audio protection | Lossless audio |

### Video-Specific Levels

| Level | Description | Video Quality |
|-------|-------------|---------------|
| 150   | Standard definition | Up to 480p |
| 200   | High definition | Up to 720p |
| 270   | Full HD | Up to 1080p |
| 300   | Ultra HD | 4K and above |

## Testing Scenarios

### Basic Output Protection Testing

```javascript
// Test basic video output protection
async function testVideoOutputProtection() {
    const testCases = [
        { name: 'SD Video', config: 'cvopl:150' },
        { name: 'HD Video', config: 'cvopl:200' },
        { name: 'Full HD Video', config: 'cvopl:270' }
    ];
    
    for (const testCase of testCases) {
        const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(${testCase.config})`;
        const result = await testLicenseAcquisition(url);
        console.log(`${testCase.name}: ${result.success ? 'PASS' : 'FAIL'}`);
    }
}
```

### HDCP Requirement Testing

```javascript
// Test HDCP requirements
async function testHDCPRequirements() {
    const hdcpConfig = 'dvop:(guid:ABB2C6F1-E663-4625-A945-972D17B231E7,data:AAAAAQ==)';
    const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(${hdcpConfig})`;
    
    const result = await testLicenseAcquisition(url);
    return result.outputProtections.hdcpRequired;
}
```

### Analog Protection Testing

```javascript
// Test analog output restrictions
async function testAnalogProtections() {
    const analogTests = [
        {
            name: 'Analog TV Protection',
            config: 'avopl:200'
        },
        {
            name: 'CGMS-A Protection',
            config: 'avop:(guid:225CD36F-F132-49EF-BA8C-C91EA28E4369,data:AAAAAQ==)'
        },
        {
            name: 'Digital Video Only',
            config: 'avop:(guid:760AE755-682A-41E0-B1B3-DCDF836A7306,data:AAAAAQ==)'
        }
    ];
    
    const results = [];
    for (const test of analogTests) {
        const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(${test.config})`;
        const result = await testLicenseAcquisition(url);
        results.push({
            test: test.name,
            success: result.success,
            analogRestricted: result.outputProtections.analogRestricted
        });
    }
    
    return results;
}
```

## Server SDK Implementation

### Basic Output Protection Setup

```csharp
// Add video output protection level
right.AddVideoOutputProtectionLevel(
    PlayReadyVideoOutputProtectionLevel.CompressedDigitalVideo, 
    270
);

// Add audio output protection level  
right.AddAudioOutputProtectionLevel(
    PlayReadyAudioOutputProtectionLevel.CompressedDigitalAudio,
    200
);
```

### Advanced Protection Configuration

```csharp
// Add specific analog video output protection
right.AddAnalogVideoOutputProtection(
    new Guid("{225CD36F-F132-49EF-BA8C-C91EA28E4369}"), 
    BitConverter.GetBytes((int)1)
);

// Add HDCP requirement
right.AddDigitalVideoOutputProtection(
    new Guid("{ABB2C6F1-E663-4625-A945-972D17B231E7}"), 
    BitConverter.GetBytes((int)1)
);

// Add maximum resolution restriction
right.AddDigitalVideoOutputProtection(
    new Guid("{9645E831-E01D-4FFF-8342-0A720E3E028F}"), 
    resolutionData
);
```

### Play Enabler Configuration

```csharp
// Allow unknown outputs at SD quality
right.AddPlayEnabler(
    new Guid("{B621D91F-EDCC-4035-8D4B-DC71760D43E9}")
);

// Allow unknown outputs at HD quality
right.AddPlayEnabler(
    new Guid("{786627D8-C2A6-44BE-8F88-08AE255B01A7}")
);
```

## Best Practices

### Output Protection Strategy

1. **Assess Content Value** - Higher value content requires stricter protection
2. **Consider Device Capabilities** - Ensure devices can support required protection levels
3. **Test Across Platforms** - Validate protection on different device types
4. **Balance Security and Usability** - Avoid overly restrictive policies

### Implementation Guidelines

1. **Start with Basic Protection** - Begin with standard protection levels
2. **Add Specific Restrictions** - Layer additional protections as needed
3. **Test Unknown Output Handling** - Validate behavior with unrecognized outputs
4. **Document Protection Requirements** - Clearly specify protection policies

### Testing Recommendations

1. **Comprehensive Testing** - Test all protection levels and combinations
2. **Device Compatibility** - Validate on target device types
3. **Output Type Testing** - Test with different output connection types
4. **Failure Scenario Testing** - Verify behavior when protection fails

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main test server functionality
- [Query String Syntax](query-string-syntax.md) - Parameter syntax reference
- [Testing Server Exceptions](testing-server-exceptions.md) - Error condition testing
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

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

---

© Microsoft Corporation. All rights reserved. [Trademarks](https://www.microsoft.com/legal/intellectualproperty/trademarks) | [Privacy](https://privacy.microsoft.com/)
