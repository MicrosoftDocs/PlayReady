---
title: Secure Stop Server for PlayReady Test Environment
description: Documentation for PlayReady secure stop test server functionality and endpoints
ms.topic: reference
ms.date: 06/30/2025
---

# Secure Stop Server for PlayReady Test Environment

## Overview

The PlayReady Secure Stop Server provides a test endpoint for validating secure stop functionality in PlayReady implementations. Secure Stop ensures that media consumption tracking data is securely transmitted from clients to content providers, enabling accurate usage monitoring and compliance reporting.

## Service Endpoint

The Secure Stop test server is available at:

```url
https://playready.directtaps.net/pr/svc/securestop.asmx
```

## Secure Stop Protocol

### Protocol Overview

Secure Stop enables clients to report session end information securely:

1. Client begins playback session
2. License specifies secure stop requirements
3. Client generates secure stop data during playback
4. At session end, client sends secure stop report to server
5. Server validates and acknowledges receipt

### Message Flow

```text
Client                    License Server           Secure Stop Server
  |                            |                           |
  |-- License Request -------->|                           |
  |<-- License Response -------|                           |
  |    (with SecureStop URL)   |                           |
  |                            |                           |
  |    [Playback Session]      |                           |
  |                            |                           |
  |-- Secure Stop Report ------|-------------------------->|
  |<-- Acknowledgment ---------|---------------------------|
```

## Server Configuration

### Secure Stop Requirements

Configure secure stop in license responses:

```json
{
  "licenseType": "persistent",
  "keyId": "key-id-guid",
  "secureStop": {
    "required": true,
    "serverUrl": "https://playready.directtaps.net/pr/svc/securestop.asmx",
    "reportingFrequency": "session-end",
    "customData": {
      "sessionId": "unique-session-identifier",
      "contentId": "content-identifier"
    }
  }
}
```

### Server Response Configuration

The server supports various response modes for testing:

```json
{
  "responseMode": "success|failure|timeout|partial",
  "acknowledgmentDelay": 0,
  "customData": {
    "testScenario": "normal-operation"
  }
}
```

## API Endpoints

### Submit Secure Stop Report

**Endpoint:** `POST /pr/svc/securestop.asmx/SubmitReport`

**Request Format:**

```http
POST /pr/svc/securestop.asmx/SubmitReport HTTP/1.1
Host: playready.directtaps.net
Content-Type: application/octet-stream

[Secure Stop Report Data - Binary Format]
```

**Response Format:**

```http
HTTP/1.1 200 OK
Content-Type: application/octet-stream

[Secure Stop Acknowledgment - Binary Format]
```

### Query Report Status

**Endpoint:** `GET /pr/svc/securestop.asmx/QueryStatus`

**Request Format:**

```http
GET /pr/svc/securestop.asmx/QueryStatus?sessionId=SESSION_ID HTTP/1.1
Host: playready.directtaps.net
```

**Response Format:**

```json
{
  "sessionId": "session-identifier",
  "status": "pending|received|processed|error",
  "timestamp": "2024-01-15T10:30:00Z",
  "reportSize": 1024,
  "processingTime": 50
}
```

## Testing Scenarios

### Basic Secure Stop Testing

Test normal secure stop flow:

```javascript
async function testBasicSecureStop() {
    // 1. Acquire license with secure stop requirement
    const license = await acquireLicense({
        keyId: 'test-key-id',
        secureStopRequired: true,
        secureStopUrl: 'https://playready.directtaps.net/pr/svc/securestop.asmx'
    });
    
    // 2. Simulate playback session
    const session = await startPlaybackSession(license);
    
    // 3. End session and generate secure stop report
    const secureStopReport = await endSessionWithSecureStop(session);
    
    // 4. Submit secure stop report
    const response = await submitSecureStopReport(secureStopReport);
    
    return response.acknowledged;
}
```

### Error Handling Testing

Test error scenarios:

```javascript
async function testSecureStopErrorHandling() {
    const testCases = [
        {
            name: 'Invalid Report Format',
            data: generateInvalidReport(),
            expectedError: 'INVALID_FORMAT'
        },
        {
            name: 'Expired Session',
            data: generateExpiredSessionReport(),
            expectedError: 'SESSION_EXPIRED'
        },
        {
            name: 'Duplicate Report',
            data: generateDuplicateReport(),
            expectedError: 'DUPLICATE_REPORT'
        }
    ];
    
    const results = [];
    for (const testCase of testCases) {
        try {
            await submitSecureStopReport(testCase.data);
            results.push({ test: testCase.name, result: 'UNEXPECTED_SUCCESS' });
        } catch (error) {
            results.push({ 
                test: testCase.name, 
                result: error.code === testCase.expectedError ? 'PASS' : 'FAIL' 
            });
        }
    }
    
    return results;
}
```

### Performance Testing

Test secure stop performance:

```javascript
async function testSecureStopPerformance() {
    const concurrentReports = 10;
    const reports = [];
    
    // Generate multiple secure stop reports
    for (let i = 0; i < concurrentReports; i++) {
        reports.push(generateSecureStopReport(`session-${i}`));
    }
    
    // Submit reports concurrently
    const startTime = Date.now();
    const promises = reports.map(report => submitSecureStopReport(report));
    const results = await Promise.allSettled(promises);
    const endTime = Date.now();
    
    return {
        totalTime: endTime - startTime,
        averageTime: (endTime - startTime) / concurrentReports,
        successCount: results.filter(r => r.status === 'fulfilled').length,
        errorCount: results.filter(r => r.status === 'rejected').length
    };
}
```

