---
title: Secure Delete Server for PlayReady Test Environment
description: Documentation for PlayReady secure delete test server functionality and endpoints
ms.topic: reference
ms.date: 06/30/2025
---

# Secure Delete Server for PlayReady Test Environment

## Overview

The PlayReady Secure Delete Server provides a test endpoint for validating secure delete functionality in PlayReady implementations. Secure Delete ensures that protected content and associated licenses can be securely removed from client devices when required, maintaining content protection and compliance requirements.

## Service Endpoint

The Secure Delete test server is available at:

```url
https://playready.directtaps.net/pr/svc/securedelete.asmx
```

## Secure Delete Protocol

### Protocol Overview

Secure Delete enables content providers to remotely trigger secure deletion of content and licenses:

1. Content provider determines deletion is required
2. Server generates secure delete command
3. Command is delivered to client device
4. Client validates and executes secure deletion
5. Client reports deletion completion to server

### Message Flow

```text
Content Provider       Secure Delete Server        Client Device
       |                        |                        |
       |-- Delete Request ----->|                        |
       |<-- Delete Command -----|                        |
       |                        |-- Push Command ------>|
       |                        |<-- Execution Report ---|
       |<-- Completion Report --|                        |
```

## Server Configuration

### Secure Delete Policy

Configure secure delete requirements in licenses:

```json
{
  "licenseType": "persistent",
  "keyId": "key-id-guid",
  "secureDelete": {
    "enabled": true,
    "serverUrl": "https://playready.directtaps.net/pr/svc/securedelete.asmx",
    "triggerMechanism": "remote|policy|expiration",
    "deletionScope": "license|content|both",
    "customData": {
      "contentId": "content-identifier",
      "policyId": "deletion-policy-id"
    }
  }
}
```

### Deletion Policies

Define various deletion scenarios:

```json
{
  "deletionPolicies": [
    {
      "policyId": "immediate-delete",
      "trigger": "remote-command",
      "scope": "both",
      "verification": "required"
    },
    {
      "policyId": "expiration-delete",
      "trigger": "license-expiration",
      "scope": "license",
      "gracePeriod": "PT24H"
    },
    {
      "policyId": "compliance-delete",
      "trigger": "compliance-violation",
      "scope": "content",
      "enforcement": "immediate"
    }
  ]
}
```

## API Endpoints

### Request Secure Delete

**Endpoint:** `POST /pr/svc/securedelete.asmx/RequestDelete`

**Request Format:**

```http
POST /pr/svc/securedelete.asmx/RequestDelete HTTP/1.1
Host: playready.directtaps.net
Content-Type: application/json

{
  "contentId": "content-identifier",
  "deviceId": "target-device-id",
  "deletionScope": "license|content|both",
  "reason": "expiration|violation|request",
  "immediateExecution": true
}
```

**Response Format:**

```json
{
  "deleteCommandId": "command-identifier",
  "status": "queued|sent|acknowledged|completed",
  "timestamp": "2024-01-15T10:30:00Z",
  "estimatedCompletion": "2024-01-15T10:35:00Z"
}
```

### Query Delete Status

**Endpoint:** `GET /pr/svc/securedelete.asmx/QueryStatus`

**Request Format:**

```http
GET /pr/svc/securedelete.asmx/QueryStatus?commandId=COMMAND_ID HTTP/1.1
Host: playready.directtaps.net
```

**Response Format:**

```json
{
  "commandId": "command-identifier",
  "status": "pending|in-progress|completed|failed",
  "progress": {
    "itemsToDelete": 5,
    "itemsDeleted": 3,
    "percentComplete": 60
  },
  "completionTime": "2024-01-15T10:35:00Z",
  "errorDetails": null
}
```

### Report Delete Completion

**Endpoint:** `POST /pr/svc/securedelete.asmx/ReportCompletion`

**Request Format:**

```http
POST /pr/svc/securedelete.asmx/ReportCompletion HTTP/1.1
Host: playready.directtaps.net
Content-Type: application/octet-stream

[Secure Delete Completion Report - Binary Format]
```

## Testing Scenarios

### Basic Secure Delete Testing

Test standard secure delete flow:

```javascript
async function testBasicSecureDelete() {
    // 1. Request secure delete for content
    const deleteRequest = {
        contentId: 'test-content-123',
        deviceId: 'test-device-456',
        deletionScope: 'both',
        reason: 'expiration',
        immediateExecution: true
    };
    
    const response = await requestSecureDelete(deleteRequest);
    
    // 2. Monitor deletion progress
    let status;
    do {
        await new Promise(resolve => setTimeout(resolve, 1000)); // Wait 1 second
        status = await queryDeleteStatus(response.deleteCommandId);
    } while (status.status === 'pending' || status.status === 'in-progress');
    
    return status.status === 'completed';
}
```

### Policy-Based Deletion Testing

Test different deletion policies:

