---

title: PlayReady Content Encryption
description: This topic provides an overview of the encryption algorithms used to protect content in the PlayReady ecosystem.
ms.assetid: "002abfe2-5478-33da-9fd9-6a1b28f24cdd"
keywords:  PlayReady content encryption,  PlayReady protects content, ECC, RSA, AES
ms.date: 02/01/2018
ms.topic: article
---


# PlayReady Content Encryption

This topic provides an overview of the encryption algorithms used to protect content in the PlayReady ecosystem.

> [!NOTE]
> See [Glossary](../Overview/glossary-and-abbreviations.md) for encryption terms and definitions.

## Encryption basics


*Symmetric key cryptography* is the simplest type of encryption. With symmetric key cryptography, the same key is used to encrypt the content and decrypt it. Symmetric key algorithms are usually small and fast. Typically, the bulk of any encryption task is handled by some form of symmetric key encryption.


*Public key cryptography*, in contrast, uses a published public key to encrypt, and a different, secret, private key to decrypt. Thus, if user "A" gives user "B" a public key, B can encrypt content for A without any other information. No matter how the content is transmitted, only A will be able to read it. Content interceptors lack the private key (secret key) and are unable to decrypt the message. Because the public key is made openly available, anyone can encrypt for A, but only A can decrypt. Public key cryptography requires computationally complex algorithms.


*Elliptic curve cryptography* (ECC) is a public key cryptography algorithm that is used to encrypt and decrypt content. It is a computationally complex function that describes an elliptic curve. Components of this algorithm are shared as a public key. Other components, used for decryption, form the private key.


*One-key Message Authentication Codes* (OMAC) is a message authentication code constructed from a block cipher. There are two OMAC algorithms, OMAC1 and OMAC2.


*Certificates* are used to ensure authenticity for entities that are not trusted. The sender of a certificate signs its name (device identifier) by using its private key. The recipient of the certificate then verifies the signature of the certificate with the sender's public key to ensure the sender's identity. Because the sender is the only owner of the private key, it is difficult to create a private key given a public key, and the certificate will not be verified correctly unless it is signed with the private key; in this case, the data source is assumed to be correct and certified communication is secure.



## PlayReady encryption algorithms



### Symmetric algorithms

The following AES encryption modes are supported:


  * **AES 128 CTR mode** &mdash; PlayReady systems can protect files and streams where the samples are encrypted in full or where only a pattern of the samples are encrypted, in CTR mode of operation. These include the Common Encryption modes 'cenc' (Common Encryption Scheme) and 'cens' (Common Encryption Scheme using a pattern of unencrypted/encrypted bytes), which are defined in ISO/IEC 23001-7.

  * **AES 128 CBC mode** &mdash; PlayReady systems starting with version 4.0 can protect files and streams that are either fully or partially encrypted with an AES 128 content key, in CBC mode of operation. These include the Common Encryption modes 'cbc1' and 'cbcs' as defined in ISO/IEC 23001-7, and any other format that is encrypted with an AES 128 content key in CBC mode.


> [!NOTE]
> PlayReady systems with version 1.X, 2.X and 3.X can only protect files encrypted in CTR mode (Common Encryption mode 'cenc'). 'cens' is not supported.
> PlayReady systems with version 4.0 and higher can protect files encrypted in CTR mode (Common Encryption modes 'cenc') and in CBC mode (Common Encryption modes 'cbcs'). The other modes 'cens' and 'cbc1' are not supported.


### ECC algorithms


Microsoft PlayReady systems use ECC (Elliptical curve cryptography) for encrypting content keys and signing protocol messages.

  * **ECC ElGamal algorithm** &mdash; Used for encrypted content keys.
  * **ECDSA** (Elliptic curve digital signature algorithm) &mdash; Used for signing messages wherever applicable in the PlayReady protocols.
  * **NIST** &mdash; Microsoft PlayReady systems use standard NIST algorithms for ECC encryption where applicable and is currently using the P-256 elliptic curve.




### Signing algorithms


For signing licenses, transient keys or data, PlayReady systems use AES OMAC1, which is equivalent to CMAC (Cipher-based message Authentication Code) and became a [NIST](http://csrc.nist.gov/publications/nistpubs/800-108/sp800-108.pdf) recommendation in May 2005. Keys are generated at random, but data is hashed with SHA256 and then the hash is signed with ECC256.




## Runtime and performance considerations


When content playback is triggered, the PlayReady Client must perform some steps before initial playback can begin. This includes finding a license, binding, or interpreting the license, decrypting the content key, and finally, preparing to decrypt the content. The PlayReady Client stack takes time to bind a license to a piece of content, and this operation is required prior to starting the content decryption and rendering. This means that the time to bind a license impacts the time to first frame when starting a playback, or the gap between tracks. The client developer as well as the application developer might want to consider optimizing their code for runtime and performance issues, to reduce the time to first frame, and allow gapless playback.

Protected containers use symmetric key encryption to encrypt the bulk of content. However, public key encryption is used within the license. This is because the license contains the content’s symmetric key, and the Server uses the client’s public key to encrypt the content’s symmetric key.

When it is time to decrypt the content, the client's private key is used to decrypt the symmetric key from the license. Only the client that the license is bound to can extract the symmetric key.

Private key decryption is more intensive computationally, than symmetric decryption; therefore, interpreting the license is computationally intensive. Once the license has been properly handled, the symmetric key is decrypted and the content may be decrypted using small and fast algorithms.

For applications or devices that are resource-constrained, start-up requires significant time and resources. Once that is complete, however, the resources are freed, decryption may proceed efficiently, and few CPU cycles or system resources are required.
