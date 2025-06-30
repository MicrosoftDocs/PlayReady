# Query String Syntax for PlayReady Test Server

## Overview

The PlayReady Test Server supports query string syntax for license requests, providing a URL-based method for specifying license parameters. This approach allows developers to embed license configuration directly in the URL, making it easy to test different scenarios and configurations.

## Syntax Format

The query string syntax uses standard URL parameters to specify license requirements:

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=CONFIGURATION&kid=KEY_ID
```

## Supported Parameters

### Configuration Parameter (`cfg`)

The `cfg` parameter specifies the license configuration:

- **persistent**: Creates a persistent license that can be stored on the device
- **non-persistent**: Creates a temporary license that expires when the application closes
- **rental**: Creates a rental license with time-based restrictions
- **subscription**: Creates a subscription-based license

### Key ID Parameter (`kid`)

The `kid` parameter specifies the Key ID for content decryption:

- Must be a valid GUID format
- Corresponds to the content's encryption key identifier
- Used to match the license with the encrypted content

## Example URLs

### Basic Persistent License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=persistent&kid=12345678-1234-1234-1234-123456789012
```

### Non-Persistent License

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=non-persistent&kid=87654321-4321-4321-4321-210987654321
```

### Rental License with 48-hour expiration

```url
https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=rental&kid=12345678-1234-1234-1234-123456789012&expiry=48h
```

## Testing Scenarios

### Basic License Acquisition

1. Generate a license request using your PlayReady client
2. Construct the URL with appropriate parameters
3. Send an HTTP POST request to the constructed URL
4. Process the returned license response

### Different License Types

Test various license configurations by changing the `cfg` parameter:

- Test persistent vs. non-persistent behavior
- Verify rental expiration functionality
- Validate subscription-based access

## Error Handling

Common error scenarios and responses:

### Invalid Key ID

- **Error**: Malformed GUID in `kid` parameter
- **Response**: HTTP 400 Bad Request with error details

### Unsupported Configuration

- **Error**: Invalid value for `cfg` parameter
- **Response**: HTTP 400 Bad Request with supported values

### Missing Parameters

- **Error**: Required parameters not provided
- **Response**: HTTP 400 Bad Request with parameter requirements

## Best Practices

1. **URL Encoding**: Ensure proper URL encoding of parameter values
2. **HTTPS Usage**: Always use secure connections for license requests
3. **Parameter Validation**: Validate parameters before making requests
4. **Error Handling**: Implement robust error handling for various scenarios

## Integration Examples

### JavaScript/HTML5

```javascript
const licenseUrl = `https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=persistent&kid=${keyId}`;
// Use with your PlayReady implementation
```

### C# Application

```csharp
string licenseUrl = $"https://playready.directtaps.net/pr/svc/rightsmanager.asmx?cfg=persistent&kid={keyId}";
// Use with PlayReady SDK
```

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [CustomData JSON Syntax](customdata-json-syntax.md) - Alternative JSON-based approach
- [Base64 JSON Syntax](base64-json-syntax.md) - Base64 encoded configuration
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with query string syntax:

1. Verify parameter formatting and values
2. Check URL encoding of special characters
3. Validate Key ID format (GUID)
4. Test with different license configurations
5. Review server response for error details

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
