---
author: dougklopfenstein
title: How to generate a PlayReady Header
description: This page describes how to generate a PlayReady Header in order to encrypt or package audio video content
ms.assetid: "D2F152D4-D0EC-4B32-9A50-A296670F4563"
keywords: PlayReady Header, PlayReady Object, Programming Guide
ms.author: rolefran
ms.date: 04/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# How to generate a PlayReady Header

The packager needs to include a PlayReady Header in the encrypted content.

For a detailed description of the PlayReady Header and the PlayReady Object, see the [PlayReady Header Specification](../Specifications/playready-header-specification.md).

The PlayReady Header contains information about the content being played back, including the key identifiers (KIDs) that identify the keys used to encrypt the data, the default license acquisition URL of the PlayReady License Server, and any custom data that you want to include. The key and KID used to encrypt the content must be shared with the PlayReady License Server that will be issuing the licenses for that specific content, typically through a Key Management System (KMS).

>[!NOTE]
>Microsoft does not provide a Key Management System with PlayReady.

Here is an example of a PlayReady Header, which may be inserted in the header of a segmented MP4 file, typically for On-Demand content. It includes the list of KIDs (the IDs of the content encryption keys) that are needed for a client to decrypt the content. It is the most common way to signal these KIDs for an On-Demand file or stream. 

```xml
<WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.3.0.0">
  <DATA>
    <PROTECTINFO>
      <KIDS>
        <KID ALGID="AESCTR" VALUE="PV1LM/VEVk+kEOB8qqcWDg=="></KID>
        <KID ALGID="AESCTR" VALUE="tuhDoKUN7EyxDPtMRNmhyA=="></KID>
      </KIDS>
    </PROTECTINFO>
    <LA_URL>http://rm.contoso.com/rightsmanager.asmx</LA_URL>
    <DS_ID>AH+03juKbUGbHl1V/QIwRA==</DS_ID>
  </DATA>
</WRMHEADER>
```

Here is an example of a PlayReady Header, for Live Linear content. It does not include any KID because the content encryption keys (and their associated KIDs) will change sometimes (for example, very frequently, or at program boundary, or every hour, or every day). The KIDs used for the content stream will be signalled in the segment headers, and it is not necessary to include any of them in the stream top level PlayReady Header. The property DECRYPTORSETUP is set to ONDEMAND, which means the PlayReady Header and Decryptor will be set on demand, meaning when the client will actually need to start decrypting a segment - and at this point, the client will have access to another PlayReady Header in the segment header to figure out what KID is involved. 

>[!NOTE]
>DECRYPTORSETUP = ONDEMAND does not mean the content is served On-Demand, it is actually the opposite.

```xml
<WRMHEADER version="4.2.0.0" xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader">
  <DATA>
    <DECRYPTORSETUP>ONDEMAND</DECRYPTORSETUP>
  </DATA>
</WRMHEADER>
```

There are multiple ways to create a PlayReady Header generator in your packager. The following sections describe, in general, how you can generate a PlayReady Header. 

## Method 1 - Build your own code based on the PlayReady Header Specification

The [PlayReady Object Specification](../Specifications/playready-header-specification.md) and [PlayReady Header Specification](../Specifications/playready-header-specification.md) are public so it is possible, and quite simple, to write code in your appliance or service that generates a PlayReady Object and a PlayReady Header, to package content.

The PlayReady Header generator needs to have input parameters such as: 

  * On Demand content or Live Linear content.
  * KID or list of KIDs that are used to protect the whole asset.
  * Encryption type used (AESCTR or AESCBC).
  * Defaut LA URL - the default URL of the PlayReady License Server that will be issuing licenses, if known at packaging time.
  * Default Domain Service Identifier, if the service is using domains.

You can now create the PlayReady Header. The following code sample demonstrates how to create a PlayReady Object that contains a PlayReady Header used for On-Demand content. 

