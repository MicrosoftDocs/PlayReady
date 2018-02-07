---
author: rolandlefranc
title: License and Policies
description: During license acquisition, the Client sends a challenge to the PlayReady License Server containing the content header and information about the user's device.
ms.assetid: "BD5E39E2-20B2-42A5-9D4F-D109DD4E67DE"
keywords: playready license, policy, policies
ms.author: rolefran
ms.topic: conceptual
ms.prod: playready
ms.technology: drm
---


# License and Policies

During license acquisition, the Client sends a challenge to the PlayReady License Server containing the content header and information about the user's device. Once the challenge is received by the PlayReady License Server, the Server parses the challenge and begins to populate the license response. The response will include the content key (CK) originally used to encrypt the content that corresponds to the key identifier (KID) sent in the license challenge, or several of them. In addition, the license response will return the PlayReady policies (rights and restrictions) under which the content can be played. 

![License Request and Response](../images/license_request_response.png)

A PlayReady policy describes the actions permitted and/or required with respect to PlayReady content and restrictions on those actions as described in the PlayReady license associated with the PlayReady content. PlayReady policies are defined in the PlayReady Compliance Rules (CR). The service provider must incorporate the mandatory policies and choose which of the optional policies to use, and have these policies integrated into the license handler on the PlayReady License Server. These policies can be rights, such as the Play right, or restrictions, such as the Minimum Security Level, Output Protection Level, expiration after first play, and so on. 

Note that a license response may contain multiple licenses. Each license contains one and only one Content Key {KID, CK} and a set of associated policies.
 
When the Client receives the license response from the PlayReady License Server, it must be able to parse the content key and the policies sent back in the licenses it receives. The PlayReady Client must be able to follow the policies sent in the license response and play back content if all the mandatory policies are met, or halt play back if any of the mandatory policies are not met. 

>[!NOTE]
>If the Client supports PlayReady Device Porting Kit v3.0 and higher, the PlayReady License Server will not provide a license that requires the Copy, Execute, or Read rights.