```javascript
async function testPolicyBasedDeletion() {
    const policies = [
        {
            name: 'Immediate Delete',
            config: { trigger: 'remote-command', scope: 'both' }
        },
        {
            name: 'Expiration Delete',
            config: { trigger: 'license-expiration', scope: 'license' }
        },
        {
            name: 'Selective Delete',
            config: { trigger: 'compliance-violation', scope: 'content' }
        }
    ];
    
    const results = [];
    for (const policy of policies) {
        try {
            const result = await testDeletionPolicy(policy.config);
            results.push({ policy: policy.name, result: 'PASS' });
        } catch (error) {
            results.push({ policy: policy.name, result: 'FAIL', error: error.message });
        }
    }
    
    return results;
}
```

### Batch Deletion Testing

Test multiple content deletion:

```javascript
async function testBatchDeletion() {
    const contentItems = [
        'content-001',
        'content-002', 
        'content-003',
        'content-004',
        'content-005'
    ];
    
    // Request batch deletion
    const batchRequest = {
        contentIds: contentItems,
        deviceId: 'test-device-789',
        deletionScope: 'both',
        reason: 'batch-cleanup'
    };
    
    const response = await requestBatchDelete(batchRequest);
    
    // Monitor batch progress
    const finalStatus = await monitorBatchProgress(response.batchCommandId);
    
    return {
        totalItems: contentItems.length,
        successfulDeletions: finalStatus.progress.itemsDeleted,
        failedDeletions: finalStatus.progress.itemsToDelete - finalStatus.progress.itemsDeleted,
        completionTime: finalStatus.completionTime
    };
}
```

## Client Integration

### JavaScript Implementation

```javascript
class SecureDeleteClient {
    constructor(serverUrl) {
        this.serverUrl = serverUrl;
    }
    
    async requestDelete(deleteRequest) {
        const response = await fetch(`${this.serverUrl}/RequestDelete`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/json'
            },
            body: JSON.stringify(deleteRequest)
        });
        
        if (!response.ok) {
            throw new Error(`Delete request failed: ${response.status}`);
        }
        
        return await response.json();
    }
    
    async queryStatus(commandId) {
        const response = await fetch(`${this.serverUrl}/QueryStatus?commandId=${commandId}`);
        
        if (!response.ok) {
            throw new Error(`Status query failed: ${response.status}`);
        }
        
        return await response.json();
    }
    
    async reportCompletion(completionData) {
        const response = await fetch(`${this.serverUrl}/ReportCompletion`, {
            method: 'POST',
            headers: {
                'Content-Type': 'application/octet-stream'
            },
            body: completionData
        });
        
        return response.ok;
    }
}

// Usage
const secureDeleteClient = new SecureDeleteClient('https://playready.directtaps.net/pr/svc/securedelete.asmx');
```

### C# Implementation

```csharp
public class SecureDeleteClient
{
    private readonly HttpClient httpClient;
    private readonly string serverUrl;
    
    public SecureDeleteClient(string serverUrl)
    {
        this.serverUrl = serverUrl;
        this.httpClient = new HttpClient();
    }
    
    public async Task<DeleteResponse> RequestDeleteAsync(DeleteRequest request)
    {
        var json = JsonConvert.SerializeObject(request);
        var content = new StringContent(json, Encoding.UTF8, "application/json");
        
        var response = await httpClient.PostAsync($"{serverUrl}/RequestDelete", content);
        response.EnsureSuccessStatusCode();
        
        var responseJson = await response.Content.ReadAsStringAsync();
        return JsonConvert.DeserializeObject<DeleteResponse>(responseJson);
    }
    
    public async Task<DeleteStatus> QueryStatusAsync(string commandId)
    {
        var response = await httpClient.GetAsync($"{serverUrl}/QueryStatus?commandId={commandId}");
        response.EnsureSuccessStatusCode();
        
        var json = await response.Content.ReadAsStringAsync();
        return JsonConvert.DeserializeObject<DeleteStatus>(json);
    }
    
    public async Task<bool> ReportCompletionAsync(byte[] completionData)
    {
        var content = new ByteArrayContent(completionData);
        content.Headers.ContentType = new MediaTypeHeaderValue("application/octet-stream");
        
        var response = await httpClient.PostAsync($"{serverUrl}/ReportCompletion", content);
        return response.IsSuccessStatusCode;
    }
}
```

## Deletion Scopes

### License-Only Deletion

Remove only the license, keeping content:

```json
{
  "deletionScope": "license",
  "preserveContent": true,
  "licenseCleanup": {
    "removeFromStore": true,
    "clearCacheReferences": true,
    "revokeBindings": true
  }
}
```

### Content-Only Deletion

Remove content files while preserving license:

```json
{
  "deletionScope": "content",
  "preserveLicense": true,
  "contentCleanup": {
    "removeFiles": true,
    "clearTemporaryFiles": true,
    "cleanupMetadata": true
  }
}
```

