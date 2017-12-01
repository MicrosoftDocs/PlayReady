---
author:
title: "4. PlayReadyDRMPlugin"
description: ""
ms.assetid: "b66271ef-e1c7-1e71-584e-53bce2f8d50f"
kindex: PlayReadyDRMPlugin
keywords: PlayReadyDRMPlugin
ms.author:
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# 4. PlayReadyDRMPlugin

<a id="ID4EN"></a>



## setPropertyString


Apps will use this method to pass parameters to PlayReady that are not otherwise possible due to the current design of the plug-in APIs.

   *  **DeviceStoreName**&mdash;The app must set the location of the device store as a property prior to opening a session. Then PlayReady will look up the **DeviceStoreName** property upon initializing the DRM Manager during calls to [openSession](#opensession). The path to the device store must be accessible to the app like the app's private data directory. The property should point to a &lt;path/filename> that should hold the HDS.

   *  **LicenseChallengeCustomData**&mdash;The app can optionally set this property prior to calls to [getKeyRequest](#getkeyrequest), where PlayReady will look up the property and compose a license acquisition challenge and include the custom data in the request.

   *  **SecureStopCustomData**&mdash;The app can optionally set this property prior to a call to generate the secure stop challenge. PlayReady will look up the property and compose the secure stop challenge and include the custom data in the request.

   *  **SelectKID**&mdash;In situations where the app has acquired multiple in-memory licenses in a single batch, it can specify a base64 encoded KID for binding.


```cpp
status_t PlayReadyDrmPlugin::setPropertyString(
String8 const &name,
String8 const &value)
{
  DRM_RESULT       dr = DRM_SUCCESS;
  Mutex::Autolock lock(&SessionManager::sLock);

  //
  // Store the Property in the name/value KeyedVector
  // for later usage.
  //
  ChkDR( mStringProperties.add(name, value));

  if (name == "SelectKID")
  {
    DRM_SUBSTRING dasstrKID = DRM_EMPTY_DRM_SUBSTRING;
    DRM_CONST_STRING dstrKID = DRM_EMPTY_DRM_STRING;
    DRM_BYTE rgbKID[CCH_BASE64_EQUIV(CCH_BASE64_EQUIV(DRM_ID_SIZE)] = {0};

    const char *pszhKID = value.string();

    // Convert the ASCII KID to UNICODE
    DRM_DSTR_FROM_PB(&dstrKID, rgbKID, sizeof(rgbKID));
    DRM_UTL_PromoteASCIItoUNICODE(pszhKID, &dasstrKID, (DRM_STRING *)&dstrKID);

    ChkDR(Drm_Content_SetProperty(
    &SessionManager::soAppContext, // DRM_APP_CONTEXT pointer
    DRM_CSP_SELECT_KID,
    dstrKID.pwszString,
    dstrKID.cchString * sizeof(DRM_WCHAR)));
  }

ErrorExit:
  return _DR_TO_STATUS(dr);
}
```

<a id="setpropertybytearray"></a>



## setPropertyByteArray


Apps will use this method to pass parameters to PlayReady that are not otherwise possible due to the current design of the Plug-in APIs.

   *  *ContentHeader*&mdash;The app should set the content header on the plug-in before attempting to create a Crypto object. The content header could be in one of the following formats:

      *  Byte array with the contents of the PlayReady Object.

      *  Byte array with the contents of the V2, V2.4, V4, V4.1, V4.2 headers (unicode XML).

      *  Wide character array specifying the 24-character KeyID.


   *  *SecureStopPublisherCert*&mdash;The app should set the Publisher Certificate once before all secure stop related calls.


```cpp
status_t PlayReadyDrmPlugin::setPropertyByteArray(
String8         const &name,
Vector<uint8_t> const &value)
{
  DRM_RESULT      dr = DRM_SUCCESS;
  Mutex::Autolock lock(&SessionManager::sLock);

  // Add the name/value pair to a KeyedVector
  mByteArrayProperties.add(name, value);

  // If the provided property is a content header
  // go ahead and set the property.
  if (name == "ContentHeader")
  {
    ChkDR(Drm_Content_SetProperty(
      &SessionManager::soAppContext, // DRM_APP_CONTEXT pointer
      DRM_CSP_AUTODETECT_HEADER,
      value.data(),
      value.size()));
  }

ErrorExit:
  return _DR_TO_STATUS(dr);
}
```

<a id="opensession"></a>



## openSession


This call should result in initializing the AppContext by calling the DRM Manager's Drm_Initialize function.


Prior to this call, the app must set **PropertyString** on the plug-in to provide the path to the device store that will be used to store the HDS.

```cpp
status_t PlayReadyDrmPlugin::openSession(Vector<luint8_t> &sessionId)
{
  DRM_RESULT          dr = DRM_SUCCESS;
  DRM_CONST_STRING    dstrDeviceStoreName = { 0 };
  String8             deviceStoreName;

  Mutex::Autolock lock(&SessionManager::sLock);

  ChkMem(mpbOpaqueBuffer =
    (DRM_BYTE*)Oem_MemAlloc(MINIMUM_APPCONTEXT_OPAQUE_BUFFER_SIZE));

  //
  // Application must call setPropertyString to set the DeviceStoreName
  // before opening the session.
  // So the call to getPropertyString with DeviceStoreName must return a value.
  //
  ChkDR(getPropertyString(String8("DeviceStoreName"), deviceStoreName));

  // Convert the deviceStoreName to a DRM_CONST_STRING */
  ChkDR(util_String8ToDrmConstString(deviceStoreName, &dstrDeviceStoreName));

  // Initialize AppContext
  ChkDR(Drm_Initialize(
    &SessionManager::soAppContext,
    NULL,             // pOEMContext : OEM can initialize and pass if needed.
    mpbOpaqueBuffer,
    MINIMUM_APPCONTEXT_OPAQUE_BUFFER_SIZE,
    &dstrDeviceStoreName));

ErrorExit:
  return _DR_TO_STATUS(dr);
}
```

<a id="ID4EQD"></a>



## closeSession


Closing a DRM Session should call Drm_Uninitialize to release the AppContext.

```cpp
status_t PlayReadyDrmPlugin::closeSession(Vector<uint8_t> const &sessionId)
{
  Mutex::Autolock lock(&SessionManager::sLock);

  // Clear the App Context
  Drm_Uninitialize(&SessionManager::soAppContext);
  SAFE_FREE(mpbOpaqueBuffer);
  return OK;
}
```

<a id="getkeyrequest"></a>



## getKeyRequest


This method will generate a license request challenge.


ContentHeader&mdash;The app can either pass the content header in the *initData* parameter or, prior to calling this function, the app must set the **ContentHeader** string property.


LicenseChallengeCustomData&mdash;The app may pass the challenge custom data in the *optionalParameters* parameter with the string key "LicenseChallengeCustomData". Alternatively, the method can pick up the **LicenseChallengeCustomData** if the app has already set it as a property.


The method will populate the *defaultUrl* if available in the content header as well as the request to be sent to the license server.

```cpp
status_t PlayReadyDrmPlugin::getKeyRequest(
        Vector<uint8_t>                   const &sessionId,
        Vector<uint8_t>                   const &initData, s// ContentHeader
        String8                           const &mimeType,
        KeyType                                 keyType,
        KeyedVector<String8, String8="">  const &optionalParameters, // ChallengeCustomData
        Vector<uint8_t>                         &request,            // Output Challenge
        String8                                 &defaultUrl,         // Output URL
        KeyRequestType                         *keyRequestType)
{
  DRM_RESULT      dr = DRM_SUCCESS;
  DRM_BYTE       *pbContentProperty = NULL;
  DRM_DWORD       cbContentProperty = 0;
  DRM_CHAR       *pchCustomData = NULL;
  DRM_DWORD       cchCustomData = 0;
  DRM_CHAR       *pchSilentURL = NULL;
  DRM_DWORD       cchSilentURL = 0;
  DRM_BYTE       *pbChallenge = NULL;
  DRM_DWORD       cbChallenge = 0;
  DRM_BOOL        fHasUrl = FALSE;
  Vector<uint8_t> contentHeader;
  String8         customData;

  Mutex::Autolock lock(&SessionManager::sLock);

  if (getValue(optionalParameters, String8("LicenseChallengeCustomData"), customData) == OK)
  {
    //
    // The Application can pass the custom data as a part of the optionalParameters.
    // The key string would be "LicenseChallengeCustomData".
    // If it is provided. The plug-in should use it when generating the license challenge.
    //
    pchCustomData = customData.data();
    cchCustomData = customData.size();
  }
  else if (getPropertyString(String8("LicenseChallengeCustomData"), customData) == OK)
  {
    //
    // Alternatively the Application could have provided customData for this operation
    // via a previous call to setPropertyString.
    // Try to retrieve it if available. Otherwise, skip without failing.
    //
    pchCustomData = customData.data();
    cchCustomData = customData.size();
  }

  //
  // The Application could choose to pass the content header as the initData
  // If the initData is passed, use it to call Drm_Content_SetProperty
  //
  if (value.size() != 0)
  {
    ChkDR(Drm_Content_SetProperty(
      &SessionManager::soAppContext, // DRM_APP_CONTEXT pointer
      DRM_CSP_AUTODETECT_HEADER,
      value.data(),
      value.size()));
  }

  //
  // First, try to retrieve the URL.
  //
  dr = Drm_LicenseAcq_GenerateChallenge(
    &SessionManager::soAppContext,
    NULL,
    0,
    NULL,
    pchCustomData,
    cchCustomData,
    pchSilentURL,
    &cchSilentURL,    // Attempt to get the URL size.
    NULL,
    NULL,
    pbChallenge,
    &cbChallenge);
  if (dr == DRM_E_BUFFERTOOSMALL)oi
  {
    fHasUrl = TRUE;

    // ContentHeader has a URL. Allocate buffer for it.
    ChkMem(pchSilentURL = (DRM_CHAR*)Oem_MemAlloc(cchSilentURL));
  }
  else if (dr == DRM_E_NO_URL)
  {
    // No Url in the content header, no need to fail.
    // The Application can get the URL independently.
    dr = DRM_SUCCESS;
  }
  else
  {
    ChkDR(dr);
  }

  //
  // Second, get the challenge size.
  //
  dr = Drm_LicenseAcq_GenerateChallenge(
    poAppContext,
    NULL,
    0,
    NULL,
    pchCustomData,
    cchCustomData,
    pchSilentURL,
    fHasUrl ? &cchSilentURL : NULL,
    NULL,
    NULL,
    pbChallenge,
    &cbChallenge);
  if (dr == DRM_E_BUFFERTOOSMALL)
  {
    // Allocate buffer that is sufficient
    // to store the license acquisition challenge.
    ChkMem(pbChallenge = (DRM_BYTE*)Oem_MemAlloc(cbChallenge));
  }
  else
  {
    ChkDR(dr);
  }

  //
  // Finally, generate challenge.
  //
  ChkDR(Drm_LicenseAcq_GenerateChallenge(
    &SessionManager::soAppContext,
    NULL,
    0,
    NULL,
    pchCustomData,
    cchCustomData,
    pchSilentURL,
    fHasUrl ? &cchSilentURL : NULL,
    NULL,
    NULL,
    pbChallenge,
    &cbChallenge));

  //
  // Write the License Challenge to the request buffer.
  //
  request.appendArray(pbChallenge, cbChallenge);

  if (fHasUrl)
  {
    defaultUrl.appendArray(pchSilentURL, cchSilentURL);
  }

ErrorExit:
  SAFE_OEM_FREE(pbChallenge);
  SAFE_OEM_FREE(pchSilentURL);
  return _DR_TO_STATUS(dr);
}
```

<a id="providekeyresponse"></a>



## provideKeyResponse


Once a `KeyRequest (LicenseChallenge)` has been sent by the app to the license server, the app should pass the `KeyResponse (LicenseResponse)` to the plug-in.

```cpp
status_t PlayReadyDrmPlugin::provideKeyResponse(
      Vector<uint8_t>        const &sessionId,
      Vector<uint8_t>        const &response,
      Vector<uint8_t>        &keySetId)
{
  DRM_RESULT           dr = DRM_SUCCESS;
  DRM_LICENSE_RESPONSE oLicenseResponse = { 0 };
  DRM_DWORD            idx = 0;
  DRM_BOOL             fExceedMaxLic = FALSE;
  Mutex::Autolock lock(&SessionManager::sLock);

  //
  // Process the response.
  //
  dr = Drm_LicenseAcq_ProcessResponse(
            &SessionManager::soAppContext,
            0,
            NULL,
            NULL,
            response.data(),
            response.size(),
            &oLicenseResponse);
  if(dr ==  DRM_E_LICACQ_TOO_MANY_LICENSES)
  {
    //
    // Received more licenses than DRM_MAX_LICENSE_ACK.
    // Allocate space for that.
    //

    oLicenseResponse.m_cMaxAcks = oLicenseResponse.m_cAcks;
    ChkMem(oLicenseResponse.m_pAcks=
    (DRM_BYTE*)Oem_MemAlloc(sizeof(DRM_LICENSE_ACK)
    * oLicenseResponse.m_cAcks ));
    ChkDR(Drm_LicenseAcq_ProcessResponse(
            &SessionManager::soAppContext,
            0,
            NULL,
            NULL,
            response.data(),
            response.size(),
            &oLicenseResponse);

    fExceedMaxLic = TRUE;
  }
  ChkDR(dr);

  //
  // Ensure that all licenses were processed successfully.
  //

  if(fExceedMaxLic)
  {
    for (idx = 0; idx < oLicenseResponse.m_cAcks; idx++)
    {
      ChkDR(oLicenseResponse.m_pAcks[idx].m_dwResult);
    }
  }
  else
  {
    for (idx = 0; idx < oLicenseResponse.m_cAcks; idx++)
    {
      ChkDR(oLicenseResponse.m_rgoAcks[idx].m_dwResult);
    }
  }

ErrorExit:
  SAFE_FREE(oLicenseResponse.m_pAcks);
  return _DR_TO_STATUS(dr);
}
```

<a id="ID4ENF"></a>



## getSecureStop(s)


Apps can call the **getSeucreStop** method to generate a secure stop challenge for the specified secure stop ID. Alternatively, the app can call **getSecureStops** to generate a challenge for all the existing secure stop sessions.


Prior to generating the secure stop challenge, the app must provide the publisher certificate by calling [setPropertyByteArray](#setpropertybytearray) and passing **SecureStopPublisherCert**.


Optionally the app can also provide **SecureStopCustomData** to be included as a part of the secure stop challenge.


After the secure stop challenge is created, the app should send it to the server and provide back the secure stop response to the [releaseSecureStops](#releasesecurestops) method.

```cpp
DRM_RESULT PlayReadyDrmPlugin::_getSecureStop(
DRM_ID       *pIdSession,
DRM_BYTE    **ppbChallenge,
DRM_DWORD    *pcbChallenge)
{
  DRM_RESULT       dr = DRM_SUCCESS;
  DRM_CHAR        *pchCustomData = NULL;
  DRM_DWORD        cchCustomData = 0;
  String8          customData;
  Vector<uint8_t>  publisherCert;

  if (getPropertyString("SecureStopCustomData", customData) == OK)
  {
    // SecureStop CustomData is optional
    pchCustomData = customData.data();
    cchCustomData = customData.size();
  }

  // Application must set SecureStopPublisherCert before calling getSecureStop(s)
  ChkDR(getPropertyByteArray("SecureStopPublisherCert", publisherCert));

  ChkDR(Drm_SecureStop_GenerateChallenge(
        &SessionManager::soAppContext,
        pIdSession,
        publisherCert.size(),
        publisherCert.data(),
        cchCustomData,
        pchCustomData,
        pcbChallenge,
        ppbChallenge));
ErrorExit:
  return dr;
}

status_t PlayReadyDrmPlugin::getSecureStop(
        Vector<uint8_t>          const &ssid,           // In
        Vector<uint8_t>                &secureStop)     // Out
{
  DRM_RESULT dr = DRM_SUCCESS;
  DRM_ID     idSecureStop = { 0 };
  DRM_BYTE  *pbChallenge = NULL;
  DRM_DWORD  cbChallenge = 0;
  Mutex::Autolock lock(&SessionManager::sLock);

  ChkArg(ssid.size() == sizeof(DRM_ID));
  memcpy(&idSecureStop, ssid.data(), sizeof(DRM_ID));

  ChkDR(_getSecureStop(
            &idSecureStop,
            &pbChallenge,
            &cbChallenge));

  secureStop.appendArray(pbChallenge, cbChallenge);
ErrorExit:
  SAFE_FREE(pbChallenge);
  return _DR_TO_STATUS(dr);
}

status_t PlayReadyDrmPlugin::getSecureStops(
            List<Vector<uint8_t> > &secureStops)
{
  DRM_RESULT dr = DRM_SUCCESS;
  DRM_BYTE  *pbChallenge = NULL;
  DRM_DWORD  cbChallenge = 0;
  Vector<uint8_t> secureStopChallenge;
  Mutex::Autolock lock(&SessionManager::sLock);

  ChkDR(_getSecureStop(
    NULL,
    &pbChallenge,
    &cbChallenge));

  secureStopChallenge.appendArray(pbChallenge, cbChallenge);
  secureStops.push_back(secureStopChallenge);
ErrorExit:
  SAFE_FREE(pbChallenge);
  return _DR_TO_STATUS(dr);
}
```

<a id="releasesecurestops"></a>



## releaseSecureStops


Once the app receives the secure stop response from the server, the message should be passed down to the plug-in to remove the secure stop information from storage.

```cpp
status_t PlayReadyDrmPlugin::releaseSecureStops(
    Vector<uint8_t>      const &ssRelease)
{
  DRM_RESULT dr = DRM_SUCCESS;
  DRM_CHAR    *pchCustomData = NULL;
  DRM_DWORD    cchCustomData = 0;
  Vector<uint8_t> publisherCert;
  Mutex::Autolock lock(&SessionManager::sLock);

  // Application must set SecureStopPublisherCert before calling
  // releaseSecureStops
  ChkDR(getPropertyByteArray("SecureStopPublisherCert", publisherCert));

  ChkDR(Drm_SecureStop_ProcessResponse(
    &SessionManager::soAppContext,
    NULL,
    publisherCert.size(),
    publisherCert.data(),
    ssRelease.size(),
    ssRelease.data(),
    &cchCustomData,
    &pchCustomData));
ErrorExit:
  SAFE_FREE(pchCustomData);
  return _DR_TO_STATUS(dr);
}
```

<a id="ID4E1G"></a>



## Unsupported APIs (No Operation)


The following list of APIs don't have a corresponding operation in PlayReady and are not required for successful execution of the supported scenarios.

<a id="ID4EAH"></a>



### queryKeyStatus

```cpp
status_t PlayReadyDrmPlugin::queryKeyStatus(
        Vector<uint8_t>                  const &sessionId,
        KeyedVector<String8, String8="">       &infoMap) const
{ return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EHH"></a>



### getProvisionRequest


PlayReady supports local provisioning only on Android devices.

```cpp
status_t PlayReadyDrmPlugin::getProvisionRequest(
        String8 const         &certType,
        String8 const         &certAuthority,
        Vector<uint8_t>       &request,
        String8               &defaultUrl) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EQH"></a>



### provideProvisionResponse


PlayReady supports local provisioning only on Android devices.

```cpp
status_t PlayReadyDrmPlugin::provideProvisionResponse(
        Vector<uint8_t>          const &response,
        Vector<uint8_t>                &certificate,
        Vector<uint8_t>                &wrappedKey) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EZH"></a>



### unprovisionDevice


PlayReady supports local provisioning only on Android devices.

```cpp
status_t PlayReadyDrmPlugin::unprovisionDevice() { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EDAAC"></a>



### setCipherAlgorithm


PlayReady doesn't encrypt/decrypt arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::setCipherAlgorithm(
        Vector<uint8_t>       const &sessionId,
        String8               const &algorithm) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EMAAC"></a>



### setMacAlgorithm


PlayReady doesn't sign/verify arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::setMacAlgorithm(
        Vector<uint8_t>       const &sessionId,
        String8               const &algorithm) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EVAAC"></a>



### encrypt


PlayReady doesn't encrypt/decrypt arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::encrypt(
        Vector<uint8_t> const &sessionId,
        Vector<uint8_t> const &keyId,
        Vector<uint8_t> const &input,
        Vector<uint8_t> const &iv,
        Vector<uint8_t>       &output) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4E5AAC"></a>



### decrypt


PlayReady doesn't encrypt/decrypt arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::decrypt(
        Vector<uint8_t> const &sessionId,
        Vector<uint8_t> const &keyId,
        Vector<uint8_t> const &input,
        Vector<uint8_t> const &iv,
        Vector<uint8_t>       &output) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EHBAC"></a>



### sign


PlayReady doesn't sign/verify arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::sign(
        Vector<uint8_t> const &sessionId,
        Vector<uint8_t> const &keyId,
        Vector<uint8_t> const &message,
        Vector<uint8_t>       &signature) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EQBAC"></a>



### verify


PlayReady doesn't sign/verify arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::verify(
        Vector<uint8_t> const &sessionId,
        Vector<uint8_t> const &keyId,
        Vector<uint8_t> const &message,
        Vector<uint8_t> const &signature,
        bool                  &match) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```

<a id="ID4EZBAC"></a>



### signRSA


PlayReady doesn't sign/verify arbitrary data.

```cpp
status_t PlayReadyDrmPlugin::signRSA(
        Vector<uint8_t> const &sessionId,
        String8         const &algorithm,
        Vector<uint8_t> const &message,
        Vector<uint8_t> const &wrappedKey,
        Vector<uint8_t>       &signature) { return _DR_TO_STATUS(DRM_E_NOTIMPL); }
```
