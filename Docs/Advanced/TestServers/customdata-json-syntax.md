---
title: CustomData JSON Syntax for PlayReady Test Server
description: Documentation for CustomData JSON syntax used in PlayReady test server license configuration
ms.topic: reference
ms.date: 06/30/2025
---

# CustomData JSON Syntax for PlayReady Test Server

## Overview

The PlayReady Test Server supports CustomData JSON syntax for advanced license configuration. This method allows developers to specify complex license parameters and policies using JSON format within the CustomData field of license requests.

## JSON Structure

The CustomData field accepts a JSON object with various configuration parameters:

```json
{
  "version": "1.0",
  "config": {
    "licenseType": "persistent|non-persistent|rental|subscription",
    "keyId": "GUID",
    "contentKey": "base64-encoded-key",
    "policies": {
      "outputProtection": {
        "digital": "required|optional|never",
        "analog": "required|optional|never"
      },
      "playback": {
        "allowOffline": true|false,
        "expirationDate": "ISO-8601-datetime",
        "gracePeriod": "duration-in-seconds"
      }
    }
  }
}
```

## Configuration Parameters

### License Type

Specifies the type of license to generate:

- **persistent**: License stored on device, survives application restart
- **non-persistent**: Temporary license, expires when application closes
- **rental**: Time-limited license with specific expiration
- **subscription**: Subscription-based license with periodic validation

### Key Management

Configure encryption keys and identifiers:

```json
{
  "keyId": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
  "contentKey": "base64EncodedContentKey",
  "keyRotation": {
    "enabled": true,
    "interval": "PT1H"
  }
}
```

### Output Protection Policies

Control output protection requirements:

```json
{
  "outputProtection": {
    "digital": {
      "hdcp": "required",
      "cgmsa": "copy-never"
    },
    "analog": {
      "macrovision": "required",
      "cgmsa": "copy-once"
    }
  }
}
```

## Example Configurations

### Basic Persistent License

```json
{
  "version": "1.0",
  "config": {
    "licenseType": "persistent",
    "keyId": "aaaaaaaa-0b0b-1c1c-2d2d-333333333333",
    "policies": {
      "playback": {
        "allowOffline": true
      }
    }
  }
}
```

### Rental License with Time Restrictions

```json
{
  "version": "1.0",
  "config": {
    "licenseType": "rental",
    "keyId": "bbbbbbbb-1c1c-2d2d-3e3e-444444444444",
    "policies": {
      "playback": {
        "expirationDate": "2024-12-31T23:59:59Z",
        "gracePeriod": 3600
      },
      "outputProtection": {
        "digital": "required",
        "analog": "optional"
      }
    }
  }
}
```

### Subscription License with Output Protection

```json
{
  "version": "1.0",
  "config": {
    "licenseType": "subscription",
    "keyId": "cccccccc-2d2d-3e3e-4f4f-555555555555",
    "policies": {
      "playback": {
        "allowOffline": false
      },
      "outputProtection": {
        "digital": "required",
        "analog": "required"
      },
      "subscription": {
        "renewalUrl": "https://subscription.service.com/renew",
        "validationInterval": "PT24H"
      }
    }
  }
}
```

## Usage in License Requests

### HTTP POST Request

Include the JSON configuration in the CustomData field:

```http
POST /pr/svc/rightsmanager.asmx HTTP/1.1
Host: playready.directtaps.net
Content-Type: application/octet-stream

[License Request with CustomData containing JSON configuration]
```

### Client Integration

#### JavaScript Example

```javascript
const customData = {
  version: "1.0",
  config: {
    licenseType: "persistent",
    keyId: keyId,
    policies: {
      playback: {
        allowOffline: true
      }
    }
  }
};

// Include in license request
const licenseRequest = {
  customData: JSON.stringify(customData),
  // ... other license request parameters
};
```

#### C# Example

```csharp
var customData = new {
    version = "1.0",
    config = new {
        licenseType = "persistent",
        keyId = keyId,
        policies = new {
            playback = new {
                allowOffline = true
            }
        }
    }
};

string jsonCustomData = JsonConvert.SerializeObject(customData);
// Include in PlayReady license request
```

## Advanced Features

### Conditional Access

Configure conditional access based on device or user attributes:

```json
{
  "conditionalAccess": {
    "deviceRestrictions": {
      "allowedDeviceTypes": ["mobile", "desktop"],
      "blockedDevices": ["emulator", "debugger"]
    },
    "geoRestrictions": {
      "allowedCountries": ["US", "CA", "GB"],
      "blockedRegions": ["region1", "region2"]
    }
  }
}
```

### Multi-Key Support

Support for multiple encryption keys:

```json
{
  "keys": [
    {
      "keyId": "key-1-guid",
      "contentKey": "base64-key-1",
      "keyType": "content"
    },
    {
      "keyId": "key-2-guid", 
      "contentKey": "base64-key-2",
      "keyType": "track"
    }
  ]
}
```

## Error Handling

### JSON Validation Errors

- **Malformed JSON**: HTTP 400 with JSON parsing error details
- **Missing Required Fields**: HTTP 400 with field validation errors
- **Invalid Field Values**: HTTP 400 with value constraint violations

### Configuration Errors

- **Unsupported License Type**: HTTP 400 with supported types list
- **Invalid Key Format**: HTTP 400 with key format requirements
- **Policy Conflicts**: HTTP 400 with policy resolution guidance

## Best Practices

1. **JSON Validation**: Validate JSON structure before sending requests
2. **Version Compatibility**: Use appropriate version for feature support
3. **Key Security**: Never expose content keys in client-side code
4. **Policy Testing**: Test different policy combinations thoroughly
5. **Error Handling**: Implement comprehensive error handling for all scenarios

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [Query String Syntax](query-string-syntax.md) - Simple URL-based configuration
- [Base64 JSON Syntax](base64-json-syntax.md) - Base64 encoded JSON format
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with CustomData JSON syntax:

1. Validate JSON format and structure
2. Check required field presence and values
3. Verify policy compatibility and constraints
4. Test with simplified configurations first
5. Review server response for detailed error information

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
