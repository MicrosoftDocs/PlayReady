---
title: License Nonce
description: A PlayReady Client includes a random GUID called the license nonce in every license request that it generates for a License Server.
ms.assetid: "9F5227F8-83AD-4B6D-A4E3-B06183879629"
keywords: playready license nonce
ms.date: 02/01/2018
ms.topic: article
---


# License Nonce


A PlayReady Client includes a random **GUID** called the License Nonce in every license request that it generates for a License Server.

If the Server delivers a license response with only non-persistent licenses, it includes in the licenses a rights identifier that contains the license request's License Nonce.

When adding the licenses received to the In-Memory-Only data store, the client verifies that the license's rights identifier matches the license request's License Nonce, and rejects the licenses that don't match.

This mechanism is designed this way for PlayReady robustness reasons, and avoids instances of an attacker replaying non-persistent licenses over and over to get an indefinite play right to a certain key identifier (KID).

If the Server delivers a license response with at least one persistent license, it includes in the license response a License Nonce. This mechanism is designed for device security reasons, to block an HDS-fill-DOS attack. This blocks an attacker from filling up the HDS by replaying a license response over and over again, which may lead to filling up the HDS, or even the memory (HDD, SSD, NAND Flash) if the device has no protection against HDS inflation, and make it inoperative.

