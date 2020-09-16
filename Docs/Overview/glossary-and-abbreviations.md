---
title: Glossary and Abbreviations
description: Contains a glossary of PlayReady terms and abbreviations.
ms.assetid: "07554286-539a-072a-14d9-81200b223c50"
keywords: glossary, playready
ms.date: 02/01/2018
ms.topic: conceptual


---


# Glossary and Abbreviations

The following high-level terms are used throughout this documentation.

| Term| Definition|
| --- | --- |
| 4K | This is generally defined as content with a resolution of 3840x2160. See also [Ultra-High Definition (UHD)](#ultrahigh). |
| AES | The Advanced Encryption Standard. Typically used to encrypt content protected by PlayReady. |
| AES 128 Content Key | Symmetric key used to encrypt and decrypt content using the AES algorithm with a key length of 128 bits (or 16 bytes), in either mode. |
| AES 128 CBC Content Key | Symmetric Key used to encrypt and decrypt content using the AES algorithm with a key length of 128 bits (or 16 bytes), in CBC mode. Consider the content key as the compound object { Key Value, ALGID }. |
| AES 128 CTR Content Key | Symmetric key used to encrypt and decrypt content using the AES algorithm with a key length of 128 bits (or 16 bytes), in CTR mode. Consider the content key as the compound object { Key Value, ALGID }. |
| AMS | Microsoft Azure Media Services. See https://azure.microsoft.com/en-us/services/media-services/. |
| AMS CP | The Content Protection (also known as DRM) functionality available in Microsoft Azure Media Services. See https://docs.microsoft.com/en-us/azure/media-services/media-services-content-protection-overview. |
| Anti-rollback clock| A process by which PlayReady detects whether a clock on the client has been reset to an earlier time by the user and triggers a rollback event. |
| Application Secrets | PlayReady stub library provided to Company and secrets, such as symmetric keys and private keys that reside in the application binary and/or in the process space of the application. |
| Attacker | Person trying to get unauthorized access to content or client secrets. In digital rights management (DRM), any user may be an attacker.|
| A/V Content | PlayReady audio and video content. |
| CA | Certificate Authority. An entity that issues digital certificates and provides trust in certificate chains. |
| CAS | Conditional Access System. |
| CBC mode | An AES encryption mode. Cipher Block Chaining (CBC) mode turns a block cipher into a stream cipher. |
| <a id="'cbcs'"></a>'cbcs' | One of the encryption modes of the Common Encryption standard. Uses the AES CBC mode with Stripped (partial) sample encryption. See also [Common Encryption (CENC)](#commencrypt). |
| CDM | See [Content Decryption Module](#contdecrypt). |
| CENC | See [Common Encryption (CENC)](#commencrypt). |
| <a id="cenc"></a>'cenc' | One of the encryption modes of the Common Encryption standard. Uses the AES CTR mode with full sample encryption. See also [Common Encryption (CENC)](#commencrypt). |
| Certificate | A digitally-signed binary document used to grant and revoke privileges to devices and computers to perform specific operations.|
| Certificate revocation list (CRL)| A list that maintains the information necessary to disable a device from being able to acquire licenses and play protected content.|
| Certificate Security Level (CSL) | The security value specified in the leafmost certificate in the certificate chain associated with a PlayReady Final Product. A PlayReady Final Product may consume only Content that has an associated License Security Level no greater than the PlayReady Final Product’s Certificate Security Level. |
| Challenge| A request from a client. A challenge contains information about the client, a list of requested rights, and other information about the content, including the content header and key identifier. |
| Clear content| A media file that is not encrypted.|
| Client | Content receiver. May be a device or an application.|
| CMAF | Common Media Application Format. A multimedia format specified in ISO/IEC 23000-19:2018. |
| <a id="commencrypt"></a>Common Encryption (CENC) | An MPEG Standard that defines encryption and container formats for protected media content specified in ISO/IEC 23001-7:2016 |
| Company Certificate | A Certificate unique to a Company issued by Microsoft for the purpose of issuing other Device/Model Certificates. |
| <a id="comply"></a>Compliance Rules | Compliance Rules specify the required behaviors of PlayReady implementations and the software accessing the implementations. Compliance Rules describe how content may be accessed and passed using specific policy rules. |
| <a id="contdecrypt"></a>Content Decryption Module (CDM) | The client component that provides the DRM functionality, including decryption. |
| Content (protected)| Videos, movies, audio, music, ebooks, executables. May be downloaded and/or streamed.|
| Content header| Part of the file structure of a PlayReady encrypted file that contains information necessary for a client to decrypt and render the content data. In a packaged file, a content header contains the key identifier, content key, license acquisition URL, and license user interface URL. This content header can also include attributes defined by the content provider.|
| Content Key | A symmetric key used to encrypt and decrypt Content. |
| Content Protection Functions | Functions related to protection of Content, including but not limited to authentication, encryption, decryption, Device Certificate signing, output protection, Metering, Secure Clock, Content revocation, key management, rights enforcement, or storing/updating information in the PlayReady Data Stores as such term is described and required in the Microsoft Implementation, to the extent such functions are implemented in a PlayReady Final Product. |
| CR | See [Compliance Rules](#comply). |
| CR&RR | Compliance and Robustness Rules.|
| Cryptographically Random | Unpredictable, in that no polynomial-time algorithm, given any sequence of bits, can guess the succeeding *K* bits with probability greater than ½^*K* + 1/*P*(*K*) for any (positive) polynomial *P* and sufficiently large *K*. |
| CBC mode | An AES encryption mode. Cipher Block Chaining (CBC) mode turns a block cipher into a stream cipher. |
| CTR mode | An AES encryption mode. Counter (CTR) mode turns a block cipher into a stream cipher. |
| Customer | Company that uses PlayReady to build a service or client.|
| DASH | See [MPEG-DASH](#mpegdash). |
| Decrypt | To convert encrypted content back into its original form. |
| Deployment certificate| An XML string used to ensure the Server is running a licensed copy of PlayReady Server SDK.|
| Device| Usually refers to a physical unit such as mobile phones, set-top boxes, and portable media players.|
| Device Secrets | Device Private Key, the private portion of the Fallback Keys, the private portion of the Device Model Keys, the Device Secret Key, the Certificate Signing Private Key, Certificate Signing Symmetric Key, Key File Protection Key and the private portion of the Domain Keys. |
| Digital rights management (DRM)| A technology that provides a persistent level of protection to digital content by encrypting it with a cryptographic key. Authorized recipients (or end users) must acquire a license to unlock and consume the content.|
| Domain (PlayReady domain)| A PlayReady entity that lets you manage content access for multiple clients. A PlayReady domain is not the same as network or Web domains.|
| Domain (CA) certificate| An XML string used to sign domain certificates issued to clients.|
| Domain controller| A PlayReady Server that manages domain membership. A domain controller determines what the domain represents (a user, a family, or a group of users, for example) and holds a list of entities that are associated with it.|
| DPK | PlayReady Device Porting Kit. |
| DRM | Digital Rights Management technology. PlayReady is the leading DRM. |
| DT | Defined Terms for PlayReady Compliance and Robustness Rules.|
| ECC | Elliptic curve cryptography.|
| Embedded License Store (ELS)| A record for storing embedded licenses.|
| EME | See [Encrypted Media Extensions](#eme). |
| Encrypt | To programmatically disguise content to hide its substance.|
| <a id="eme"></a>Encrypted Media Extensions (EME) | A W3C Standard for HTML interfaces that allow HTML5 applications to do DRM operations. See [https://www.w3.org/TR/encrypted-media/](https://www.w3.org/TR/encrypted-media/). |
| Enhanced Content Protection (ECP) | Content protection measures over and beyond those generally considered sufficient to obtain HD content in the past. |
| Extensible policies| License rights and restrictions added on to the existing extensible media rights (XMR) policy system to create special policies applicable to specific subsets of the PlayReady ecosystem. These policies are client enforced, and client implementors must elect to enable support for extensible policies.|
| <a id="xmr"></a>Extensible media rights (XMR)| A binary schema used for representing licenses within PlayReady.|
| Final Product | See [PFPL](#pfpl). |
| FPL | See [PFPL](#pfpl). |
| Full Ultra-High Definition Content (Full UHD) | UHD content with Full 4K resolution&mdash;4096 x 2160 pixels.  |
| Full Sample Encryption | See ['cenc'](#cenc).
| Hashed data store (HDS)| A file also know as a PlayReady data store, that contains all licenses, certificates, and related content access protection data associated with a particular client. This file is created by the PlayReady Client runtime when a device is first started and individualized.
| HLS | HTTP Live Streaming. An adaptive streaming protocol that was introduced by Apple. |
| IIS | See [Internet Information Services](#iis). |
| Initialization | The process of updating the PlayReady runtime on the client, allowing licenses to be bound to the client. This process increases security by making it difficult to corrupt more than one player at a time.|
| Integrated Circuit (IC) | A set of electronic circuits on one small plate ("chip") of semiconductor material, normally silicon. |
| <a id="iis"></a>Internet Information Services | Web Server created by Microsoft for use on Windows Server. |
| Intermediate Product | See [PIPL](#pipl). |
| IPL | See [PIPL](#pipl). |
| IV (Initialization Vector) | A block of bits enabling multiple instances of a stream or block cipher to produce unique streams despite using the same encryption key. |
| Key | A piece of data that is required to unlock a packaged media file. This key is included in a separate license.|
| Key Identifier (KID) | A value that identifies the key for a protected media file.|
| Key Rotation | A technique that seamlessly changes the encryption keys of a stream at specific times. PlayReady supports Scalable Licenses that allows implementation of very frequent and effective key rotation. |
| Leaf license | The element of a license chain that contains the content key and is bound to a root license. |
| License | Data attached to protected content that describes how the content can be used. A license is a data structure that contains, but is not limited to, policies and an encrypted content key. |
| License acquisition | The process of obtaining a license to play a packaged media file. The client attempts to obtain a license from a license acquisition URL, which is specified in the packaged media file.|
| License acquisition URL (LAURL) | The URL that points to the first Web page that appears in the license acquisition process. A license acquisition URL is included in each packaged media file; when a user tries to play a media file that is not licensed, the player opens the license acquisition URL to acquire a license.|
| License chain | A license for digital media content that is composed of connected elements that include a root license and one or more leaf licenses, each of which contains a subset of rights for the content.|
| License key seed | A shared secret value that is used to generate keys to encrypt media files.|
| License Integrity Key | A symmetric key used to verify that a License has not been tampered with. |
| Licenser/License Server | Function in the service back end that issues PlayReady licenses. Developed by the service based on the Microsoft PlayReady Server SDK.|
| License Store | An area on a device where licenses are stored. The License Store is usually a part of the hashed data store (HDS). |
| Metering | The process for counting the number of times content is played.|
| Metering aggregation service/Metering Server | A service that collects and processes metering data from clients. |
| Metering certificate | An XML string that contains the metering identifier and URL for a metering aggregation service. |
| Metering challenge | Metering data from a client, indicating how many times protected digital media files were used. The metering challenge is sent to a metering aggregation service by the client.|
| Metering identifier (MID) | The value that identifies the specific license for which content is being metered.|
| Metering response | A confirmation from a metering aggregation service that metering data was successfully reported by a client.|
| Metering Server | A computer that monitors the number of times an action has been performed on specific content.|
| Microsoft Implementation | The implementation of PlayReady Functionality provided to a Company as source code, binaries, technical documentation, tools, and/or sample files under the Company’s PlayReady Agreement. |
| <a id="mpegdash"></a>MPEG DASH | Dynamic Adaptive Streaming over HTTP. An adaptive streaming protocol which is an MPEG standard. |
| MSI installer| A Windows installer file.|
| NIST algorithms | Algorithms standardized by the National Institute of Standards and Technology of the United States of America. |
| ODM | Original Design Manufacturer. A company that designs and manufactures a product that is branded by another firm for sale. |
| OEM | Original Equipment Manufacturer. A company that produces devices using their own brand. |
| OS | Operating System. PlayReady is supported on all operating systems. |
| Output protection level (OPL)| A setting in a license that indicates which technologies can be used to play protected digital media content.|
| Packaging| The process by which clear content is encrypted to protect it from unlicensed use.|
| Partial Sample Encryption | See ['cbcs'](#cbcs).
| Partner | Company that resells products including PlayReady functionality to customers.|
| Personally Identifiable Information | Any information that can be used to identify, contact, or locate end users of PlayReady. |
| <a id="pipl"></a>PIPL, IPL | PlayReady Intermediate Product Licensee. A company that has signed a PlayReady Intermediate Product License with Microsoft. |
| <a id="pfpl"></a>PFPL, FPL | PlayReady Final Product Licensee. A company that has signed a PlayReady Final Product License with Microsoft. |
| Player | A client program or control that receives digital media content streamed from a Server or played from local files. Windows Media Player is an example of a player.|
| PK | PlayReady Device Porting Kit. |
| PlayReady CA | PlayReady Certificate Authority. Microsoft is the Certificate Authority for PlayReady Client and Server Certificates. |
| PlayReady Components | Components of a SL2000 or SL3000 qualified product that are subject to the PlayReady Compliance and Robustness Rules. |
| PlayReady Device Porting Kit| The portion of PlayReady content access and protection technology used for designing PlayReady applications for devices such as mobile phones, set-top boxes, and portable media players.|
| PlayReady Interface for Trusted Execution Environment (PRiTEE) | The PlayReady Interface for Trusted Execution Environments created using the PlayReady Device Porting Kit as described in the PlayReady Documentation.  |
| PlayReady Product | A PlayReady Final Product implementing any feature(s) or functionality(s) of the Device Porting Kit or a PlayReady Intermediate Product implementing a PlayReady Trusted Execution Environment. |
| PlayReady Server SDK| The portion of PlayReady content access and protection technology used for designing applications and plug-ins for use on a License Server, a Metering Server, a domain controller, a Secure Stop Server, and a Secure Delete Server.|
| PlayReady SL3000 Certificate | A Certificate provided by Microsoft for the purpose of enabling PlayReady Final Products to access PlayReady SL3000 Functionality. |
| PlayReady SL3000 Compliant Product | PlayReady Final Product that uses an SL3000 Conformant Intermediate Product and conforms to the SL3000 Compliance and Robustness Rules.  |
| PlayReady Trusted Execution Environment | A Trusted Execution Environment found on any computing device reporting a Certificate Security Level of 3000.  |
| Policy | The description in the license of the actions permitted or the restrictions on the content. |
| Private key| The secret half of a public/private key pair used in cryptography. Private keys are typically used to digitally sign a message that can be verified with the corresponding public key, or decrypt a message that has been encrypted with the corresponding public key.|
| Professional Software Tools | Professional tools, such as the software equivalent of in-circuit emulators, disassemblers, loaders, or patchers, implemented in software, such as would be used primarily by persons of professional skill and training, but not including either (i) professional tools or equipment that are made available on the basis of a non-disclosure agreement or (ii) Circumvention Tools. |
| Protect| To encrypt files with a key and add information such as the license acquisition URL.|
| Protected content| Videos, movies, audio, music, ebooks, executables. May be downloaded and/or streamed.|
| Protocol Secrets | All numerical, algorithmic and implementation secrets related to protocol execution. |
| 'pssh' box | Protection System Specific Header box. An object defined in the Common Encryption Standard that carries DRM-specific information. |
| Public key| The non-secret half of a public/private key pair used in cryptography. Public keys are typically used to encrypt sessions, files, and messages, which are then decrypted using the corresponding private key, or verify the digital signature of a message signed using the corresponding private key.|
| Restrictions| An attribute of a license that specifies the conditions under which a client cannot use a media file.|
| Revenue tracking| A process that logs the number of times a specific license is issued to play a media file.|
| Revocation| A process identifying clients that have compromised security, and preventing them from getting access to additional licenses for decrypting content that has been protected.|
| Revocation list| A list that contains all the application certificates of those client applications known to be damaged or corrupted. This list is included in licenses and then is stored on a user's device by the digital rights management (DRM) component of the client application.|
| Rights| An attribute of a license that specifies the conditions under which a client can use a media file.|
| Robustness| Rules that specify whether a specific device is sufficiently robust to resist attacks.|
| Robustness Rules | Robustness Rules specify different PlayReady assets and the levels of robustness required to protect each asset type. |
| Root license| The element of a license chain that is bound to a device and is required to decrypt the content key in the leaf license.|
| Root Public Key | A public key controlled by Microsoft that is trusted by PlayReady Final Products. |
| RR | Robustness Rules for PlayReady Products.|
| SDK| Software development kit.|
| Secrets | <b>Content secrets</b>: Content encryption key. <b>Client secrets</b>: Device unique private key, device PlayReady TEE key. |
| Secure Clock| A hardware clock that can only be set by specific routines&mdash;it cannot be set by the user.|
| Secure Code | Any code that is authorized to execute inside the [TEE](#tee).  |
| Secure Delete| The process by which service providers receive a secure acknowledgement when a persistent license is deleted by the application on the client.|
| Secure Stop| The process by which a client can confidently assert to a media streaming service that media playback has stopped for any given piece of content.|
| Service | Service that provides protected content to users.|
| Service provider | A Media, or Video, or Audio Service Provider is a  company that provides a media, video, or audio service to its subscribers or customers. An example is Netflix providing a video playback service to its users in exchange for a monthly subscription fee.|
| SL| Security Level.|
| SL2000 | PlayReady Security Level 2000. |
| SL3000 | PlayReady Security Level 3000. |
| SOAP | Simple Object Access Protocol. The protocol used by default between PlayReady Servers and clients. Payloads are XML carried over HTTP or HTTPS. |
| SOC | See [System on a Chip (Soc)](#soc). |
| SSTP | Smooth Streaming Transport Protocol. An adaptive streaming protocol that was introduced by Microsoft. |
| Standard Definition Content (SD) | Video with a resolution of 640x480. See High Definition and Ultra-High Definition. |
| Stream| Digital media that is in the process of being delivered in a continuous flow across a network.|
| Super distribution| A process by which users help to increase the distribution and sales of packaged files by sharing them with other users.|
| <a id="soc"></a>System on a Chip (SoC) | An integrated circuit (IC) that integrates all components of a computer or other electronic system into a single chip. It may contain digital, analog, mixed-signal, and often radio-frequency functions—all on a single chip substrate. |
| <a id="tee"></a>Trusted Execution Environment (TEE) | A hardware-enforced secure processing environment on a device that: (i) provides a Hardware Root of Trust, (ii) provides a Secure Boot process, (iii) runs only authenticated code that has been approved for use within the secure processing environment, (iv) provides for Secure Execution of PlayReady functionality, and (v) provides a Secure Media Pipeline and has a Certificate Security Level of 3000. |
| <a id="ultrahigh"></a>Ultra-High Definition Content (UHD) | Ultra-High Definition content. This is generally defined as content with a resolution of 3840x2160, that is, 4K content. However, this may also be used to include content with any of these following advanced features: Early-window content, Enhanced Chroma, Increased frame rate. |
| User| Person who consumes content from a service on a client. |
| UWP | Universal Windows Platform. |
| XMR| See [extensible media rights (XMR)](#xmr). |