# [C++](#tab/cpp)
```
// This function gets values from the key management system and your specified encryption mode
// (and optionally the domainID), creates a PlayReady Header, adds the header to a 
// PlayReady Object, and stores them in a file in UTF-16 little endian format

void buildRMObject(string KeyID1, string KeyID2, string encryptMode, string domainID)
{
	// The string parameters include the following:
	// KeyID1, KeyID2 - The key identifiers - these values are returned from the key management system or
	//                                        the KeySeed mechanism
	// encryptMode - the encryption mode used to encrypt content, can be AESCTR or AESCBC
	// domainID - the optional domain service identifier (only used for domains)

	string xmlString = "<WRMHEADER xmlns=\"http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader\" version=\"4.3.0.0\"><DATA><PROTECTINFO><KIDS><KID ALGID=\"";
	xmlString.append(encryptMode);
	xmlString.append("\" VALUE=\"");
	xmlString.append(KeyID1);
	xmlString.append("\"></KID><KID ALGID=\"");
	xmlString.append(encryptMode);
	xmlString.append("\" VALUE=\"");
	xmlString.append(KeyID2);
	xmlString.append("\"></KID></KIDS></PROTECTINFO><LA_URL>http://rm.contoso.com/rightsmanager.asmx</LA_URL><DS_ID>");
	xmlString.append(domainID);
	xmlString.append("</DS_ID></DATA></WRMHEADER>");

	// Convert the PlayReady header to UFT-16 format
	wstring_convert<codecvt_utf8_utf16<wchar_t>> convert;
	wstring utf16XML = convert.from_bytes(xmlString);

	// Calculate the length of the PlayReady Header
	int32_t headerLength = (utf16XML.size() * sizeof(wchar_t));
	// Calculate the length of the PlayReady Object
	int32_t objectLength = headerLength + 10;
	// Set the number of PlayReady object records (in this case, 1)
	int16_t recordCount = 1;
	// Set the record type (in this case, a PlayReady Header)
	// If this was an embedded license store, this value would be 3
	int16_t recordType = 1;

	// Write the PlayReady Object and PlayReady Header to a file
	wofstream wofs("C:\\Temp\\PRObject.txt", ios::binary);
	wofs.imbue(locale(wofs.getloc(),
			  new codecvt_utf16<wchar_t, 0x10ffff, little_endian>));
	wofs.write(reinterpret_cast<const wchar_t *>(&objectLength), 2);
	wofs.write(reinterpret_cast<const wchar_t *>(&recordCount), 1);
	wofs.write(reinterpret_cast<const wchar_t *>(&recordType), 1);
	wofs.write(reinterpret_cast<const wchar_t *>(&headerLength), 1);
	wofs <<  utf16XML;
}
```
# [C#](#tab/cs)
```
// This function gets values from the key management system and your specified encryption
// mode (and optionally the domainID), creates a PlayReady Header, adds the header to a 
// PlayReady Object, and stores them in a file in UTF-16 little endian format

public void buildRMHeader(string KeyID1, string KeyID2, string encryptMode, string domainID)
{
    // The string parameters are values include the following:
    // KeyID1, KeyID2 - The key identifiers - these values are returned from the key management
    //                                        system or the KeySeed mechanism
    // encryptMode - the encryption mode used to encrypt content, can be AESCTR or AESCBC
    // domainID - the optional domain service identifier (only used for domains)

    string prHeader;

    // Create the PlayReady Header
    prHeader = "<WRMHEADER xmlns=\"http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader\" version=\"4.3.0.0\"><DATA><PROTECTINFO><KIDS><KID ALGID=\"";
    prHeader += encryptMode;
    prHeader += "\" VALUE=\"";
    prHeader += KeyID1;
    prHeader += "\"></KID><KID ALGID=\"";
    prHeader += encryptMode;
    prHeader += "\" VALUE=\"";
    prHeader += KeyID2;
    prHeader += "\"></KID></KIDS></PROTECTINFO><LA_URL>http://rm.contoso.com/rightsmanager.asmx</LA_URL><DS_ID>";
    prHeader += domainID;
    prHeader += "</DS_ID></DATA></WRMHEADER>";

    // Convert the PlayReady Header to UTF-16 little endian
    byte[] headerBytes = System.Text.Encoding.Unicode.GetBytes(prHeader);

    // Calculate the length of the PlayReady Header
    Int16 headerLength = (short)headerBytes.Length;
    // Calculate the length of the  PlayReady Object
    Int32 proLength = headerLength + 10;
    // Set the number of PlayReady object records (in this case, 1)
    Int16 recordCount = 1;
	  // Set the record type (in this case, a PlayReady Header)
	  // If this was an embedded license store, this value would be 3
    Int16 recordType = 1;

    // Embed the PlayReady Header in the PlayReady Object
    byte[] pro = new byte[proLength];
    System.Buffer.BlockCopy(BitConverter.GetBytes(proLength), 0, pro, 0, 4);
    System.Buffer.BlockCopy(BitConverter.GetBytes(recordCount), 0, pro, 4, 2);
    System.Buffer.BlockCopy(BitConverter.GetBytes(recordType), 0, pro, 6, 2);
    System.Buffer.BlockCopy(BitConverter.GetBytes(headerLength), 0, pro, 8, 2);
    System.Buffer.BlockCopy(headerBytes, 0, pro, 10, headerLength);

    // Write the PlayReady Object to a file

    System.IO.File.WriteAllBytes("C:\\Temp\\PRObject.txt", pro);
}
```
---

## Method 2 - Use the PlayReady Server API

If you are a PlayReady Server SDK licensee, the server SDK contains the **PlayReadyHeader** class that can be used to construct a PlayReady Header. It includes methods you can use and properties you can fill in with the information required for a PlayReady Header. 

The **PlayReadyHeader** class is described in detail in the PlayReady documentation you receive with your PlayReady Server SDK license. The PlayReady Server SDK also includes a sample packager (AESPackaging) that demonstrates how to create a PlayReady Header.

As in Method 1, you will need the KeyID(s) that were generated by the key management system, the encryption type (AESCTR or AESCBC), the URL of the PlayReady license server,and optionally, the domain service identifier.  

## Method 3 - Use a Windows application

Things you need before you begin.
  1. You have to have the KeyID(s) that were generated by the key management system.
  2. You have to know the encryption type (AESCTR or AESCBC).
  3. Create the PlayReady header inside the PlayReady object using the Windows 10 PlayReadyHeaderContentHeader class.

As in the previous methods, you will need the KeyID(s) that were generated by the key management system, the encryption type (AESCTR or AESCBC), the URL of the PlayReady license server,and optionally the domain service identifier.

