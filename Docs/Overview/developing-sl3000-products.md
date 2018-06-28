---
author: rolandlefranc
title: Developing SL3000 Clients
description: Procedure to develop and distribute PlayReady Security Level 3000 Clients
ms.assetid: "E658777F-FF3A-4898-A884-B281107A621E"
keywords: clients, playready, playbook, security level, 3000, sl3000
ms.author: rolefran
ms.date: 06/01/2018
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---

# Developing PlayReady Security Level 3000 Clients

## Introduction 

This page is intended to serve as a step-by-step guide for PlayReady Licensees seeking SL3000 Compliance for PlayReady Intermediate or Final Products. The document outlines the end-to-end process for Intermediate and Final Products and details the requirements for SL3000 Conformant Intermediate Products.

This page contains two main sections:

 - The SL3000 Design Process section outlines the end-to-end process to be followed by a PlayReady Licensee seeking SL3000 Compliance for an Intermediate Product or a PlayReady Final Product. 

 - The SL3000 Requirements section details the requirements for SL3000 Conformant Intermediate Products. It is important, and required, that IPLs verify these requirements and document this verification for FPLs in a form of “checklist”, because of the nature of the requirements: they’re deep in the hardware and the TEE, and FPLs might not always be in the capacity of verifying these requirements themselves. The provided test report or checklist is a tool to use by IPLs so FPLs know what tests were already run and passed, and can confidently do the supplemental tests that verify the entire conformity of the Final Product.

There is no such section detailing the requirements for Final Products, because FPLs make the final self-assessment of the Final Product that they distribute to end-users, and are not required to communicate their tests to anyone.

## 2. SL3000 Design Process Overview

A PlayReady Security Level is a publicly available and widely understood definition of robustness for PlayReady Products. While products may exceed the robustness requirements for a specific PlayReady Security Level, it establishes the minimum bar that must be met by a product in order to consume content requiring the defined level of protection. The [PlayReady Compliance and Robustness Rules](http://www.microsoft.com/playready/licensing/compliance/) updated in April 2015 introduce the PlayReady Security Level 3000 (SL3000), and requirements for PlayReady TEE implementations to meet the hardware security requirements for PlayReady Enhanced Content Protection. PlayReady SL3000 is designed to be sufficient to meet the security standards for a wide range of content producers, including premium Hollywood content.

PlayReady SL3000 Self-Assessment is intended to assist PlayReady Licensees in obtaining distribution rights for UHD (4K), other types of Enhanced Content (e.g. HDR, 3D, etc.), and new Enhanced Content Delivery Models (e.g., early window).

The security of a PlayReady Product depends critically on the robustness of the PlayReady implementation. A security review, including hardware and firmware, is required for Intermediate Products to qualify for SL3000. The security review is based on the SL3000 Requirements, outlined in Section 4 of this document. This security review must be documented, and the documentation communicated to companies building a Final Products based on this Intermediate Product. This security review can be conducted by a third-party test house, or by the implementer themselves (the IPL).

![PlayReady SL3000 IPL Design](../images/sl3000_design_ipl.png)

PlayReady Final Products are not required to be reviewed by a third-party test house to qualify for SL3000 Compliance. However, Final Products that wish to ship with an SL3000 Certificate may only do so when they meet the requirements for SL3000 Compliant Final Products.  This requires the Final Product to utilize an SL3000 Conformant Intermediate Product and conform to the SL3000 Compliance and Robustness rules. 

![PlayReady SL3000 FPL Design](../images/sl3000_design_fpl.png)

## 3. SL3000 Requirements for Intermediate Products

The security of a PlayReady Product depends critically on the robustness of the PlayReady implementation. As such, Microsoft has defined requirements in the [PlayReady Compliance and Robustness rules](http://www.microsoft.com/playready/licensing/compliance/) that all PlayReady Intermediate Products MUST meet or exceed before they can be distributed to Final Product Licensees. The checklist below is a tool for IPLs to document the security review they’ve run on their product before they distribute it. This security review documentation must be communicated to companies building a Final Product based on this Intermediate Product.

The requirements are broken into 5 categories: 
 1)	CA: Content Accessibility
 2)	CPR: Content Protection Robustness
 3)	PKR: PlayReady Device Porting Kit Robustness
 4)	TEER: PlayReady Trusted Execution Environment (TEE) Robustness
 5)	TEEC: PlayReady Trusted Execution Environment (TEE) Compliance

### SL3000 Requirements for Intermediate Products Test Report – Check List

![PlayReady SL3000 IPL Design Report](../images/sl3000_design_report1.png)

| Requirement	| Underlying Rule | Title | Requirement | Testing Procedure(s) Overview & Resource Usage | Result |
| --- | --- | --- | --- | --- | --- |
| CA-1.1 | RR 2.2.1 | Product Design - TEE | PlayReady Product is clearly designed such that is uses a PlayReady Trusted Execution Environment (TEE). | Architecture Review and Code Review | - |
| CA-1.2 | RR 2.2.1 | Product Design - TEE | PlayReady Product only uses Content Protection Functions implemented by a PlayReady TEE. |  Architecture Review and Code Review | - |
| CA-2.1 | RR 2.2.2.1 | Decrypted Content | Decrypted A/V Content must not be readable or be placed outside the PlayReady Trusted Execution Environment.  Decrypted A/V Content must not be available to code running outside the PlayReady TEE | Architecture Review and Code Review. Penetration Tests under tools XYZ | - |
| CA-2.2 | RR 2.2.2.2 | Application Secrets | Application Secrets must not be available in contiguous cleartext memory except when in use to decrypt Content and/or keying material.  Application Secrets must not be available to code running outside the PlayReady Trusted Execution Environment. | Architecture Review and Code Review | - |
