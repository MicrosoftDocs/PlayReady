---
author: 
title: "License Nonce"
description: ""
ms.assetid: "9F5227F8-83AD-4B6D-A4E3-B06183879629"
kindex: nonce, license
kindex: license, nonce
keywords: 
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# License Nonce
   
  
A PlayReady client includes a random **GUID** called the license nonce in every license request that it generates for a license server. {::comment}For example:{:/comment}

{::comment}
```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xmlns:xsd="http://www.w3.org/2001/XMLSchema" 
xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
  <soap:Body>
    <AcquireLicense xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
      <challenge>
        <Challenge xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
          <LA xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols" Id="SignedData" ml:space="preserve">
            <Version>1</Version>
            <ContentHeader>
              <WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.0.0.0">
                <DATA>
                  <PROTECTINFO>
                    <KEYLEN>16</KEYLEN>
                    <ALGID>AESCTR</ALGID>
                  </PROTECTINFO>
                  <KID>4Rplb+TbNES8tGkNFWTEHA==</KID>
                  <LA_URL>http://playready-testserver.azurewebsites.net/rightsmanager.asmx</LA_URL>
                  <LUI_URL>http://playready-estserver.azurewebsites.net/getrights.html</LUI_URL>
                </DATA>
              </WRMHEADER>
            </ContentHeader>
            <CLIENTINFO>
              <CLIENTVERSION>10.0.16384.10011</CLIENTVERSION>
            </CLIENTINFO>
            <RevocationLists>
              <RevListInfo>
                <ListID>ioydTlK2p0WXkWklprR5Hw==</ListID>
                <Version>11</Version>
              </RevListInfo>
              <RevListInfo>
                <ListID>gC4IKKPHsUCCVhnlttibJw==</ListID>
                <Version>11</Version>
              </RevListInfo>
              <RevListInfo>
                <ListID>Ef/RUojT3U6Ct2jqTCChbA==</ListID>
                <Version>34</Version>
              </RevListInfo>
              <RevListInfo>
                <ListID>BOZ1zT1UnEqfCf5tJOi/kA==</ListID>
                <Version>12</Version>
              </RevListInfo>
            </RevocationLists>
            <LicenseNonce>lojenZOMSu6K8OgsuUB7lA==</LicenseNonce>
            <ClientTime>1487020942</ClientTime>
            <EncryptedData xmlns="http://www.w3.org/2001/04/xmlenc#" Type="http://www.w3.org/2001/04/xmlenc#Element">
              <EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc"></EncryptionMethod>
              <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
                <EncryptedKey xmlns="http://www.w3.org/2001/04/xmlenc#">
                  <EncryptionMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecc256"></EncryptionMethod>
                  <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
                    <KeyName>WMRMServer</KeyName>
                  </KeyInfo>
                  <CipherData>
                    <CipherValue>2JQuE1S1bJmeEPzDbNMutlSAqQXYUgOhjIMiW11i5FDw9F4mIeWnyoWntA4F7DEL+g4DO+TldfSQro8P6BmnWVicNc+yI0SAeTgz8C/duFgfbm/EP2ApXemtsPkmSi4lfYA1n6+mOGaJ5ff+E+58lK+cBfc4pu5S47QYFUEubzk=</CipherValue>
                  </CipherData>
                </EncryptedKey>
              </KeyInfo>
              <CipherData>
                <CipherValue>xSloZkCcxKULbV72y/ZihWqnUxYwMtZMiFVMtDHvxcxAX9ksIHX5S9idIidPRqESytz7KjdsU/xQFUsllhegeFSxBeooK8Gh7hyBSdEGH+OHJc3LejN18nFqWkQqev7PBbWKfj5ke2Vgjir9kkiLxSuZyuj4EfJEdrV50AEcUhO4pU003iQOm3sqP9vqYDazCLRrXMWCImxgV6V2r8ykNwJ/s/uGiYEZuVOoE5kuK0nb3XiAOa0S4VH29//KlN1Dymlgn49V3wocZtUO4qqg=</CipherValue>
              </CipherData>
            </EncryptedData>
          </LA>
          <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
            <SignedInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"></CanonicalizationMethod>
              <SignatureMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecdsa-sha256"></SignatureMethod>
              <Reference URI="#SignedData">
                <DigestMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#sha256"></DigestMethod>
                <DigestValue>QF4icfarWi9bF61LlvS+AjvrTv4WB10C9hg9AFVxo5o=</DigestValue>
              </Reference>
            </SignedInfo>
            <SignatureValue>TgoCoi0FPKJsuPlOT5P2UEwWonfstM9FUagK5zGMSGvQk+T0ieyIqoOI6+6Rfhye0OtnzOFC1Ii4r+jGaRpCnw==</SignatureValue>
            <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <KeyValue>
                <ECCKeyValue>
                  <PublicKey>KhSCjNAz2d8IVZW3gk2jJG96orpXhVqwXxARo5tikjYY99ieZyP3IPztIS/bl9kGvJTxXaMA07K2Ph+8DLeCyg==</PublicKey>
                </ECCKeyValue>
              </KeyValue>
            </KeyInfo>
          </Signature>
        </Challenge>
      </challenge>
    </AcquireLicense>
  </soap:Body>
</soap:Envelope>
```
{:/comment}

