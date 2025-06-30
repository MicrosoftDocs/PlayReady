# Versioned Servers for PlayReady Test Environment

## Overview

The PlayReady Test Environment provides multiple versioned servers to support testing across different PlayReady versions and feature sets. Each versioned server implements specific PlayReady capabilities and compliance requirements, enabling comprehensive testing of client implementations.

## Available Server Versions

### PlayReady 1.x Test Servers

Legacy servers for PlayReady 1.0-1.3 compatibility testing:

```url
https://playready-v1.directtaps.net/pr/svc/rightsmanager.asmx
```

**Features:**

- Basic license acquisition
- Simple output protection
- Legacy SOAP protocols
- Silverlight compatibility

### PlayReady 2.x Test Servers

Servers supporting PlayReady 2.0-2.3 features:

```url
https://playready-v2.directtaps.net/pr/svc/rightsmanager.asmx
```

**Features:**

- Enhanced license policies
- Domain-bound licenses
- Secure stop functionality
- Hardware-based DRM support

### PlayReady 3.x Test Servers

Modern servers with PlayReady 3.0+ capabilities:

```url
https://playready-v3.directtaps.net/pr/svc/rightsmanager.asmx
```

**Features:**

- Common Encryption (CENC) support
- Advanced output protection levels
- Secure delete functionality
- Enhanced key rotation

### PlayReady 4.x Test Servers

Latest servers supporting PlayReady 4.0+ features:

```url
https://playready-v4.directtaps.net/pr/svc/rightsmanager.asmx
```

**Features:**

- SL3000 security level support
- Advanced hardware security
- Enhanced policy enforcement
- Modern encryption standards

## Version-Specific Testing

### Client Version Detection

Test server compatibility with different client versions:

```javascript
// Test client version compatibility
async function testClientVersionCompatibility(clientVersion) {
    const serverUrl = getServerUrlForVersion(clientVersion);
    const response = await testLicenseAcquisition(serverUrl);
    return response.success;
}

function getServerUrlForVersion(version) {
    const versionMap = {
        '1.x': 'https://playready-v1.directtaps.net/pr/svc/rightsmanager.asmx',
        '2.x': 'https://playready-v2.directtaps.net/pr/svc/rightsmanager.asmx',
        '3.x': 'https://playready-v3.directtaps.net/pr/svc/rightsmanager.asmx',
        '4.x': 'https://playready-v4.directtaps.net/pr/svc/rightsmanager.asmx'
    };
    return versionMap[version];
}
```

### Feature Compatibility Matrix

| Feature | v1.x | v2.x | v3.x | v4.x |
|---------|------|------|------|------|
| Basic License Acquisition | ✓ | ✓ | ✓ | ✓ |
| Domain-Bound Licenses | ✗ | ✓ | ✓ | ✓ |
| Secure Stop | ✗ | ✓ | ✓ | ✓ |
| Secure Delete | ✗ | ✗ | ✓ | ✓ |
| Hardware Security | ✗ | Partial | ✓ | ✓ |
| Advanced OPLs | ✗ | ✗ | ✓ | ✓ |
| SL3000 Support | ✗ | ✗ | ✗ | ✓ |

## Version-Specific Configuration

### PlayReady 1.x Configuration

Basic license configuration for legacy clients:

```xml
<LicenseAcquisition>
    <Header>
        <DATA>
            <PROTECTINFO>
                <KEYLEN>16</KEYLEN>
                <ALGID>AESCTR</ALGID>
            </PROTECTINFO>
            <KID>base64-encoded-kid</KID>
            <CHECKSUM>base64-encoded-checksum</CHECKSUM>
        </DATA>
    </Header>
</LicenseAcquisition>
```

### PlayReady 2.x Configuration

Enhanced configuration with domain support:

```json
{
    "version": "2.0",
    "licenseType": "persistent",
    "keyId": "key-id-guid",
    "domainBinding": {
        "required": true,
        "domainId": "domain-service-id"
    },
    "outputProtection": {
        "digital": "required",
        "analog": "copy-never"
    }
}
```

### PlayReady 3.x Configuration

Modern configuration with advanced features:

```json
{
    "version": "3.0",
    "licenseType": "persistent",
    "keyId": "key-id-guid",
    "securityLevel": "SL2000",
    "outputProtectionLevels": {
        "compressedDigitalVideo": 270,
        "uncompressedDigitalVideo": 270,
        "analogVideo": 150,
        "compressedDigitalAudio": 200,
        "uncompressedDigitalAudio": 200
    },
    "secureStop": {
        "required": true,
        "serverUrl": "https://securestop.service.com"
    }
}
```

### PlayReady 4.x Configuration

Latest configuration with SL3000 support:

```json
{
    "version": "4.0", 
    "licenseType": "persistent",
    "keyId": "key-id-guid",
    "securityLevel": "SL3000",
    "hardwareBinding": {
        "required": true,
        "allowSoftwareFallback": false
    },
    "outputProtectionLevels": {
        "compressedDigitalVideo": 270,
        "uncompressedDigitalVideo": 270,
        "analogVideo": 100
    },
    "advancedSecurity": {
        "antiRollbackClock": true,
        "tamperResistance": "required"
    }
}
```

## Testing Scenarios by Version

### Version Compatibility Testing

Test scenarios for each server version:

#### PlayReady 1.x Testing

```javascript
// Basic license acquisition test
async function testPlayReady1x() {
    const config = {
        serverUrl: 'https://playready-v1.directtaps.net/pr/svc/rightsmanager.asmx',
        playRight: 1,
        keyId: 'test-key-id'
    };
    
    return await testBasicLicenseAcquisition(config);
}
```