For more information about PlayReady policies, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) and the [Defined Terms for PlayReady Compliance and Robustness Rules](https://www.microsoft.com/playready/licensing/compliance/). 

## PlayReady Rights

The following PlayReady rights are listed in the PlayReady Compliance Rules:

  *  Play right (see CR 3.1): right for a Client to decrypt PlayReady Audio/Video content (movies and music), render it, and pass it to Outputs. 
  *  Execute right (see CR 4.1): right for a Client to decrypt PlayReady Executable content (applications), and execute it. No longer supported in PlayReady 3.0 and later. 
  *  Read right (see CR 5.1): right for a Client to decrypt PlayReady Literary content (ebooks), and display it. No longer supported in PlayReady 3.0 and later. 

## Rights Restrictions and other Policies

The PlayReady Compliance Rules contain a full list of right modifiers (extensions and restrictions) that may apply to the license. Each of these modifiers has multiple properties:
 
  *  **Action**&mdash;specifies the action of the policy (for example, engage HDCP encryption on the HDMI output). 
  *  **Optional**&mdash;specifies if the Client must engage the action or must try to engage the action (for example, Output Control for Uncompressed Digital Video Content 250, see CR 3.6.5).
  *  **Must Understand**&mdash;specifies if a Client is allowed to bind a license and decrypt content even if it does not understand the policy. Applicable for Clients of a lower version (for example, a PlayReady 2.X Client) receiving a license including PlayReady policy introduced in a future version (for example, a PlayReady 3.X Server, see CR 2.4).
  *  **Best Effort**&mdash;another way to specify if the Client must engage the action or must try to engage the action (for example, Macrovision Best Effort, see CR 2.4).

The following sections list some of the more commonly used right modifiers.

### Absolute Expiration Policy

One of the common restrictions is the absolute time date expiration policy. Every license may include an absolute time date expiration policy. If it is present, the Client must stop binding this license and decrypting content if the current date time is after that value.

A practical example is a user on a Client playing content from a monthly subscription service. The monthly renewal day of the service for this user is the 15th of the month. The user starts playback on the 2nd of the month (the 2nd of November, 2017). The License Server will give the right to the user until the 15th of the month, and include an Expiration policy set to 11/16/2017, 0:00am. Whenever the user pays the subscription fee for the next month, the service will issue another license with an Expiration date set one month later. 

This policy is by definition a Must Understand and Mandatory (meaning, not Best Effort) policy, so a Client that binds a license that includes this policy MUST: 

  *  Have a PlayReady Trusted Clock System to have a trusted time. A PlayReady Secure Clock or a PlayReady Anti-Rollback Clock are two acceptable forms of PlayReady Trusted Clock Systems for PlayReady Clients.
  *  Have this PlayReady Trusted Clock set.
  *  Be able to parse and understand the Expiration policy in the license.
  *  Compare the current time from the PlayReady Trusted Clock System with the Expiration value.
  *  Not bind the license if the current time is past the Expiration value. 
 
>[!NOTE]
>Whenever a License Server sets an Absolute Expiration policy in a license, Microsoft strongly recommends that a Begin Date policy also be set, for Robustness Reasons. See [Best Practices for License Policies](policies-best-practices.md) for more details.

### Begin Date Policy 

Another common restriction is the begin date policy. If it is present, the Client must not bind this license and begin decrypting content until the current date time is after that value.

For business models that require content to be used only for a limited amount of time, such as in a rental scenario, an end date is required to indicate when the license expires and the content can no longer be played (for example, the content can only be played until 5pm EST, May 15, 2018). This is sufficient for a rental scenario. However, specifying a begin date with the end date is a natural impedance to clock rollback attacks.

This policy is by definition a Must Understand and Mandatory (meaning, not Best Effort) policy, so a Client that binds a license that includes this policy MUST: 

  *  Have a PlayReady Trusted Clock System to have a trusted time. A PlayReady Secure Clock or a PlayReady Anti-Rollback Clock are two acceptable forms of PlayReady Trusted Clock Systems for PlayReady Clients.
  *  Have this PlayReady Trusted Clock set.
  *  Be able to parse and understand the Begin Date policy in the license.
  *  Compare the current time from the PlayReady Trusted Clock System with the Begin Date value.
  *  Not bind the license if the current time is before the Begin Time value.

For more information, see [Using BeginDate with EndDate](policies-best-practices.md#begindate) 

### Expiration After First Play Policy 

Besides scenarios in which content can be played back depending on a begin time and end time, there is also the model that specifies how long content can be played back after the content is first played. The expiration after first play policy, if present, indicates that the Client must stop binding this license and decrypting content if the current number of seconds after the content was first played matches the value in this policy.

> [!NOTE]
> For content that was purchased to own, users expect the content to play indefinitely on their devices. Services would most likely issue licenses for this content with no expiration at all. However, because users change devices frequently, and because each device may change its PlayReady identity some time (when a re-individualization is run, or when a device is completely reinstalled), services should be ready at any time to re-issue licenses for purchased content that was previously delivered to a user or a device.


### Security Level Policy

PlayReady Clients all have a property set in their Unit-level Client Certificate called the Client Security Level. When a License Server sends a license to a Client, it includes in the license the MinimumSecurityLevel policy and sets its value to 150, 2000, or 3000. This value means that the license can be bound and content can be decrypted only on Clients that have this Security Level, or a higher one.

See the [Client Security Level](security-level.md#securitylevelpolicy) page for more information about that policy.

### Output Control for Uncompressed Digital Video Content Policy 

A service may want to allow a Client to decrypt and render content, but restrict how it flows to external outputs, like HDMI outputs. The service may want to do this because there might be recorders plugged to the HDMI cable, capable of making a very good copy of the original content.

PlayReady has all sorts of Output Protection controls for analog, digital, and wireless outputs. One of the most common is the HDCP policy for HDMI outputs (see CR 3.6.5). Depending on the value the License Server sets for this policy, which may be 100, 250, 270, 300 (see CR 6.7), the Client must try to engage, or must engage HDCP on the HDMI outputs when playing back on these outputs. 

For example, if the license includes an Output Control for Uncompressed Digital Video Content set to 300 (also known as Digital Video OPL 300), the Client MUST engage HDCP on the HDMI output when playing content. If the Client cannot engage HDCP (any version) on an HDMI output, it has two options: 

  *  Play content and block this output. For example, play on an internal screen or on an analog output, but block the signal on the HDMI output. 
  *  Just not play the content. If the device has an internal screen, an analog output, and an HDMI output, blocking the playback on all outputs just because the device can’t engage HDCP on the HDMI output would certainly be a suboptimal user experience. The user may ask “why does it not play on the analog output although the restriction only applies to the HDMI output?”. However, this option is acceptable from a PlayReady Compliance perspective as it fulfills the CR&RRs.

Note that HDCP Type 1 is supported starting with HDCP version 2.1, so engaging HDCP Type 1 won’t be possible on devices that support only HDCP 2.0 or 1.4.

### Other Policies 
PlayReady supports dozens if not hundreds of different policies beyond the ones described on this page. Please read the [Compliance Rules for PlayReady Products](https://www.microsoft.com/playready/licensing/compliance/) for the complete definition of the supported policies.


## XMR Specification 

PlayReady licensed companies have access to a more comprehensive documentation package that includes the *PlayReady Extensible Media Rights (XMR) Specification* that describes precisely each of these policies and the way they’re coded in a license. 

## See also

[Licenses Restricted by Binding Policy](licenses-restricted-by-binding-policy.md)

[Licenses Restricted by Extensible Policy](licenses-restricted-by-extensible-policy.md)