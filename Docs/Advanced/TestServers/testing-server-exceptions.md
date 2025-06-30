# Testing Server Exceptions

## Overview

The PlayReady Test Server includes special functionality to programmatically trigger various server exceptions. This capability allows client developers to test how their devices and applications respond to different error conditions that may occur during license acquisition in production environments.

## Server Exception Testing

Client developers can use these server exception commands to validate error handling in their implementations. This includes testing scenarios such as device revocation, internal server errors, protocol mismatches, and domain-related exceptions.

### Transaction Example

Here's an example of how server exceptions work:

**Request URL:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c065)
```

**Server Response:**
```http
HTTP/1.1 500 Internal Server Error
Cache-Control: private
Content-Length: 764
Content-Type: text/xml; charset=utf-8

<?xml version="1.0" encoding="utf-8" ?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" 
               xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns:xsd="http://www.w3.org/2001/XMLSchema">
    <soap:Body>
        <soap:Fault>
            <faultcode>soap:Server</faultcode>
            <faultstring>
                System.Web.Services.Protocols.SoapException: Device Certificate Revoked.
                at Microsoft.Media.Drm.RightsManager.ConvertRmServerException(RMServerException ex)
                at Microsoft.Media.Drm.RightsManager.AcquireLicense(XmlDocument challenge)
            </faultstring>
            <faultactor>http://prtsprod-rightsmanager.azurewebsites.net/rightsmanager.asmx?cfg=(errorcode:0x8004c065)</faultactor>
            <detail>
                <Exception>
                    <StatusCode>0x8004c065</StatusCode>
                </Exception>
            </detail>
        </soap:Fault>
    </soap:Body>