#### PlayReady 2.x Testing

```javascript
// Domain-bound license test
async function testPlayReady2x() {
    const config = {
        serverUrl: 'https://playready-v2.directtaps.net/pr/svc/rightsmanager.asmx',
        licenseType: 'persistent',
        keyId: 'test-key-id',
        domainRequired: true
    };
    
    return await testDomainBoundLicense(config);
}
```

#### PlayReady 3.x Testing

```javascript
// Secure stop functionality test
async function testPlayReady3x() {
    const config = {
        serverUrl: 'https://playready-v3.directtaps.net/pr/svc/rightsmanager.asmx',
        licenseType: 'persistent', 
        keyId: 'test-key-id',
        secureStopRequired: true,
        securityLevel: 'SL2000'
    };
    
    return await testSecureStopFunctionality(config);
}
```

#### PlayReady 4.x Testing

```javascript
// Hardware security test
async function testPlayReady4x() {
    const config = {
        serverUrl: 'https://playready-v4.directtaps.net/pr/svc/rightsmanager.asmx',
        licenseType: 'persistent',
        keyId: 'test-key-id',
        securityLevel: 'SL3000',
        hardwareBindingRequired: true
    };
    
    return await testHardwareSecurity(config);
}
```

## Server Selection Strategy

### Automatic Version Detection

```javascript
async function selectOptimalServer(clientCapabilities) {
    // Check client PlayReady version
    const clientVersion = clientCapabilities.playreadyVersion;
    
    // Select compatible server version
    if (clientVersion >= '4.0') {
        return 'https://playready-v4.directtaps.net/pr/svc/rightsmanager.asmx';
    } else if (clientVersion >= '3.0') {
        return 'https://playready-v3.directtaps.net/pr/svc/rightsmanager.asmx';
    } else if (clientVersion >= '2.0') {
        return 'https://playready-v2.directtaps.net/pr/svc/rightsmanager.asmx';
    } else {
        return 'https://playready-v1.directtaps.net/pr/svc/rightsmanager.asmx';
    }
}
```

### Feature-Based Selection

```javascript
function selectServerByFeatures(requiredFeatures) {
    const serverCapabilities = {
        'v4': ['basic', 'domain', 'secureStop', 'secureDelete', 'sl3000'],
        'v3': ['basic', 'domain', 'secureStop', 'secureDelete', 'sl2000'],
        'v2': ['basic', 'domain', 'secureStop'],
        'v1': ['basic']
    };
    
    // Find minimum server version that supports all required features
    for (const [version, features] of Object.entries(serverCapabilities).reverse()) {
        if (requiredFeatures.every(feature => features.includes(feature))) {
            return `https://playready-${version}.directtaps.net/pr/svc/rightsmanager.asmx`;
        }
    }
    
    throw new Error('No compatible server version found');
}
```

## Migration Testing

### Cross-Version Compatibility

Test license compatibility across different server versions:

```javascript
async function testCrossVersionCompatibility() {
    const keyId = 'test-key-12345';
    const results = {};
    
    // Test each server version
    for (const version of ['v1', 'v2', 'v3', 'v4']) {
        try {
            const serverUrl = `https://playready-${version}.directtaps.net/pr/svc/rightsmanager.asmx`;
            results[version] = await testLicenseAcquisition(serverUrl, keyId);
        } catch (error) {
            results[version] = { success: false, error: error.message };
        }
    }
    
    return results;
}
```

### Upgrade Path Testing

Test client upgrade scenarios:

```javascript
async function testUpgradePath(fromVersion, toVersion) {
    // Get license from old server
    const oldServerUrl = `https://playready-${fromVersion}.directtaps.net/pr/svc/rightsmanager.asmx`;
    const oldLicense = await acquireLicense(oldServerUrl);
    
    // Test license compatibility with new server
    const newServerUrl = `https://playready-${toVersion}.directtaps.net/pr/svc/rightsmanager.asmx`;
    return await validateLicenseCompatibility(newServerUrl, oldLicense);
}
```

## Best Practices

### Server Selection Guidelines

1. **Match Client Version**: Use server version that matches or is compatible with client
2. **Feature Requirements**: Select based on required DRM features
3. **Security Level**: Choose appropriate security level for content
4. **Backward Compatibility**: Test with older server versions for compatibility

### Testing Recommendations

1. **Version Matrix Testing**: Test all client-server version combinations
2. **Feature Isolation**: Test individual features on appropriate server versions
3. **Migration Scenarios**: Test upgrade and downgrade paths
4. **Error Handling**: Test version mismatch error scenarios

## Monitoring and Diagnostics

### Server Health Checks

```javascript
async function checkServerHealth(version) {
    const serverUrl = `https://playready-${version}.directtaps.net/pr/svc/rightsmanager.asmx`;
    
    try {
        const response = await fetch(`${serverUrl}?health`);
        return {
            version: version,
            status: response.ok ? 'healthy' : 'unhealthy',
            responseTime: response.headers.get('x-response-time')
        };
    } catch (error) {
        return {
            version: version,
            status: 'error',
            error: error.message
        };
    }
}
```

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [How to Test Client-Server Versions](../how-to-test-client-server-versions.md) - Version testing guidance
- [How to Migrate](../how-to-migrate.md) - Migration guidance
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with versioned servers:

1. Verify client-server version compatibility
2. Check feature support matrix
3. Test with appropriate server version
4. Review version-specific configuration requirements
5. Validate security level requirements

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
