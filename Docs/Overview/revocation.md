---
title: PlayReady Revocation
description: When Microsoft identifies a Client with compromised security, the device may be revoked and added to a revocation list.
ms.assetid: "09869289-666b-272e-1cc2-97079cb71204"
keywords: playready revocation,  revocation list
ms.date: 02/01/2018
ms.topic: conceptual
---


# PlayReady Revocation

## What is PlayReady Revocation

Revocation is a process to identify clients that have compromised security, and prevent those clients from getting access to additional licenses for decrypting content that has been protected.


When Microsoft identifies a client with compromised security, the device may be revoked and added to a revocation list. The revocation list is periodically downloaded by the License Servers that issue licenses for protected content. License Servers use this revocation list to deny licenses to devices that have been revoked, thereby preventing the device from playing newly protected content.


Revocation lists are refreshed on devices when they are not up to date. The revocation list may also be issued with licenses. The DRM component on the device checks this revocation list before transferring content to other devices. By preventing communication with revoked components, revoked applications no longer work. Once revoked, the only way to fix the situation is to replace the revoked element or remove the revoked component from a newer version of the revocation list.


## Link to the current PlayReady Revocation Lists

Microsoft builds and maintains the revocation list and its versioning structure. PlayReady customers can download this list from the following link:

**PlayReady Revocation List(https): [https://aka.ms/revinfo](https://aka.ms/revinfo)**

**PlayReady Revocation List(http): [http://go.microsoft.com/fwlink/?LinkId=110086](https://go.microsoft.com/fwlink/?LinkId=110086)**

## Requirement for PlayReady Servers

Per the requirements of the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/), companies operating a PlayReady Server "must update the PlayReady Server Software Development Kit certificate revocation lists for each PlayReady Server once a week". This ensures any compromised client gets its license requests declined in a reasonable time frame after its addition by Microsoft to the Revocation List.

## Ignoring Individual Entries in the PlayReady Revocation List

Starting with PlayReady Server version 4.3, your server application may explicitly ignore one or more revoked hashes and continue to issue content to them even though they are revoked. This may be useful to companies that both produce and distribute protected content and who wish to have more control over where that content can flow.

To utilize this feature, you will need to create a new XML file containing the certificate hashes you wish to ignore as well as add a new entry to the web.config file of your RMSDK implementation.  The XML file has the following format.

<?XML VERSION="1.0" ENCODING="UTF-8"?>
   <REVALLOWINFO>
      <ALLOWLIST>
         <CERTIFICATEHASH>2C4OCYBGE3XZ3ODIUVUWD0SVLWH4W1NX9EA5DMJZ/PK=</CERTIFICATEHASH>
         <CERTIFICATEHASH>9OHU9A1KAJYI9BUWQWAVXBOO7R4XS+GG8HV0ESDBTNW=</CERTIFICATEHASH>
      </ALLOWLIST>
   </REVALLOWINFO>

The data within the "CertificateHash" node must match the hash of the revoked model or company certificate. Microsoft intends to publish this information, along with corresponding model information, for future revocations.  

You must also reference this XML file from within your server configuration.

* For .Net Core-based RMSDK deployments, the XML file should be added as an item project, and the RevocationAllowFile string in config/RMSDKConfig.cs should be updated with the path to the XML file.
* For IIS-based RMSDK deployments, this is done by adding a new key with a name of "REVOCATIONALLOWFILE" which points to your XML file to the web.config file.

    * For example, if the XML file above was named "REVOCATIONALLOWSAMPLE.XML", the web.config file would be updated as follows:

<?XML VERSION="1.0" ENCODING="UTF-8"?>
   <CONFIGURATION>
      <APPSETTINGS>
         <ADD KEY="HANDLERDLL" VALUE="BIN\CFGHANDLER.DLL"/>
         <ADD KEY="SERVERCERTIFICATECONFIGFILE" VALUE="APP_DATA\TESTSERVICEDEPLOYMENTCERT_EX20200311.XML"/>           
         <ADD KEY="REVOCATIONDATAFILE" VALUE="REVINFO2V43_20180427.XML"/>
         <ADD KEY="ROBUSTNESSVERSIONSDATAFILE" VALUE="ROBUSTNESSVERSIONS.XML"/>
         <ADD KEY="REVOCATIONALLOWFILE" VALUE="REVOCATIONALLOWSAMPLE.XML">
         ...

