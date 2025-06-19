---
title: PlayReady Key Seed
description: This page specifies the PlayReady Key Seed algorithm that allows diverisfy content keys based on a KID.
ms.assetid: "62995E85-EE3A-4C36-844B-950719194185"
keywords: PlayReady key seed, kid, content key, specification
ms.date: 06/01/2018
ms.topic: article
---


# PlayReady Key Seed

Services implementing PlayReady must maintain a Key Management System (KMS) to store and manage content keys. Specifically, the values of {KID, Content Key} are stored for each content asset that is managed by the service. These values are stored at encryption time, and retrieved at license issuance time.

PlayReady provides a convenient way to avoid a complex KMS. The *Content Key Seed algorithm* allows derivation of different content keys for a collection of content assets, from a varying KID and a fixed Key Seed:

  `Ck(KID) = f(KID, KeySeed)`

The following is the PlayReady standard algorithm:

```cs
byte[] GeneratePlayReadyContentKey(byte[] keySeed, Guid keyId)
{
    const int DRM_AES_KEYSIZE_128 = 16;
    byte[] contentKey = new byte[DRM_AES_KEYSIZE_128];
    //
    //  Truncate the key seed to 30 bytes, key seed must be at least 30 bytes long.
    //
    byte[] truncatedKeySeed = new byte[30];
    Array.Copy(keySeed, truncatedKeySeed, truncatedKeySeed.Length);
    //
    //  Get the keyId as a byte array
    //
    byte[] keyIdAsBytes = keyId.ToByteArray();
    //
    //  Create sha_A_Output buffer.  It is the SHA of the truncatedKeySeed and the keyIdAsBytes
    //
    SHA256Managed sha_A = new SHA256Managed();
    sha_A.TransformBlock(truncatedKeySeed, 0, truncatedKeySeed.Length, truncatedKeySeed, 0);
    sha_A.TransformFinalBlock(keyIdAsBytes, 0, keyIdAsBytes.Length);
    byte[] sha_A_Output = sha_A.Hash;
    //
    //  Create sha_B_Output buffer.  It is the SHA of the truncatedKeySeed, the keyIdAsBytes, and
    //  the truncatedKeySeed again.
    //
    SHA256Managed sha_B = new SHA256Managed();
    sha_B.TransformBlock(truncatedKeySeed, 0, truncatedKeySeed.Length, truncatedKeySeed, 0);
    sha_B.TransformBlock(keyIdAsBytes, 0, keyIdAsBytes.Length, keyIdAsBytes, 0);
    sha_B.TransformFinalBlock(truncatedKeySeed, 0, truncatedKeySeed.Length);
    byte[] sha_B_Output = sha_B.Hash;
    //
    //  Create sha_C_Output buffer.  It is the SHA of the truncatedKeySeed, the keyIdAsBytes,
    //  the truncatedKeySeed again, and the keyIdAsBytes again.
    //
    SHA256Managed sha_C = new SHA256Managed();
    sha_C.TransformBlock(truncatedKeySeed, 0, truncatedKeySeed.Length, truncatedKeySeed, 0);
    sha_C.TransformBlock(keyIdAsBytes, 0, keyIdAsBytes.Length, keyIdAsBytes, 0);
    sha_C.TransformBlock(truncatedKeySeed, 0, truncatedKeySeed.Length, truncatedKeySeed, 0);
    sha_C.TransformFinalBlock(keyIdAsBytes, 0, keyIdAsBytes.Length);
    byte[] sha_C_Output = sha_C.Hash;
    for (int i = 0; i < DRM_AES_KEYSIZE_128; i++)
    {
        contentKey[i] = Convert.ToByte(sha_A_Output[i] ^ sha_A_Output[i + DRM_AES_KEYSIZE_128]
                                       ^ sha_B_Output[i] ^ sha_B_Output[i + DRM_AES_KEYSIZE_128]
                                       ^ sha_C_Output[i] ^ sha_C_Output[i + DRM_AES_KEYSIZE_128]);
    }

    return contentKey;
}
```


