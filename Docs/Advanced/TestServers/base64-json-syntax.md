---
title: Base64 JSON Syntax for PlayReady Test Server
description: Documentation for Base64 JSON syntax used in PlayReady test server license configuration
ms.topic: reference
ms.date: 06/30/2025
---

# Base64 JSON Syntax for PlayReady Test Server

## Overview

The PlayReady Test Server supports Base64 JSON syntax for license configuration, providing a compact and URL-safe method for embedding complex license parameters. This approach encodes JSON configuration data in Base64 format, making it suitable for URL parameters and HTTP headers.

## Encoding Process

The Base64 JSON syntax involves two steps:

1. Create a JSON configuration object
2. Encode the JSON string using Base64 encoding

```text
JSON Configuration → Base64 Encoding → URL Parameter
```

## Basic JSON Structure

Before encoding, create a JSON configuration:

```json
{
  "licenseType": "persistent",
  "keyId": "12345678-1234-1234-1234-123456789012",
  "outputProtection": {
    "digital": "required",
    "analog": "optional"
  }
}
```

## Base64 Encoding Examples

### Simple Configuration

**Original JSON:**

```json
{"licenseType": "persistent", "keyId": "12345678-1234-1234-1234-123456789012"}
```

**Base64 Encoded:**

```text
eyJsaWNlbnNlVHlwZSI6InBlcnNpc3RlbnQiLCJrZXlJZCI6IjEyMzQ1Njc4LTEyMzQtMTIzNC0xMjM0LTEyMzQ1Njc4OTAxMiJ9
```

### Complex Configuration

**Original JSON:**

```json
{
  "licenseType": "rental",
  "keyId": "87654321-4321-4321-4321-210987654321",
  "expirationDate": "2024-12-31T23:59:59Z",
  "outputProtection": {
    "digital": "required",
    "analog": "never"
  }
}
```

**Base64 Encoded:**

```text
eyJsaWNlbnNlVHlwZSI6InJlbnRhbCIsImtleUlkIjoiODc2NTQzMjEtNDMyMS00MzIxLTQzMjEtMjEwOTg3NjU0MzIxIiwiZXhwaXJhdGlvbkRhdGUiOiIyMDI0LTEyLTMxVDIzOjU5OjU5WiIsIm91dHB1dFByb3RlY3Rpb24iOnsiZGlnaXRhbCI6InJlcXVpcmVkIiwiYW5hbG9nIjoibmV2ZXIifX0=
```

## URL Usage

### Query Parameter Format

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data=BASE64_ENCODED_JSON
```

### Complete Example URLs

#### Persistent License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data=eyJsaWNlbnNlVHlwZSI6InBlcnNpc3RlbnQiLCJrZXlJZCI6IjEyMzQ1Njc4LTEyMzQtMTIzNC0xMjM0LTEyMzQ1Njc4OTAxMiJ9
```

#### Rental License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data=eyJsaWNlbnNlVHlwZSI6InJlbnRhbCIsImtleUlkIjoiODc2NTQzMjEtNDMyMS00MzIxLTQzMjEtMjEwOTg3NjU0MzIxIiwiZXhwaXJhdGlvbkRhdGUiOiIyMDI0LTEyLTMxVDIzOjU5OjU5WiJ9
```

## Configuration Options

### License Types

Support for all standard license types:

```json
{
  "licenseType": "persistent|non-persistent|rental|subscription"
}
```

### Output Protection Settings

Configure digital and analog output protection:

```json
{
  "outputProtection": {
    "digital": "required|optional|never",
    "analog": "required|optional|never",
    "hdcp": {
      "version": "1.4|2.0|2.1|2.2",
      "required": true
    }
  }
}
```

### Time-Based Restrictions

Set expiration and grace periods:

```json
{
  "expirationDate": "2024-12-31T23:59:59Z",
  "gracePeriod": 3600,
  "firstPlayExpiration": "PT48H"
}
```

## Implementation Examples

### JavaScript/HTML5

```javascript
// Create configuration object
const config = {
  licenseType: "persistent",
  keyId: keyId,
  outputProtection: {
    digital: "required",
    analog: "optional"
  }
};