If the server delivers a license response with only non-persistent licenses, it includes in the licenses a {::comment}<code>RightsId = LicenseRequest.LicenseNonce</code>{:/comment} rights identifier that contains the license request's license nonce. 

{::comment}
```xml
<GLOBAL_POLICY_CONTAINER>
    ...
    <RIGHTSID>lojenZOMSu6K8OgsuUB7lA==</RIGHTSID>
    ...
</GLOBAL_POLICY_CONTAINER>
```
{:/comment}

When adding the licenses received to the In-Memory-Only data store, the client verifies that {::comment}<code>license.RightsId == LicenseRequest.LicenseNonce</code>{:/comment}the license's rights identifier matches the license request's license nonce, and rejects the licenses that don't match.

This mechanism is designed for PlayReady robustness reasons, and avoids instances of an attacker replaying non-persistent licenses over and over to get an indefinite play right to a certain key identifier (KID).



{::comment}
> ![](note.gif)**Note** In case of multiple non-persistent licenses in a license response, PlayReady Server SDK applies the following pattern:
{::comment}>
{::comment}>     * First license's RIGHTSID = LicenseRequest.LicenseNonce
{::comment}>     * Second license's RIGHTSID = LicenseRequest.LicenseNonce + 1
{::comment}>     * Third license's RIGHTSID = LicenseRequest.LicenseNonce + 2
{::comment}>     * And so on.
{:/comment}

{::comment}For an SL2000 client, this check is done in the **DRM_NST_AddLicense** function, which returns DRM_E_NONCE_STORE_TOKEN_NOT_FOUND if the check fails. If the check fails for a valid license response, it means that the client is not well designed and did a check of <code>license.RIGHTSID</code> against an incorrect value of <code>LicenseRequest.LicenseNonce</code>. This should be considered a bug in the client.{:/comment}

If the server delivers a license response with at least one persistent license, it includes in the license response a license nonce{::comment} such as <code>LicenseResponse.LicenseNonce = LicenseRequest.LicenseNonce</code>{:/comment}. This mechanism is designed for device security reasons, to block an HDS-fill-DOS attack. This blocks an attacker from filling up the HDS by replaying a license response over and over again, which may lead to filling up the HDS, or even the memory (HDD, SSD, NAND Flash) if the device has no protection against HDS inflation, and make it inoperative.

{::comment}
Beginning with PlayReady Device Porting Kit v4.0, the Client has a REE verification that the license response is not replayed.

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
  <soap:Body>
    <AcquireLicenseResponse xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
      <AcquireLicenseResult>
        <Response xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
          <LicenseResponse xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols" Id="SignedData">
            <Version>1</Version>
            <Licenses>
              License>WE1SAAAAAAOEKFlh9h82lYAAQALAAAAHAABABDmRVkmRJjTAp4QotBfdIb/</License>
            </Licenses>
            <LicenseNonce>lojenZOMSu6K8OgsuUB7lA==</LicenseNonce>
            <ResponseID>vKWeGii4xuygdomgxUZYAo5/fdq/GYuShMSNwbmED9g=</ResponseID>
            <SigningCertificateChain>Q0hBSQAAAAEAAAOYAAAAAAAAAAJDRVJUAAAAAQAAAdQAAAFEAAEAAQAAAFgE13gX0W1OkNDHU88Gi4uuAAAAAAAAAAAAAAALw4Y+6q241UOlbEjtRilzOz2/k9LejX8Ms7Fw06/5+Q060QpP6xas=</SigningCertificateChain>
          </LicenseResponse>
          <Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
            <SignedInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
              <CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"></CanonicalizationMethod>
              <SignatureMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecdsa-sha256"></SignatureMethod>
              <Reference URI="#SignedData">
                <DigestMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#sha256"></DigestMethod>
                <DigestValue>lqZSFHELrOHvAfTRQyK3HiUy1PNoWJbOeaNsMR8PBtY=</DigestValue>
              </Reference>
            </SignedInfo>
            <SignatureValue>iixp2J5KbJT5mj0sK5Bqc3ZYpdUD3N8nvydrFhU46RFVHaCn7G/yZxrWKO8LFs/QgN/Gz/w5W7rhYDfPSg1+UA==</SignatureValue>
          </Signature>
        </Response>
      </AcquireLicenseResult>
    </AcquireLicenseResponse>
  </soap:Body>
</soap:Envelope>
```
{:/comment}
