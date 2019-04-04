---
author: jackwi111
description: Adopt and integrate device fingerprinting
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Adopt and integrate device fingerprinting
---


# Implement device fingerprinting

Based on cutting-edge machine learning and artificial intelligence, Dynamics 365 Fraud Protection offers device fingerprinting. This feature enables the service to identify the **devices** (not individuals) across multiple sessions or interactions that engage with your business, all while respecting customer privacy. By tracking elements related to a device (computer, Xbox, tablet, and so on), you can link individual devices to events. Using device fingerprinting, you can link seemingly unassociated events to each other by capturing and identifying unique device characteristics during the Add PI, sign in, or checkout processes.

Device fingerprinting runs on Azure. It is cloud-scalable, reliable, and provides enterprise-grade security. A major advantage over similar products in the marketplace is that device fingerprinting is being continually tested against the latest fingerprinting-evasion fraudster tools.

Integrating device fingerprinting for Dynamics 365 Fraud Protection consists of:

- Provisioning DNS
- Integrating with your website

## Set up DNS

1.	Choose a subdomain under your root domain (for example, f.contoso.com - can be any prefix).
1. Create a Canonical Name (CNAME) for your subdomain pointing to fpt.dfp.microsoft.com.

*Example*

Merchant website: www.contoso.com (this link is not live and meant for illustration only)

DNS record: f.contoso.com points to fpt.dfp.microsoft.com

[!NOTE]
Use the instance identifier (instance_id) provided during Dynamics 365 Fraud Protection setup process. Without this instance_id, you cannot integrate with device fingerprinting.

2.	For backend onboarding, provide the SSL certificate for this subdomain to the Dynamics 365 Fraud Protection team.

## Integrate device fingerprinting with your website

Your web application should serve the device fingerprinting before submitting a transaction (such as Add PI, checkout, or sign-in). Follow these steps to integrate device fingerprinting with your website.

1.	Insert a script tag on the web pages where you will profile your user’s devices.

```<script src="https://fpt.<Your_Root_Domain>.com/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>```

- Your_Root_Domain: Merchant website root domain.
- instance_id: Placeholder for the instance ID representing you. This will be provisioned during the Dynamics 365 Fraud Protection onboarding process.
- session_id: Device user’s session identifier. It can be up to 128 characters long and can only contain the following characters: upper and lowercase English letters, digits, underscore or hyphen ([a-z], [A-Z], 0-9, _, -). Using the GUID is suggested for the session ID, but not required.

*Example*

```<script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>```

Sample response for mdt.js

```var a={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};a.doFpt=function(a){var b=a.createElement("IFRAME");b.id="fpt_frame",b.style.width="1px",b.style.height="1px",b.style.position="absolute",b.style.visibility="hidden",b.style.left="10px",b.style.bottom="0px",b.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px;display:none");var c="https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691";b.setAttribute("src",c),a.body.appendChild(b)};```

2. Load device fingerprinting after the page elements are loaded.

    a.doFpt(this.document);

3. When submitting transactions in the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services), do the following:
 - Set session ID in **deviceContextId** field.
 - Set a.dc from mdt.js response in the **deviceContextDC** field on the deviceContext object.