</soap:Envelope>
```

## Exception Parameters

### Generic Exception Parameter

| Parameter | Description | Example URL |
|-----------|-------------|-------------|
| `errorcode:XXXXXXXX` | Request the server to respond with a specific exception | `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0xXXXXXXXX)` |

### Device and Client Exceptions

#### Device Certificate Revoked

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C065` | `DRM_E_DEVCERT_REVOKED` | Server cannot deliver a license to a revoked client device |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c065)
```

**Usage**: Test how client handles device revocation scenarios.

### Server Internal Exceptions

#### Internal Server Error

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C600` | `DRM_E_SERVER_INTERNAL_ERROR` | Server throws an internal server exception |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c600)
```

**Usage**: Test client resilience to server-side internal errors.

#### Invalid Message

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C601` | `DRM_E_SERVER_INVALID_MESSAGE` | The request sent to the server was invalid |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c601)
```

**Usage**: Test client handling of malformed request responses.

#### Protocol Version Mismatch

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C60B` | `DRM_E_SERVER_PROTOCOL_VERSION_MISMATCH` | The protocol version specified in the request was not supported by the server |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c60b)
```

**Usage**: Test client behavior with unsupported protocol versions.

#### Service Specific Exception

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C604` | `DRM_E_SERVER_SERVICE_SPECIFIC` | The server throws a service specific exception (typically from the license handler) |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c604)
```

**Usage**: Test client handling of service-specific errors.

### Protocol and Redirect Exceptions

#### Protocol Redirect

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C60D` | `DRM_E_SERVER_PROTOCOL_REDIRECT` | The protocol has a redirect |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c60d)
```

**Usage**: Test client handling of server redirects.

### Domain-Related Exceptions

#### Domain Required

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C605` | `DRM_E_SERVER_DOMAIN_REQUIRED` | Server received a standard license request from client and requires the client to join domain in order to receive a domain-bound license |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c605)
```

**Usage**: Test domain joining scenarios and client domain awareness.

#### Renew Domain

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C606` | `DRM_E_SERVER_RENEW_DOMAIN` | Server received a request from client with a domain certificate including an outdated domain version. Requires the client to update its domain certificate |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c606)
```

**Usage**: Test domain certificate renewal processes.

#### Device Limit Reached

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C602` | `DRM_E_SERVER_DEVICE_LIMIT_REACHED` | Server was willing to add client to a domain account but the account has already reached the limit of number of devices |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c602)
```

**Usage**: Test client handling of domain device limits.

#### Not a Domain Member

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C60A` | `DRM_E_SERVER_NOT_A_MEMBER` | Server received a valid domain bound license request from client, but client has been previously removed from domain by service |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c60a)
```

**Usage**: Test client behavior when removed from domain.

#### Unknown Account ID

| Parameter | Exception | Description |
|-----------|-----------|-------------|
| `errorcode:8004C60C` | `DRM_E_SERVER_UNKNOWN_ACCOUNTID` | Server received a domain bound license request from client for a certain account id, but this id is unknown to the service |

**Example:**
```url
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:0x8004c60c)
```

**Usage**: Test client handling of unknown domain account scenarios.

## Testing Scenarios

### Basic Exception Testing

```javascript
async function testServerExceptions() {
    const exceptions = [
        { name: 'Device Revoked', code: '0x8004c065' },
        { name: 'Internal Error', code: '0x8004c600' },
        { name: 'Invalid Message', code: '0x8004c601' },
        { name: 'Protocol Mismatch', code: '0x8004c60b' }
    ];
    
    const results = [];
    for (const exception of exceptions) {
        try {
            const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:${exception.code})`;
            const response = await testLicenseAcquisition(url);
            results.push({
                test: exception.name,
                result: 'UNEXPECTED_SUCCESS',
                error: 'Expected exception but got success'
            });
        } catch (error) {
            results.push({
                test: exception.name,
                result: 'EXPECTED_EXCEPTION',
                errorCode: error.statusCode,
                message: error.message
            });
        }
    }
    
    return results;
}
```

### Domain Exception Testing

```javascript
async function testDomainExceptions() {
    const domainExceptions = [
        { name: 'Domain Required', code: '0x8004c605' },
        { name: 'Renew Domain', code: '0x8004c606' },
        { name: 'Device Limit Reached', code: '0x8004c602' },
        { name: 'Not a Member', code: '0x8004c60a' },
        { name: 'Unknown Account', code: '0x8004c60c' }
    ];
    
    const results = [];
    for (const exception of domainExceptions) {
        try {
            const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:${exception.code})`;
            await testLicenseAcquisition(url);
            results.push({
                test: exception.name,
                result: 'FAIL',
                reason: 'Expected domain exception but got success'
            });
        } catch (error) {
            results.push({
                test: exception.name,
                result: 'PASS',
                exceptionType: exception.name,
                statusCode: error.statusCode
            });
        }
    }
    
    return results;
}
```

### Client Robustness Testing

```javascript
async function testClientRobustness() {
    // Test how client handles rapid exception scenarios
    const rapidTests = [
        '0x8004c065', // Device revoked
        '0x8004c600', // Internal error  
        '0x8004c601', // Invalid message
        '0x8004c60b'  // Protocol mismatch
    ];
    
    const startTime = Date.now();
    const promises = rapidTests.map(code => {
        const url = `http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(errorcode:${code})`;
        return testLicenseAcquisitionWithTimeout(url, 5000);
    });
    
    const results = await Promise.allSettled(promises);
    const endTime = Date.now();
    
    return {
        totalTime: endTime - startTime,
        results: results.map((result, index) => ({
            errorCode: rapidTests[index],
            status: result.status,
            handled: result.status === 'rejected' // We expect rejections
        }))
    };
}
```

## Client Implementation Guidelines

### Exception Handling Best Practices

```javascript
class PlayReadyExceptionHandler {
    handleLicenseAcquisitionError(error) {
        switch (error.statusCode) {
            case 0x8004C065: // Device revoked
                return this.handleDeviceRevoked();
                
            case 0x8004C600: // Internal server error
                return this.handleServerError(error);
                
            case 0x8004C601: // Invalid message
                return this.handleInvalidMessage(error);
                
            case 0x8004C60B: // Protocol version mismatch
                return this.handleProtocolMismatch(error);
                
            case 0x8004C605: // Domain required
                return this.handleDomainRequired(error);
                
            case 0x8004C606: // Renew domain
                return this.handleDomainRenewal(error);
                
            default:
                return this.handleUnknownError(error);
        }
    }
    
