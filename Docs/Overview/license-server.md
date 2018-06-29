---
author: rolandlefranc
title: PlayReady License Server
description: The process of obtaining a license to play back PlayReady protected content is handled by a PlayReady License Server.
ms.assetid: "57039377-25D5-4F70-97C8-E62E47DC75CE"
keywords: PlayReady License Server
ms.author: rolefran
ms.date: 02/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# PlayReady License Server


The process of obtaining a license to play back PlayReady protected content is handled by a PlayReady License Server. The PlayReady Server contains the handler that authorizes playback of PlayReady protected client. It does this by providing the encryption key that unlocks the encrypted content that the client requests to play. In addition, the PlayReady License Server response contains the rights and rights restrictions for that content.

The following figure shows the steps that describe how a client gets a license from a PlayReady license service.

![Video Service Architecture](../images/video_service_arch.png)

  1.  The client obtains media to be played back.
  2.  The client initiates a license request from the PlayReady license service. The client can either proactively request the license before playing back the content, or reactively request the license once it discovers a license is required after playback begins.
  3.  The PlayReady License Server receives the request from the client and processes the license request.
  4.  The PlayReady License Server sends the response to the request back to the client. The license response will contain the key to unlock the encrypted media, along with a set of rights and rights restrictions that specify exactly what can be played back.
  5.  The client receives the license response, parses the rights and rights restrictions, and begins playback.

## Development and Deployment of a PlayReady License Server

