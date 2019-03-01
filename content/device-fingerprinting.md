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

Device Fingerprinting is a Microsoft-developed, anti-fraud system to identify unique devices across multiple sessions or interactions with Microsoft services. By tracking elements related to a device (computer, Xbox, tablets, and so on), you can link individual fraudsters to events. In most cases, fraudsters are unlikely to use a unique device for each unique payment instrument (PI) involved in an attempted fraud. 

Device Fingerprinting technology detects variables not previously recorded within the risk decision engine. With this optimization, Device Fingerprinting can better identify fraudulent behavior, and link seemingly unassociated events to each other by capturing and identifying unique device characteristics during the Add PI, log in, sign in, or checkout processes.

Integrating Device Fingerprinting for Dynamics 365 Fraud Protection consists of:

- Provisioning DNS
- Integrating with your website


## Provision DNS

1.	Create a Canonical Name (CNAME) for fpt.Your_Root_Domain.com pointing to fpt.dfp.microsoft.com.

*Example*

Merchant website: [Contoso](http://www.contso.com)
DNS record: fpt.contso.com points to fpt.dfp.microsoft.com

2.	For backend onboarding, inform the Dynamics 365 Fraud Protection team about your root domain. (fpt.Your_Root_Domain.com will be added to the SSL certificate managed by Microsoft.)

## Integrate Microsoft Device Fingerprinting with your website

Your web application should serve the Device Fingerprinting before submitting a transaction (such as Add PI, Checkout, or Sign-in). Follow these steps to integrate Device Fingerprinting with your website.

1.	Insert a script tag on the web pages where you will profile your user’s devices.

```<script src="https://fpt.<Your_Root_Domain>.com/mdt.js?session_id=<session_id>&customerId=<customer_id>" type="text/javascript"></script>```

- Your_Root_Domain: Merchant website root domain.
- customer_id: Placeholder for the customer ID representing you. This will be provisioned during Dynamics 365 Fraud Protection onboarding process.
- session_id: Device user’s session identifier. It can be up to 128 characters long and can only contain the following characters: upper and lowercase English letters, digits, underscore or hyphen ([a-z], [A-Z], 0-9, _, -). GUID is wise choice for session ID although session ID doesn’t have to be GUID.

*Example*

```<script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&customerId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>```

Sample response for mdt.js

```var a={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};a.doFpt=function(a){var b=a.createElement("IFRAME");b.id="fpt_frame",b.style.width="1px",b.style.height="1px",b.style.position="absolute",b.style.visibility="hidden",b.style.left="10px",b.style.bottom="0px",b.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px;display:none");var c="https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691";b.setAttribute("src",c),a.body.appendChild(b)};```

2. Load device fingerprinting after the page elements are loaded.

    a.doFpt(this.document);

3. When submitting transactions in the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/), set the session ID in deviceContextId field, and set a.dc from mdt.js response in the deviceContextDC field on the deviceContext object for the Purchase API.

