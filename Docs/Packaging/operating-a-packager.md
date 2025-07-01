---
title: Operating a PlayReady Packager
description: Describes the basic process of operating a PlayReady packager
ms.assetid: "726C14AE-AE51-4DE3-BB11-F43FFE18CE9B"
keywords:  PlayReady, packager, encryptor, operating packager
ms.date: 05/11/2018
ms.topic: how-to
---

# Operating a PlayReady Packager

Note that operating a packager that provides PlayReady protection for content you want to protect:

* Does not require a licensing agreement from Microsoft.
* Does not bear any fees or royalty payments to Microsoft.

The following figure shows the overall view of how a PlayReady packager operates with other parts of the content delivery system.

![PlayReady Packager Operation](../images/packager_operation.png)

Steps:

1. You need to connect the packager to a Key Management system to store the content encryption keys for each piece of content. Alternatively, you may set the content encryption keys or Key Seed manually through the packager's interface.

2. The packager receives clear content.

3. The packager outputs protected content.

## Packaging and Client Policies

The packager just packages and protects the content. It does not define the policies that will be sent to clients by the PlayReady License Server.

Once the content is protected, the service can define any set of PlayReady policies to be sent to any client independently, by inserting them in the license generated for that particular client. That means, the same piece of content, once protected, and identified with its KID or list of KIDs, can be served to client A with a certain set of playback policies (for example, play on internal screen, up to the 4K resolution, for 48 hours maximum), while served to client B with a different set of playback policies (for example, play on internal and external screens, up to the 1080p resolution maximum, with no time limitation).


## See also
[PlayReady Test Content](../Advanced/TestContent/playready-test-content.md)