// Convert to JSON and encode
const jsonString = JSON.stringify(config);
const base64Data = btoa(jsonString);

// Build URL
const licenseUrl = `https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data=${base64Data}`;
```

### C# Application

```csharp
using System;
using System.Text;
using Newtonsoft.Json;

// Create configuration object
var config = new {
    licenseType = "persistent",
    keyId = keyId,
    outputProtection = new {
        digital = "required",
        analog = "optional"
    }
};

// Convert to JSON and encode
string jsonString = JsonConvert.SerializeObject(config);
byte[] jsonBytes = Encoding.UTF8.GetBytes(jsonString);
string base64Data = Convert.ToBase64String(jsonBytes);

// Build URL
string licenseUrl = $"https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data={base64Data}";
```

### Python Example

```python
import json
import base64

# Create configuration dictionary
config = {
    "licenseType": "persistent",
    "keyId": key_id,
    "outputProtection": {
        "digital": "required",
        "analog": "optional"
    }
}

# Convert to JSON and encode
json_string = json.dumps(config)
base64_data = base64.b64encode(json_string.encode('utf-8')).decode('utf-8')

# Build URL
license_url = f"https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=base64&data={base64_data}"
```

## Advanced Configurations

### Multi-Track Content

Configuration for content with multiple tracks:

```json
{
  "licenseType": "persistent",
  "tracks": [
    {
      "keyId": "video-key-guid",
      "trackType": "video",
      "outputProtection": {
        "digital": "required"
      }
    },
    {
      "keyId": "audio-key-guid", 
      "trackType": "audio",
      "outputProtection": {
        "digital": "optional"
      }
    }
  ]
}
```

### Domain-Bound Licenses

Configuration for domain-bound content:

```json
{
  "licenseType": "persistent",
  "keyId": "domain-key-guid",
  "domainBinding": {
    "domainId": "domain-service-id",
    "domainAccountId": "account-identifier",
    "required": true
  }
}
```

## Testing and Validation

### Decoding Verification

To verify Base64 encoding:

```javascript
// Decode Base64 back to JSON
const decodedJson = atob(base64Data);
const configObject = JSON.parse(decodedJson);
console.log(configObject);
```

### Common Test Scenarios

1. **Basic License Types**: Test each license type individually
2. **Output Protection**: Verify different protection levels
3. **Time Restrictions**: Test expiration and grace periods
4. **Complex Configurations**: Test multi-track and domain scenarios

## Error Handling

### Encoding Errors

- **Invalid JSON**: Malformed JSON structure before encoding
- **Encoding Issues**: Character encoding problems during Base64 conversion
- **URL Safety**: Ensure proper URL encoding of Base64 data

### Server-Side Errors

- **Decoding Failures**: HTTP 400 with Base64 decoding error
- **JSON Parsing**: HTTP 400 with JSON structure errors
- **Configuration Invalid**: HTTP 400 with configuration validation errors

## Best Practices

1. **JSON Validation**: Validate JSON before encoding
2. **URL Encoding**: Properly encode Base64 data for URLs
3. **Size Limits**: Keep configurations reasonably sized for URL limits
4. **Testing**: Test encoding/decoding process thoroughly
5. **Error Handling**: Handle both encoding and server errors gracefully

## Advantages

- **Compact**: More compact than full JSON in URLs
- **URL Safe**: Base64 encoding is URL-safe
- **Flexible**: Supports complex configuration objects
- **Standard**: Uses standard Base64 encoding

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [CustomData JSON Syntax](customdata-json-syntax.md) - Full JSON configuration format
- [Query String Syntax](query-string-syntax.md) - Simple parameter-based approach
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with Base64 JSON syntax:

1. Verify JSON structure before encoding
2. Test Base64 encoding/decoding process
3. Check URL encoding of Base64 data
4. Validate configuration parameters
5. Review server error responses for details

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