## Client Integration

### JavaScript Implementation

```javascript
class SecureStopClient {
    constructor(serverUrl) {
        this.serverUrl = serverUrl;
    }
    
    async submitReport(secureStopData) {
        const response = await fetch(`${this.serverUrl}/SubmitReport`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/octet-stream'
            },
            body: secureStopData
        });
        
        if (!response.ok) {
            throw new Error(`Secure stop submission failed: ${response.status}`);
        }
        
        return await response.arrayBuffer();
    }
    
    async queryStatus(sessionId) {
        const response = await fetch(`${this.serverUrl}/QueryStatus?sessionId=${sessionId}`);
        
        if (!response.ok) {
            throw new Error(`Status query failed: ${response.status}`);
        }
        
        return await response.json();
    }
}

// Usage
const secureStopClient = new SecureStopClient('https://playready.directtaps.net/pr/svc/securestop.asmx');
```

### C# Implementation

```csharp
public class SecureStopClient
{
    private readonly HttpClient httpClient;
    private readonly string serverUrl;
    
    public SecureStopClient(string serverUrl)
    {
        this.serverUrl = serverUrl;
        this.httpClient = new HttpClient();
    }
    
    public async Task<byte[]> SubmitReportAsync(byte[] secureStopData)
    {
        var content = new ByteArrayContent(secureStopData);
        content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
        
        var response = await httpClient.PostAsync($"{serverUrl}/SubmitReport", content);
        response.EnsureSuccessStatusCode();
        
        return await response.Content.ReadAsByteArrayAsync();
    }
    
    public async Task<SecureStopStatus> QueryStatusAsync(string sessionId)
    {
        var response = await httpClient.GetAsync($"{serverUrl}/QueryStatus?sessionId={sessionId}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        return JsonConvert.DeserializeObject<SecureStopStatus>(json);
    }
}
```

## Data Format

### Secure Stop Report Structure

The secure stop report contains:

- **Session Identifier**: Unique session ID
- **Content Identifier**: Content being consumed
- **Usage Data**: Playback duration, quality, etc.
- **Device Information**: Client device details
- **Timestamp Information**: Session start/end times
- **Digital Signature**: Cryptographic proof of authenticity

### Report Validation

The server validates reports for:

- **Format Integrity**: Correct binary structure
- **Digital Signature**: Cryptographic authenticity
- **Session Validity**: Valid session parameters
- **Timestamp Accuracy**: Reasonable time values
- **Duplicate Detection**: Prevention of duplicate submissions

## Advanced Features

### Custom Data Support

Include custom data in secure stop reports:

```json
{
  "customData": {
    "contentProvider": "test-provider",
    "userAgent": "PlayReady-Client/4.0",
    "playbackQuality": "HD",
    "geolocation": "US-WEST"
  }
}
```

### Batch Reporting

Submit multiple secure stop reports in a single request:

```javascript
async function submitBatchReports(reports) {
    const batchData = {
        reports: reports,
        batchId: generateBatchId(),
        timestamp: new Date().toISOString()
    };
    
    const response = await fetch(`${serverUrl}/SubmitBatch`, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json'
        },
        body: JSON.stringify(batchData)
    });
    
    return await response.json();
}
```

## Monitoring and Analytics

### Report Analytics

The test server provides analytics endpoints:

```http
GET /pr/svc/securestop.asmx/Analytics?period=24h
```

Response includes:

- Total reports received
- Average processing time
- Error rates by type
- Geographic distribution
- Client version statistics

### Health Monitoring

Monitor server health:

```javascript
async function checkSecureStopServerHealth() {
    const response = await fetch('https://playready.directtaps.net/pr/svc/securestop.asmx/Health');
    return await response.json();
}
```

## Best Practices

### Client Implementation

1. **Reliable Delivery**: Implement retry logic for failed submissions
2. **Offline Support**: Queue reports when network is unavailable
3. **Data Validation**: Validate report data before submission
4. **Error Handling**: Handle server errors gracefully
5. **Privacy**: Protect sensitive data in reports

### Testing Recommendations

1. **Comprehensive Scenarios**: Test normal and error conditions
2. **Performance Testing**: Validate under load conditions
3. **Network Conditions**: Test with various network scenarios
4. **Data Integrity**: Verify report data accuracy
5. **Security Testing**: Validate cryptographic components

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [Secure Delete Server](secure-delete-server.md) - Related secure functionality
- [Versioned Servers](versioned-servers.md) - Server version information
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with secure stop functionality:

1. Verify secure stop is enabled in license
2. Check report format and structure
3. Validate network connectivity to server
4. Review server response for error details
5. Test with simplified scenarios first

Common issues:

- **Report Format Errors**: Invalid binary format or structure
- **Signature Validation**: Cryptographic signature issues
- **Network Timeouts**: Server connectivity problems
- **Session Expiration**: Reports submitted too late

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