    handleDeviceRevoked() {
        // Device is revoked - cannot proceed
        throw new Error('Device has been revoked and cannot play protected content');
    }
    
    handleServerError(error) {
        // Retry with exponential backoff
        return this.retryWithBackoff(error.originalRequest);
    }
    
    handleDomainRequired(error) {
        // Initiate domain joining process
        return this.joinDomain(error.domainServiceUrl);
    }
    
    handleDomainRenewal(error) {
        // Renew domain certificate
        return this.renewDomainCertificate(error.domainServiceUrl);
    }
}
```

### C# Exception Handling

```csharp
public class PlayReadyExceptionHandler
{
    public async Task<bool> HandleLicenseException(Exception ex)
    {
        if (ex is SoapException soapEx)
        {
            var statusCode = ExtractStatusCode(soapEx);
            
            switch (statusCode)
            {
                case 0x8004C065: // Device revoked
                    return HandleDeviceRevoked();
                    
                case 0x8004C600: // Internal server error
                    return await HandleServerError(soapEx);
                    
                case 0x8004C605: // Domain required
                    return await HandleDomainRequired(soapEx);
                    
                case 0x8004C606: // Renew domain
                    return await HandleDomainRenewal(soapEx);
                    
                default:
                    return HandleUnknownError(soapEx);
            }
        }
        
        return false;
    }
    
    private uint ExtractStatusCode(SoapException soapEx)
    {
        // Extract status code from SOAP fault detail
        var detail = soapEx.Detail;
        var statusNode = detail?.SelectSingleNode("//StatusCode");
        
        if (statusNode != null && uint.TryParse(statusNode.InnerText.Replace("0x", ""), 
            NumberStyles.HexNumber, null, out uint statusCode))
        {
            return statusCode;
        }
        
        return 0;
    }
}
```

## Validation and Testing

### Expected Behaviors

When testing with server exceptions, validate that your client:

1. **Properly Parses Exceptions** - Correctly extracts error codes and messages
2. **Handles Gracefully** - Doesn't crash or hang on exceptions
3. **Provides User Feedback** - Shows appropriate error messages to users
4. **Implements Retry Logic** - Retries appropriate errors with backoff
5. **Supports Domain Operations** - Handles domain-related exceptions correctly

### Test Validation Checklist

- [ ] Client correctly identifies exception types
- [ ] Appropriate user messages are displayed
- [ ] Client doesn't crash on any exception type
- [ ] Retry logic works for recoverable errors
- [ ] Domain joining/renewal processes are triggered correctly
- [ ] Device revocation is handled securely
- [ ] Performance remains acceptable under error conditions

## Best Practices

### Client Development

1. **Comprehensive Error Handling** - Handle all documented exception types
2. **User Experience** - Provide clear, actionable error messages
3. **Retry Strategy** - Implement appropriate retry logic for transient errors
4. **Security** - Ensure device revocation prevents content access
5. **Testing** - Test all exception scenarios during development

### Error Recovery

1. **Graceful Degradation** - Continue operation when possible
2. **Clear Communication** - Inform users of issues and solutions
3. **Automatic Recovery** - Attempt automatic resolution where appropriate
4. **Fallback Options** - Provide alternative content or services
5. **Logging** - Log exceptions for debugging and analytics

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main test server functionality
- [Query String Syntax](query-string-syntax.md) - Parameter syntax reference
- [Testing Output Protections](testing-output-protections.md) - Output protection testing
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

© Microsoft Corporation. All rights reserved. [Trademarks](https://go.microsoft.com/fwlink/?LinkID=623755) | [Privacy](https://privacy.microsoft.com/)
