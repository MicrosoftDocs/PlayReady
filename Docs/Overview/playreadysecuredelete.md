---
author:
title: "PlayReady Secure Delete"
description: "The PlayReady Secure Delete feature allows service providers to receive secure acknowledgement when a persistent license is deleted by the app on the client."
ms.assetid: "012a9779-4bc0-450f-a1ec-ef93c9d25a8e"
kindex: license, Secure Delete
kindex: processing, Secure Delete
kindex: delete, secure
keywords: Secure Delete, Secure Delete license
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady Secure Delete


Introduced in PlayReady version 4.0, *PlayReady Secure Delete* is a feature that allows service providers to receive secure acknowledgement when a persistent license is deleted by the app on the client. Previously, when a license was deleted, service providers were not notified when deletion was completed. With PlayReady Secure Delete, the following operations are possible.

* Service providers can track which licenses are currently stored and which licenses have been deleted, on a given client machine.
* Service providers can issue a specific number of persistent licenses to a client, and track the count of licenses on that client’s machine.
* The Secure Delete feature also satisfies the [Encrypted Media Extensions (EME) specification](http://www.w3.org/TR/encrypted-media/){:target="_blank"} requirement as defined in September 2017, which specifies that a record of license deletion must be sent to the server upon license deletion.

## Secure Delete scenario

The following figure illustrates a Secure Delete flow.

![secure delete](playready_secure_delete.jpg){:width="75%"}

Before Secure Delete occurs, the app or client first instantiates a PlayReady Content Decryption Module (CDM) and acquires a persistent license from the server (Steps 1-7 in the figure above).

{::comment}
In the code below, `MediaKeys.createSession` returns a `MediaKeySession` object that represents a context for the message exchange with the CDM. The Key System is a decryption mechanism and/or content protection provider, represented as a reverse domain name. The value in this case is `com.microsoft.playready.recommendation`.

> ![](note.gif)**Note** Use the `com.microsoft.playready.recommendation.2000` or `com.microsoft.playready.recommendation.3000` to restrict access if your device must support either SL3000 or SL2000.

```cpp
requestMediaKeySystemAccess('com.microsoft.playready.recommendation')

...
// App creates a persistent license session.
var keySession = mediaKey.createSession("persistent-license");

// App generates a License Acquisition request.
keySession.generateRequest("keyids", initData);

// App gets the SessionId that the uniquely identifies the session.
var sessionId = keySession.sessionId;

// App gets back the license response, and updates.
keySession.update(licenseAcquisitionResponse);
```
{:/comment}
Next, PlayReady stores the license in the data store (HDS, Hashed Data Storage), along with a record of the license session blob, which is composed of a session identifier (SessionId) and one or more key identifiers (KIDs). When the app or client initiates a license deletion request, it will call the appropriate APIs {::comment}(`keySession.load` and `keySession.remove`) {:/comment}to remove the license(s) associated with the KID from the data store. During a non-Secure Delete license removal process, PlayReady removes the license(s) from the data store without further action. Using Secure Delete, PlayReady not only removes the license(s) associated with the KID from the data store, but also generates a Secure Delete challenge that contains the SessionId and KID(s) (Steps 12-13 in the figure above).

The app or client then sends the Secure Delete challenge to the Secure Delete server, which then processes the challenge{::comment} with a call to [ProcessDeleteLicenseData](processdeletelicensedatamethod.md){:/comment}. {::comment}The ProcessDeleteLicenseData method could for example, maintain a count of the licenses in the data store.{:/comment}

After processing the Secure Delete challenge, the Secure Delete server sends an un-encrypted, unsigned Secure Delete response that contains a base 64 encoded SessionId to the app (or client).

Finally, once the client receives the Secure Delete response, PlayReady validates that the SessionId contained in the Secure Delete response matches the SessionId that was used to generate the Secure Delete challenge. If the validation is successful, PlayReady removes the record of the license session from the data store.

{::comment}
```cpp
// App creates a persistent license session.
var keySession = mediaKey.createSession("persistent-license");

// App loads the persistent license session using the SessionId previously acquired.
keySession.load(sessionId);

// App removes the license. After this call, the App will receive a MediaKey event
// with the Secure Delete challenge.
keySession.remove();

// App feeds back the Secure Delete response retrieved from the server.
keySession.update(secureDeleteResponse)
```

## Secure Delete challenge example

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
               xmlns:xsd="http://www.w3.org/2001/XMLSchema"
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <ProcessDeleteLicenseData
      xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
      <challenge>
        <Challenge
          xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
          <DeleteLicenseData
            xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols"
            Id="SignedData">
            <Version>1</Version>
            <SessionID>BASE_64_ENCODED_SESSION_ID</SessionID>
            <KIDS>
              <KID>BASE_64_ENCODED_KID_1</KID>
              <KID>BASE_64_ENCODED_KID_2</KID>
              <KID>BASE_64_ENCODED_KID_3</KID>
            </KIDS>
            <EncryptedData
              xmlns="http://www.w3.org/2001/04/xmlenc#"
              Type="http://www.w3.org/2001/04/xmlenc#Element">
              <EncryptionMethod
                Algorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc">
              </EncryptionMethod>
              <KeyInfo
                xmlns="http://www.w3.org/2000/09/xmldsig#">
                <EncryptedKey
                  xmlns="http://www.w3.org/2001/04/xmlenc#">
                  <EncryptionMethod
                    Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecc256">
                  </EncryptionMethod>
                  <KeyInfo
                    xmlns="http://www.w3.org/2000/09/xmldsig#">
                    <KeyName>WMRMServer</KeyName>
                  </KeyInfo>
                  <CipherData>
                    <CipherValue>BASE_64_ENCODED_CIPHER_VALUE</CipherValue>
                  </CipherData>
                </EncryptedKey>
              </KeyInfo>
              <CipherData>
                <CipherValue>BASE_64_ENCODED_CIPHER_VALUE</CipherValue>
              </CipherData>
            </EncryptedData>
          </DeleteLicenseData>
          <Signature
            xmlns="http://www.w3.org/2000/09/xmldsig#">
            <SignedInfo
              xmlns="http://www.w3.org/2000/09/xmldsig#">
              <CanonicalizationMethod
                Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315">
              </CanonicalizationMethod>
              <SignatureMethod
                Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecdsa-sha256">
              </SignatureMethod>
              <Reference URI="#SignedData">
                <DigestMethod
                  Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#sha256">
                </DigestMethod>
                <DigestValue>BASE_64_ENCODED_DIGEST_VALUE</DigestValue>
              </Reference>
            </SignedInfo>
            <SignatureValue>BASE_64_ENCODED_SIGNATURE</SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <KeyValue>
                <ECCKeyValue>
                  <PublicKey>BASE_64_ENCODED_PUBLIC_KEY</PublicKey>
                </ECCKeyValue>
              </KeyValue>
            </KeyInfo>
          </Signature>
        </Challenge>
      </challenge>
    </ProcessDeleteLicenseData>
  </soap:Body>
</soap:Envelope>
```

## Secure Delete response example

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope
  xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <ProcessDeleteLicenseDataResponse
      xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
      <ProcessDeleteLicenseDataResult>
        <Response
          xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
          <DeleteLicenseResponse
            xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
            <Version>1</Version>
            <SessionID>BASE_64_ENCODED_SESSION_ID</SessionID>
          </DeleteLicenseResponse>
        </Response>
      </ProcessDeleteLicenseDataResult>
    </ProcessDeleteLicenseDataResponse>
  </soap:Body>
</soap:Envelope>
```

## See also

* [Creating a Device App Using the CDMi Interface](creatingadeviceappusingthecdmiinterface.md)
* [Secure Delete Server](securedeleteserver.md)
* [Secure Delete](securedeletedpk.md)
{:/comment}