You are not required to develop and deploy your own PlayReady license service. You can obtain these services from a third party, such as a [PlayReady Partner](https://www.microsoft.com/playready/partners/). However, if you do decide to develop your own PlayReady license service, Microsoft provides the PlayReady Server Software Development Kit (SDK) free of charge to those who want to program their own PlayReady License Server. Note that a PlayReady License Server only runs on Windows Server.

A PlayReady License Server can be developed and deployed in numerous ways:

  *  Develop the License Server yourself or through a third party.
  *  Operate the License Server yourself or through an application service provider (ASP).
  *  Deploy on a physical Server or a virtual Server.
  *  Deploy on the premises, in a private cloud, or in a public cloud.

PlayReady Server SDK provides the following functionality for License Servers:

  *  Technology integrates on any network infrastructure (proxies and so on).
  *  Technology integrates with any web service or logic.
  *  Delivered as Windows Server libraries, plus C# code in the SDK. Includes sample handlers in source code.

## Samples

The following is a license request sample:

```XML
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
	<soap:Body>
		<AcquireLicense xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
			<challenge>
				<Challenge xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
					<LA xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols" Id="SignedData" xml:space="preserve">
						<Version>1</Version>
						<ContentHeader>
							<WRMHEADER xmlns="http://schemas.microsoft.com/DRM/2007/03/PlayReadyHeader" version="4.0.0.0">
								<DATA>
									<PROTECTINFO>
										<KEYLEN>16</KEYLEN>
										<ALGID>AESCTR</ALGID>
									</PROTECTINFO>
									<KID>jADgM0TEcEeYmaMh4HndNg==</KID>
								</DATA>
							</WRMHEADER>
						</ContentHeader>
						<CLIENTINFO>
							<CLIENTVERSION>3.1.0.1017</CLIENTVERSION>
						</CLIENTINFO>
						<RevocationLists>
							<RevListInfo><ListID>ioydTlK2p0WXkWklprR5Hw==</ListID><Version>0</Version></RevListInfo>
							<RevListInfo><ListID>gC4IKKPHsUCCVhnlttibJw==</ListID><Version>0</Version></RevListInfo>
							<RevListInfo><ListID>Ef/RUojT3U6Ct2jqTCChbA==</ListID><Version>0</Version></RevListInfo>
							<RevListInfo><ListID>BOZ1zT1UnEqfCf5tJOi/kA==</ListID><Version>0</Version></RevListInfo>
						</RevocationLists>
						<CustomData>User=Roland</CustomData>
						<LicenseNonce>7GYVLC7wvGVR0nqGYXs4DQ==</LicenseNonce>
						<ClientTime>1446224160</ClientTime>
						<EncryptedData xmlns="http://www.w3.org/2001/04/xmlenc#" Type="http://www.w3.org/2001/04/xmlenc#Element">
							<EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes128-cbc"></EncryptionMethod>
							<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
								<EncryptedKey xmlns="http://www.w3.org/2001/04/xmlenc#">
									<EncryptionMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecc256"></EncryptionMethod>
									<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
										<KeyName>WMRMServer</KeyName>
									</KeyInfo>
									<CipherData>
										<CipherValue>Yt2ys5Fp83ayPvva8kT2THtEGze5se5YWaP======</CipherValue>
									</CipherData>
								</EncryptedKey>
							</KeyInfo>
							<CipherData>
							<CipherValue>uLdvYtc5oRk/MD0Dy72ZKH8PuHRI2RBzygKJHGu/M4boyiPOpMQnNlFB30qADHzND7fDwSfZGbOgP/g9OaT1LYDWHU/vq7f0CtiWddtwDSleb651HyQYOmWCcBSY9SVrjXXKITMsQL8PBXQh3O90GZSzS3UKo8OcyhO/yCmTsVWs0EYE98ikWjaPJfoQdvjSfklLjeveqGHhY7YZiSDMTksguLIMycsSTbGelL0P6IIDL7dj===========</CipherValue>
							</CipherData>
						</EncryptedData>
					</LA>
					<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
						<SignedInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
							<CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"></CanonicalizationMethod>
							<SignatureMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecdsa-sha256"></SignatureMethod>
							<Reference URI="#SignedData">
								<DigestMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#sha256"></DigestMethod>
								<DigestValue>NnkxTbC9yLGwYWSRfOz3VqKRYd62AGqTnwpSHsCklhI=</DigestValue>
							</Reference>
						</SignedInfo>
						<SignatureValue>Av2+yCEBdJD9+euMzGzuPb5rYgPlXNszEEr+cF7LwbE/Kln1e8JyhAEdIy14z4U43/oQMvMg40QaOAqv3ElM2g==</SignatureValue>
						<KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
							<KeyValue>
								<ECCKeyValue>
									<PublicKey>nrZWFO4ExmBomY+Xu5sATbSRi+tjRqMC+bVaKwn5ZAkdoER3nn8eE+yxXA0CkuhhmAmAqYDX7RY2q+MbAvoZuA==</PublicKey>
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

&nbsp;

The following is a license response sample:

```xml
<?xml version="1.0" encoding="utf-8"?>
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<soap:Body>
		<AcquireLicenseResponse xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols">
			<AcquireLicenseResult>
				<Response xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols/messages">
					<LicenseResponse xmlns="http://schemas.microsoft.com/DRM/2007/03/protocols" Id="SignedData">
						<Version>1</Version>
						<Licenses>
							<License>WE1SAAAAAANryW57jI0QQJItXt7rxagIAAMAAQAAAWIAAgAEAAAACAADAAIAAABEAAEAEgAAABAAAAAAVjOhZgAAABMAAAAMVjOhKgABADIAAAAMAAAAHgABADQAAAAKB9AAAAAzAAAACgABAAMACQAAAPIAAQAKAAAAnowA4DNExHBHmJmjIeB53TYAAQADAIAKFe+fsiOCUo/ndSfV1p0YK1qzUAgypRhiMUObPbmJ+P3GMFziaM+O0jHVttk0TAxxGsreh3PumUKJJ1CYMCYGJSgFm7ceuCsOxRBKCJcH+jGVlocmKMw0zrG41DeTrgDLw/rDDEDtmQvIwezIcwUwqWFxq7o5+kYWA4TdwTZNRAAAACoAAABMAAEAQOSjiOqgw3D8yP0vsKUOkh9SDIb3OghTm5812xCi7Y1q+Yr2U6KPQAUDgandzhhSKvebDjmWCIhxcjv+cIE5WIsAAQALAAAAHAABABBDCGMQnJ3JfqzT5K+5nS5k</License>
						</Licenses>
						<RevInfo>
							<Revocation>
								<ListID>ioydTlK2p0WXkWklprR5Hw==</ListID>
								<ListData>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</ListData>
							</Revocation>
							<Revocation>
								<ListID>gC4IKKPHsUCCVhnlttibJw==</ListID>
								<ListData>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</ListData>
							</Revocation>
							<Revocation>
								<ListID>Ef/RUojT3U6Ct2jqTCChbA==</ListID>
								<ListData>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</ListData>
							</Revocation>
							<Revocation>
								<ListID>BOZ1zT1UnEqfCf5tJOi/kA==</ListID>
								<ListData>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</ListData>
							</Revocation>
						</RevInfo>
						<Acknowledgement>
							<TransactionID>265e4a30-72f9-4f46-b41e-102a21ac4bc9</TransactionID>
						</Acknowledgement>
						<LicenseNonce>7GYVLC7wvGVR0nqGYXs4DQ==</LicenseNonce>
						<ResponseID>8qXNFxP4rrn+Rkx3rFTDYQZnfLMkJOm04N2JjWIXZ90=</ResponseID>
						<SigningCertificateChain>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA</SigningCertificateChain>
					</LicenseResponse>
					<Signature xmlns="http://www.w3.org/2000/09/xmldsig#">
						<SignedInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
							<CanonicalizationMethod Algorithm="http://www.w3.org/TR/2001/REC-xml-c14n-20010315"></CanonicalizationMethod>
							<SignatureMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#ecdsa-sha256"></SignatureMethod>
							<Reference URI="#SignedData">
								<DigestMethod Algorithm="http://schemas.microsoft.com/DRM/2007/03/protocols#sha256"></DigestMethod>
								<DigestValue>H9QaFwGEr4BnkJX0nRoztartIba7dcvEU5G1vYu9jTs=</DigestValue>
							</Reference>
						</SignedInfo>
						<SignatureValue>IVN3sGMpJ+O/3c1eLXRpEi1s7EuRGDLG/hLLdbLvHq7g/vzKEzw0NH0eB5MUiYuD9HaZlYZVbNGxaX74qed+Hw==</SignatureValue>
					</Signature>
				</Response>
			</AcquireLicenseResult>
		</AcquireLicenseResponse>
	</soap:Body>
</soap:Envelope>
```

## See also
[PlayReady Test Server](http://test.playready.microsoft.com/)