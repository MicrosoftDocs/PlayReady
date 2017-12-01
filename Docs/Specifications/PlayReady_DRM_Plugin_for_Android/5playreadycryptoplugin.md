---
author: 
title: "5. PlayReadyCryptoPlugin"
description: ""
ms.assetid: "ae6a4428-2874-023a-ce5d-93fbc7bbb49b"
kindex: PlayReadyCryptoPlugin
keywords: PlayReadyCryptoPlugin
ms.author: 
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# 5. PlayReadyCryptoPlugin
 
<a id="ID4EN"></a>

   

## PlayReadyCryptoPlugin  
   
  
Constructor to create a **PlayReadyCryptoPlugin** object.   
   
```cpp
PlayReadyCryptoPlugin::PlayReadyCryptoPlugin(
      const uint8_t sessionId[16],
      const void *  data,
      size_t        size);
{
  DRM_RESULT         dr = DRM_SUCCESS;
  Mutex::Autolock lock(&SessionManager::sLock);

  ChkDR(Drm_Reader_Bind(
         &SessionManager::soAppContext,
         NULL,
         0,
         NULL,
         NULL,
         &moDecryptContext));

ErrorExit:
  // Cache the Bind Result and check for it on the first call to decrypt.
  mdrBindResult = dr;
}
```
  
<a id="ID4EZ"></a>

   

## requiresSecureDecoderComponent  
   
  
A secure decoder component is required to process PlayReady encrypted content.   
   
```cpp
bool PlayReadyCryptoPlugin::requiresSecureDecoderComponent(const char *mime) const
{
  // Must always return true for PlayReady Content.
  return true;
}
```
  
<a id="decrypt"></a>

   

## decrypt  
   
  
The decryption called by **MediaCodec**.   
   
  
Since the decryption method will not give out clear samples, but rather an OEM-specific handle, the OEM must ensure that **MediaCodec** is able to operate correctly on that handle.   
   
```cpp
ssize_t PlayReadyCryptoPlugin::decrypt(
      bool                 secure,
      const uint8_t        key[16],
      const uint8_t        iv[16],
      Mode                 mode,
      const void          *srcPtr,
      const SubSample     *subSamples,
      size_t               numSubSamples,
      void                *dstPtr,
      AString             *errorDetailMsg)
{
  DRM_RESULT        dr = DRM_SUCCESS;
  DRM_DWORD         idx = 0;
  DRM_DWORD         idxSubSample = 0;
  DRM_DWORD         cbEncryptedContent = 0;
  DRM_UINT64        ui64InitializationVector;
  DRM_DWORD        *pdwEncryptedRegionMappings = NULL;
  DRM_DWORD         cbOpaqueClearContentHandle = 0;
  Mutex::Autolock lock(mLock);

  // Only AES_CTR is supported
  ChkBOOL(mode == kMode_AES_CTR, DRM_E_UNSUPPORTED_ALGORITHM);
  ChkArg(secure == TRUE);

  // Ensure that bind returned successfully in the constructor.
  ChkDR( mdrBindResult );

  // Allocate a list for the region mapping.
  ChkMem(pdwEncryptedRegionMappings
        = Oem_MemAlloc(sizeof(DRM_DWORD)* numSubSamples * 2));

  // Fill the region mappings list with the information
  // from the subSamples.
  for (idxSubSample = 0; idxSubSample < numSubSamples; idxSubSample++)
  {
    pdwEncryptedRegionMappings[idx++] 
          = subSamples[idxSubSample].mNumBytesOfClearData;
    pdwEncryptedRegionMappings[idx++] 
          = subSamples[idxSubSample].mNumBytesOfEncryptedData;

    // Calculate the total number of bytes
    cbEncryptedContent += 
          (subSamples[idxSubSample].mNumBytesOfClearData 
          + subSamples[idxSubSample].mNumBytesOfEncryptedData);
  }

  // Convert the IV from a uint8 array to a DRM_UINT64
  // Endianess should be taken into consideration.
  ChkStatus(initializeIV(iv, &ui64InitializationVector));

  // Decrypt
  ChkDR(Drm_Reader_DecryptOpaque(
      &moDecryptContext,
      numSubSamples * 2,
      pdwEncryptedRegionMappings,
      ui64InitializationVector,
      cbEncryptedContent,
      srcPtr,
      &cbOpaqueClearContentHandle,
      &dstPtr);

ErrorExit:
  // Free the Region mappings list.
  SAFE_FREE(pdwEncryptedRegionMappings);

  if (DRM_FAILED(dr))
  {
    // If an error occurs, fill the errorMessage
    // then return the DRM_RESULT
    SetErrorDetails(errorDetailMsg, dr);
    return _DR_TO_STATUS(dr);
  }
  // In case of success, return the size of the handle pointing
  // to the clear content.
  return cbOpaqueClearContentHandle;
}
```
  
<a id="ID4EUB"></a>

   

## ~PlayReadyCryptoPlugin  
   
  
The crypto plug-in destructor must close the decryptor context.   
   
```cpp
~PlayReadyCryptoPlugin::PlayReadyCryptoPlugin()
{
  Mutex::Autolock lock(mLock);
  Drm_Reader_Close(&moDecryptContext);
}
```
  
