---
title: "PlayReady Test License Server"
description: "Comprehensive documentation for the PlayReady Public Test License Server including syntax options, parameters, and usage examples."
ms.topic: reference
ms.date: 01/01/2018
---

# PlayReady Test License Server

The PlayReady Public Test Server available at `https://test.playready.microsoft.com/service/rightsmanager.asmx` unconditionally delivers to clients licenses with customizable rights and right restrictions, by providing parameters as arguments to the license request. The client can specify the rights requested in the returned license(s) by providing a set of parameters in the query string, or in the request headers. The PlayReady Public Test Server now supports multiple syntaxes to provide these parameters so testers can choose the one most appropriate to their case.

The recommended syntax is the **Query String Syntax**.

## Test Key Seed

Unless the LA URL includes a custom Key Seed to be used (e.g. by using the parameter `keyseed:VB8xp/ZsROLmaEu3Zyug4DH0r0MmA/tTcmFMBEqL`), the key seed used is the Test Key Seed given below:

**Test Key Seed (bytes):**

```c
{ 0x5D, 0x50, 0x68, 0xBE, 0xC9, 0xB3, 0x84, 0xFF, 0x60, 0x44, 0x86, 0x71, 0x59, 0xF1, 0x6D, 0x6B, 0x75, 0x55, 0x44, 0xFC, 0xD5, 0x11, 0x69, 0x89, 0xB1, 0xAC, 0xC4, 0x27, 0x8E, 0x88 }
```

**Test Key Seed (Base64):**

```text
"XVBovsmzhP9gRIZxWfFta3VVRPzVEWmJsazEJ46I"
```

## Supported Syntax Options

The PlayReady Test Server supports four different syntax options for specifying license parameters:

### 1. Query String Syntax (Recommended)

**Examples:**

- `https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(begindate:20151201,expiration:20171230)`
- `https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg=(kid:B6E39626-1CFB-4AA1-BCBD-4EF1ABA7843A,sl:3000),(kid:7C9484BA-C238-467A-869C-CDD8C7167712,sl:2000)`

**Features:**

- Similar to a JSON syntax (not real JSON though)
- Easy to read and edit
- Does not include unsafe characters (like ampersand) and should not require escaping any of them
- Note: the query string must not include any space characters (' ')
- Note: '+' characters are acceptable in the base64 encoded arguments
- Allows requests for multiple licenses in one license response, and set parameters for each of them
- Example: video track encrypted with one key set at SL3000, and audio track encrypted with another key set at SL2000
- New date time format yyyymmdd (example: 20171231) and allows set hours, minutes and seconds: yyyymmdd[hhmmss] (example: 20171231235959)

See the full documentation: [Query String Syntax](query-string-syntax.md)

### 2. CustomData JSON Syntax

**Example:**

```http
https://test.playready.microsoft.com/service/rightsmanager.asmx
```

with:

```json
CustomData = "json=[{'kid':'B6E39626-1CFB-4AA1-BCBD-4EF1ABA7843A','sl':'3000'},{'kid':'7C9484BA-C238-467A-869C-CDD8C7167712','sl':'2000'}]"
```

**Features:**

- Pure JSON syntax
- Allows requests for multiple licenses in one license response, and set parameters for each of them
- Allow all sorts of properties and combinations of rights and right restrictions
- Require the client to be able to insert data in LicenseRequest.CustomData

See the full documentation: [CustomData JSON Syntax](customdata-json-syntax.md)

### 3. Base64 JSON Syntax

**Example:**
```
https://test.playready.microsoft.com/service/rightsmanager.asmx?cfg64=W3sna2lkJzonQjZFMzk2MjYtMUNGQi00QUExLUJDQkQtNEVGMUFCQTc4NDNBJywnc2wnOiczMDAwJ30seydraWQnOic3Qzk0ODRCQS1DMjM4LTQ2N0EtODY5Qy1DREQ4QzcxNjc3MTInLCdzbCc6JzIwMDAnfV0=
```

**Features:**
- Pure JSON syntax
- Not that easy to read and edit though
- Does not include unsafe characters and should not require escaping any of them
- Allows requests for multiple licenses in one license response, and set parameters for each of them
- Allow all sorts of properties and combinations of rights and right restrictions
- Allows to insert customdata values in the query string
- Does not require the client to be able to insert data in LicenseRequest.CustomData
- Note: '+' characters are acceptable in the base64 encoded string

See the full documentation: [Base64 JSON Syntax](base64-json-syntax.md)

### 4. Legacy Syntax

**Example:**
```
https://test.playready.microsoft.com/service/rightsmanager.asmx?PlayRight=1&FirstPlayExpiration=60&UncompressedDigitalVideoOPL=270
```

**Features:**
- Inherited from and compatible with the previous test server hosted on `https://playready.directtaps.net/rightsmanager.asmx`
- The '&' character in the LA URL isn't well supported by XML parser, so for inclusion as a LA_URL value in a WRMHEADER (media file header or media stream header), you have to escape this character
- Example: `https://test.playready.microsoft.com/service/rightsmanager.asmx?PlayRight=1&amp;UseSimpleNonPersistentLicense=1`
- Limited possibilities (one license only)
- "US" date format: mm/dd/yyyy (example: 12/31/2017)

See the full documentation: [Legacy Syntax](legacy-syntax.md)

## Rights and Right Restrictions Reference

The full description of the rights and right restrictions is published in the [PlayReady Compliance and Robustness Rules](https://www.microsoft.com/playReady/licensing/compliance).

## Related Topics

- [PlayReady Test Servers Overview](playready-test-servers.md)
- [Query String Syntax](query-string-syntax.md)
- [CustomData JSON Syntax](customdata-json-syntax.md)
- [Base64 JSON Syntax](base64-json-syntax.md)
- [Legacy Syntax](legacy-syntax.md)
- [Versioned Servers](versioned-servers.md)
- [Secure Stop Server](secure-stop-server.md)
- [Secure Delete Server](secure-delete-server.md)