### Complete Deletion

Remove both license and content:

```json
{
  "deletionScope": "both",
  "thoroughCleanup": true,
  "verification": {
    "confirmLicenseRemoval": true,
    "confirmContentRemoval": true,
    "verifyNoResidualData": true
  }
}
```

## Security Considerations

### Command Authentication

Secure delete commands must be authenticated:

```json
{
  "commandAuthentication": {
    "signature": "cryptographic-signature",
    "certificateChain": ["cert1", "cert2"],
    "timestamp": "2024-01-15T10:30:00Z",
    "nonce": "random-value"
  }
}
```

### Verification Requirements

Ensure secure deletion is properly executed:

```json
{
  "verificationRequirements": {
    "cryptographicProof": true,
    "overwriteVerification": true,
    "witnessReporting": true,
    "tamperDetection": true
  }
}
```

## Advanced Features

### Conditional Deletion

Configure conditional deletion triggers:

```json
{
  "conditionalDeletion": {
    "conditions": [
      {
        "type": "time-based",
        "trigger": "2024-12-31T23:59:59Z"
      },
      {
        "type": "usage-based",
        "trigger": "max-plays-exceeded"
      },
      {
        "type": "location-based",
        "trigger": "geographic-restriction"
      }
    ],
    "logicalOperator": "OR"
  }
}
```

### Rollback Capability

Support for deletion rollback (where possible):

```json
{
  "rollbackSupport": {
    "enabled": true,
    "retentionPeriod": "PT72H",
    "backupLocation": "secure-backup-store",
    "rollbackConditions": ["deletion-error", "false-positive"]
  }
}
```

## Monitoring and Reporting

### Deletion Analytics

Track secure delete operations:

```javascript
async function getDeletionAnalytics(period) {
    const response = await fetch(`${serverUrl}/Analytics?period=${period}`);
    return await response.json();
}

// Example response
{
  "period": "24h",
  "totalDeletions": 150,
  "successfulDeletions": 145,
  "failedDeletions": 5,
  "averageExecutionTime": "2.3s",
  "deletionReasons": {
    "expiration": 89,
    "violation": 12,
    "request": 49
  }
}
```

### Compliance Reporting

Generate compliance reports for auditing:

```javascript
async function generateComplianceReport(startDate, endDate) {
    const params = new URLSearchParams({
        startDate: startDate.toISOString(),
        endDate: endDate.toISOString(),
        format: 'detailed'
    });
    
    const response = await fetch(`${serverUrl}/ComplianceReport?${params}`);
    return await response.blob(); // Returns PDF report
}
```

## Best Practices

### Implementation Guidelines

1. **Verification**: Always verify deletion completion
2. **Logging**: Maintain detailed deletion logs
3. **Security**: Use strong authentication for delete commands
4. **Recovery**: Implement appropriate backup strategies
5. **Testing**: Thoroughly test deletion scenarios

### Performance Optimization

1. **Batch Operations**: Group related deletions
2. **Asynchronous Processing**: Use async deletion for large operations
3. **Resource Management**: Monitor system resources during deletion
4. **Scheduling**: Schedule deletions during low-usage periods

## Error Handling

### Common Error Scenarios

- **Authentication Failures**: Invalid or expired credentials
- **Content Not Found**: Specified content doesn't exist
- **Deletion Conflicts**: Content currently in use
- **System Errors**: Storage or network issues
- **Policy Violations**: Deletion not permitted by policy

### Error Recovery

```javascript
async function handleDeletionError(commandId, error) {
    switch (error.type) {
        case 'AUTHENTICATION_FAILED':
            // Refresh credentials and retry
            await refreshAuthToken();
            return await retryDeletion(commandId);
            
        case 'CONTENT_IN_USE':
            // Wait and retry
            await waitForContentRelease();
            return await retryDeletion(commandId);
            
        case 'SYSTEM_ERROR':
            // Log error and schedule retry
            await logSystemError(error);
            return await scheduleDeletionRetry(commandId);
            
        default:
            throw new Error(`Unhandled deletion error: ${error.message}`);
    }
}
```

## Related Documentation

- [PlayReady Test Server Service](playready-test-server-service.md) - Main service overview
- [Secure Stop Server](secure-stop-server.md) - Related secure functionality
- [Versioned Servers](versioned-servers.md) - Server version information
- [PlayReady Test Servers](playready-test-servers.md) - Complete server documentation

## Support and Troubleshooting

For issues with secure delete functionality:

1. Verify secure delete is enabled in license
2. Check deletion scope and policy configuration
3. Validate command authentication
4. Monitor deletion progress and status
5. Review error logs for specific issues

Common troubleshooting steps:

- Test with simplified deletion scenarios
- Verify network connectivity to server
- Check device permissions for content deletion
- Validate cryptographic signatures
- Review policy conflicts

For additional support, refer to the main [PlayReady Test Servers](playready-test-servers.md) documentation.
