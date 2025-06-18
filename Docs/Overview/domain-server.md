---
title: PlayReady Domain Server
description: You can manage content access for multiple Clients through a single entity, called a PlayReady domain.
ms.assetid: "0F53EB0C-1BF0-4949-8889-244AE669A28D"
keywords: about PlayReady domains,  PlayReady domain server
ms.date: 02/01/2018
ms.topic: article
---


# PlayReady Domain Server

*PlayReady Domains* are a feature that allows services to deliver licenses that are bound to a group (domain) of devices, not just one device. By doing that, devices can then share the content and the license bound to a domain between them, without involving the use of a license server again. The service has full control over what devices are in a certain domain, and how large the domains are.


A *PlayReady Domain Server*, also known as a *PlayReady Domain Controller*, is a server that receives PlayReady transactions from PlayReady clients to join a domain, leave a domain, or renew their domain certificate.

It is a logical server based on the *PlayReady Server SDK* like all the PlayReady Server types, and can be operated on the same machine as the other PlayReady servers, or on a different machine.

## See also

[PlayReady Domains](../Features/domains.md)
