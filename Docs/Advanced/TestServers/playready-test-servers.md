---
title: PlayReady Test Servers
description: Documentation for PlayReady test servers and their various service configurations
author: Microsoft
ms.author: Microsoft
ms.date: 06/30/2025
ms.service: playready
ms.topic: reference
---

# PlayReady Test Servers

This section provides comprehensive documentation for Microsoft's PlayReady test servers, including various license server configurations, syntax options, and specialized services. These test servers are designed to help developers validate their PlayReady implementations across different scenarios and server configurations.

## Overview

The PlayReady test server infrastructure includes:

- **Main License Server** - Primary test server with multiple syntax options
- **Query String Syntax** - Modern recommended syntax for license parameters
- **JSON-based Syntaxes** - CustomData and Base64 JSON approaches
- **Legacy Syntax** - Backward compatibility support
- **Versioned Servers** - Different PlayReady Server SDK versions
- **Specialized Services** - Secure Stop and Secure Delete functionality

All test servers are publicly accessible and designed for development and testing purposes.

## Test Server Documentation

### Main License Server

The primary PlayReady test server with comprehensive configuration options and multiple syntax support.

- **[PlayReady Test Server Service](playready-test-server-service.md)**
  - Overview of the main test server
  - Test key seed configuration
  - Multiple syntax options
  - Rights and restrictions reference
  - Basic usage examples

### License Server Syntax Options

Detailed documentation for different ways to configure license parameters with the test server.

#### Query String Syntax (Recommended)

- **[Query String Syntax](query-string-syntax.md)**
  - Modern syntax introduced in 2017
  - JSON-like parameter format
  - Full PlayReady 3.X+ feature support
  - Multi-license scenarios
  - Comprehensive parameter reference

#### JSON-Based Syntaxes

- **[CustomData JSON Syntax](customdata-json-syntax.md)**
  - Pure JSON parameter format
  - Parameters in LicenseRequest.CustomData
  - Full feature support
  - Multi-license capabilities

- **[Base64 JSON Syntax](base64-json-syntax.md)**
  - Base64-encoded JSON parameters
  - Query string compatible
  - No client CustomData modification required
  - URL-safe parameter encoding

#### Legacy Support

- **[Legacy Syntax](legacy-syntax.md)**
  - Backward compatibility syntax
  - Inherited from playready.directtaps.net
  - Limited feature set
  - PlayReady 1.0-3.0 support

### Specialized Test Services

#### Version Compatibility Testing

- **[Versioned Servers](versioned-servers.md)**
  - Multiple PlayReady Server SDK versions
  - Interoperability testing
  - Version-specific behavior validation
  - Historical server configurations

#### Advanced Features Testing

- **[Secure Stop Server](secure-stop-server.md)**
  - PlayReady 3.0+ Secure Stop testing
  - Metering certificate workflow
  - License acquisition with Secure Stop
  - Challenge/response validation

- **[Secure Delete Server](secure-delete-server.md)**
  - PlayReady 4.0+ Secure Delete testing
  - EME remove() function testing
  - License deletion workflows
  - Client implementation validation

### Testing and Validation Tools

- **[Testing Output Protections](testing-output-protections.md)**
  - Complete output protection testing procedures
  - Compliance rules mapping
  - Protection level validation
  - Hardware security testing

- **[Testing Server Exceptions](testing-server-exceptions.md)**
  - Server exception simulation
  - Error handling validation
  - Domain exception testing
  - Client robustness testing

- **[Testing Client Info](testing-client-info.md)**
  - Client capability detection
  - Security level validation
  - Feature compatibility testing
  - Certificate chain analysis

### Documentation and Resources

- **[Documentation Links](documentation-links.md)**
  - Comprehensive PlayReady documentation resources
  - Official Microsoft documentation
  - Sample applications and code
  - Training materials and support

## Getting Started

### For Basic Testing

1. **Start with the [PlayReady Test Server Service](playready-test-server-service.md)** - Understand the main test server capabilities
2. **Use [Query String Syntax](query-string-syntax.md)** - Learn the recommended modern syntax
3. **Test basic scenarios** - Play rights, security levels, and expiration

### For Advanced Testing

1. **Multi-license scenarios** - Use JSON syntaxes for complex configurations
2. **Version compatibility** - Test with [Versioned Servers](versioned-servers.md)
3. **Advanced features** - Validate Secure Stop and Secure Delete functionality

### For Legacy Support

1. **Use [Legacy Syntax](legacy-syntax.md)** - For backward compatibility testing
2. **Version-specific testing** - Validate against older server SDK versions

## Common Server URLs

### Main Test Server

```http
http://test.playready.microsoft.com/service/rightsmanager.asmx
```

### Basic License Acquisition Examples

```http
# Simple license with default settings
http://test.playready.microsoft.com/service/rightsmanager.asmx

# License with specific security level
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(sl:3000)

# Multi-license scenario
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(kid:GUID1,sl:3000),(kid:GUID2,sl:2000)
```

### Specialized Services

```http
# Secure Stop testing
http://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(securestop:true)

# Versioned servers (example: PlayReady 2.0)
http://test.playready.microsoft.com/directtaps/svc/pr20/rightsmanager.asmx
```

## Key Features

### Test Key Seed

All servers use a common test key seed unless explicitly overridden:

```
Test Key Seed (Base64): "XVBovsmzhP9gRIZxWfFta3VVRPzVEWmJsazEJ46I"
```

### Supported Rights

- **Play Right** - Standard content playback
- **Copy Right** - Content copying permissions  
- **Execute Right** - Application execution rights
- **Read Right** - Data reading permissions

### Output Protection Levels

- **Security Levels** - 150, 2000, 3000
- **Audio OPL** - Compressed and uncompressed digital audio
- **Video OPL** - Compressed and uncompressed digital video
- **Analog OPL** - Analog video output protection

## Testing Guidelines

### Best Practices

1. **Start Simple** - Begin with basic Play rights and default settings
2. **Use Query String Syntax** - Leverage the modern recommended approach
3. **Test Incrementally** - Add complexity gradually
4. **Validate Responses** - Check license properties and restrictions
5. **Test Error Scenarios** - Validate error handling and edge cases

### Common Scenarios

1. **Basic Playback** - Simple Play right with default security level
2. **Persistent Licenses** - Licenses stored on client device
3. **Expiration Testing** - Time-based and usage-based restrictions
4. **Multi-Key Content** - Separate keys for audio and video
5. **Output Protection** - Various OPL configurations

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

- [PlayReady Test Content](../TestContent/playready-test-content.md)
- [PlayReady Features](../../Features/playready-features.md)
- [How to Test PlayReady Clients](../how-to-test-client-server-versions.md)
