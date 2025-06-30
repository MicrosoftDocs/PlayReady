# Legacy Syntax for PlayReady Test Server

## Overview

The PlayReady Test Server maintains support for legacy syntax to ensure backward compatibility with older PlayReady implementations and existing client applications. This legacy approach uses simplified parameter formats and traditional HTTP methods that have been supported since early PlayReady versions.

## Legacy URL Format

The legacy syntax uses a simplified URL structure:

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=1&kid=KEY_ID
```

## Supported Legacy Parameters

### PlayRight Parameter

The `PlayRight` parameter specifies basic license permissions:

- **1**: Allow playback (basic license)
- **2**: Allow playback with copy protection
- **3**: Allow playback with enhanced protection
- **0**: Deny playback (for testing denial scenarios)

### Key ID Parameter (`kid`)

Legacy format supports simplified Key ID specification:

- Standard GUID format: `12345678-1234-1234-1234-123456789012`
- Simplified format: `123456789012345678901234567890123456`
- Base64-encoded format: `base64-encoded-key-id`

## Legacy License Types

### Basic Playback License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=1&kid=12345678-1234-1234-1234-123456789012
```

### Copy-Protected License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=2&kid=12345678-1234-1234-1234-123456789012
```

### Enhanced Protection License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=3&kid=12345678-1234-1234-1234-123456789012
```

## Legacy HTTP Methods

### POST Request Format

Traditional SOAP-based license acquisition:

```http
POST /pr/svc/rightsmanager.asmx HTTP/1.1
Host: playready.directtaps.net
Content-Type: text/xml; charset=utf-8
SOAPAction: "http://schemas.microsoft.com/DRM/2007/03/protocols/AcquireLicense"

<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://www.w3.org/2003/05/soap-envelope">
  <soap:Body>
    <AcquireLicense xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
      <challenge>base64-encoded-challenge</challenge>
    </AcquireLicense>
  </soap:Body>
</soap:Envelope>
```

### GET Request Format

Simple GET-based license requests:

```http
GET /pr/svc/rightsmanager.asmx?PlayRight=1&kid=12345678-1234-1234-1234-123456789012 HTTP/1.1
Host: playready.directtaps.net
```

## Client Integration Examples

### Legacy JavaScript Implementation

```javascript
// Legacy URL construction
function buildLegacyLicenseUrl(keyId, playRight) {
    return `https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=${playRight}&kid=${keyId}`;
}

// Basic license request
const licenseUrl = buildLegacyLicenseUrl(keyId, 1);

// Use with legacy PlayReady implementations
```

### Legacy C# Implementation

```csharp
// Legacy license request construction
public string BuildLegacyLicenseUrl(string keyId, int playRight)
{
    return $"https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight={playRight}&kid={keyId}";
}

// Usage
string licenseUrl = BuildLegacyLicenseUrl(keyId, 1);
```

## Compatibility Matrix

### PlayReady Version Support

| PlayReady Version | Legacy Support | Recommended Approach |
|------------------|----------------|---------------------|
| 1.0 - 1.3        | Full          | Legacy Syntax       |
| 2.0 - 2.3        | Full          | Legacy or Modern    |
| 3.0+             | Limited       | Modern Syntax       |
| 4.0+             | Deprecated    | Modern Syntax       |

### Client Platform Support

| Platform | Legacy Support | Notes |
|----------|----------------|-------|
| Windows Legacy | Full | Original implementation |
| Silverlight | Full | Legacy platform support |
| Windows 10+ | Limited | Modern APIs preferred |
| Mobile Platforms | Varies | Check platform documentation |

## Migration Guidance

### From Legacy Syntax

When migrating from legacy syntax to modern approaches:

#### Step 1: Identify Current Usage

```javascript
// Current legacy usage
const legacyUrl = `https://playready.directtaps.net/pr/svc/rightsmanager.asmx?PlayRight=1&kid=${keyId}`;
```

#### Step 2: Map to Modern Equivalent

```javascript
// Modern equivalent
const modernConfig = {
    licenseType: "persistent",
    keyId: keyId,
    policies: {
        playback: {
            allowOffline: true
        }
    }
};
```

#### Step 3: Update License Acquisition

```javascript
// Modern license request
const licenseUrl = "https://playready.directtaps.net/pr/svc/rightsmanager.asmx";
// Include modern configuration in request body
```

## Limitations of Legacy Syntax

### Functional Limitations

- **Limited Policy Control**: Basic playback permissions only
- **No Advanced Features**: Missing modern DRM capabilities
- **Simplified Protection**: Basic copy protection options
- **No Domain Support**: Domain-bound licenses not supported

### Security Considerations

- **Older Encryption**: Uses legacy encryption methods
- **Limited Validation**: Reduced security validation
- **Compatibility Issues**: May not work with modern security requirements

## Testing Legacy Implementations

### Basic Functionality Tests

```javascript
// Test basic playback
testLegacyLicense(keyId, 1); // Should allow playback

// Test copy protection
testLegacyLicense(keyId, 2); // Should enable copy protection

// Test denial scenario
testLegacyLicense(keyId, 0); // Should deny playback
```

### Compatibility Testing

1. **Version Testing**: Test with different PlayReady versions
2. **Platform Testing**: Verify on supported platforms
3. **Feature Testing**: Validate available features work correctly
4. **Migration Testing**: Test upgrade paths to modern syntax

## Error Handling

### Legacy-Specific Errors

- **Unsupported PlayRight**: Invalid PlayRight parameter value
- **Legacy Key Format**: Key ID format not supported in legacy mode
- **Version Mismatch**: Client version incompatible with legacy server

### Error Response Format

Legacy error responses use simplified XML format:

```xml
<?xml version="1.0" encoding="utf-8"?>
<Error>
    <Code>400</Code>
    <Message>Invalid PlayRight parameter</Message>
</Error>
```

## Best Practices

### When to Use Legacy Syntax

1. **Legacy Systems**: Supporting older PlayReady implementations
2. **Backward Compatibility**: Maintaining compatibility with existing clients
3. **Simple Requirements**: Basic playback without advanced features
4. **Migration Period**: During transition to modern implementations

### Recommended Alternatives

For new implementations, consider:

- [Query String Syntax](query-string-syntax.md) - Simple modern approach
- [CustomData JSON Syntax](customdata-json-syntax.md) - Advanced configuration
- [Base64 JSON Syntax](base64-json-syntax.md) - Compact modern format

## Deprecation Notice

> **Note**: Legacy syntax support is maintained for backward compatibility but is deprecated for new implementations. Consider migrating to modern syntax for enhanced features and security.

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [Query String Syntax](query-string-syntax.md) - Modern simple approach
- [How to Migrate](../how-to-migrate.md) - Migration guidance
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with legacy syntax:

1. Verify PlayReady version compatibility
2. Check parameter format and values
3. Test with simplified configurations
4. Consider migration to modern syntax
5. Review platform-specific documentation

For migration assistance and modern alternatives, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
