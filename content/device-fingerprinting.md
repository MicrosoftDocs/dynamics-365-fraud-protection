---
author: jackwi111
description: This topic explains how to implement device fingerprinting.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 02/25/2019

ms.topic: conceptual
title: Implement device fingerprinting
---

# Implement device fingerprinting

Based on cutting-edge machine learning and artificial intelligence (AI), Microsoft Dynamics 365 Fraud Protection offers device fingerprinting. This feature enables the service to identify **devices** (not individuals) across multiple sessions or interactions that engage with your business. At the same time, it respects customer privacy.

By tracking elements that are related to a device (computer, Xbox, tablet, and so on), you can link individual devices to events. Therefore, device fingerprinting lets you link seemingly unrelated events to each other by capturing and identifying unique device characteristics during the processes for adding a payment instrument, sign-in, and checkout.

Device fingerprinting runs on Microsoft Azure. It's cloud-scalable and reliable, and provides enterprise-grade security. A major advantage that device fingerprinting has over similar products in the marketplace is that it's continually tested against the latest fingerprinting evasion tools that fraudsters use.

The process of integrating device fingerprinting for Dynamics 365 Fraud Protection consists of the following tasks:

- Set up Domain Name System (DNS).
- Integrate device fingerprinting with your website.

## Set up DNS

1. Select a subdomain under your root domain. (For example, select **f.contoso.com**. Any prefix can be used.)
2. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

    **Example**

    - **Merchant website:** `www.contoso.com`
    - **DNS record:** `f.contoso.com`, which points to `fpt.dfp.microsoft.com`

    > [!NOTE]
    > Use the instance identifier (**instance\_id** value) that is provided during the setup process for Dynamics 365 Fraud Protection. You must have this value to integrate device fingerprinting with your website.

3. For back-end onboarding, generate the Secure Sockets Layer (SSL) certificate for the selected subdomain.
4. To start the process of exchanging SSL certificates, contact <DFPHelp@microsoft.com>.

## Integrate device fingerprinting with your website

Your web application should serve the device fingerprinting before it submits a transaction (such as a transaction for adding a payment instrument, sign-in, or checkout). Follow these steps to integrate device fingerprinting with your website.

1. Insert a **script** element on the webpages where you will profile your user's devices.

    ```
    <script src="https://fpt.<Your_Root_Domain>.com/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Root\_Domain** – The root domain of the merchant website.
    - **session\_id** – The device user's session identifier. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). Although we recommend that a globally unique identifier (GUID) be used for the session ID, this approach isn't required.
    - **instance\_id** – A placeholder for the instance ID that represents you. This value is provisioned during the onboarding process for Dynamics 365 Fraud Protection.

    **Example**

    ```
    <script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here is an example of a response for mdt.js.

    ```javascript
    var a={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&
    CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",
    customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};a.doFpt=function(a)
    {var b=a.createElement("IFRAME");b.id="fpt_frame",b.style.width="1px",b.style.height="1px",
    b.style.position="absolute",b.style.visibility="hidden",b.style.left="10px",b.style.bottom="0px",
    b.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;
    left:-200;border:0px;display:none");var c="https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-
    fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691";b.setAttribute("src",c),a.body.appendChild(b)};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```
    a.doFpt(this.document);
    ```

3. When you submit transactions in the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services), complete the following actions:

    - In the **deviceContextId** field, set a session ID.
    - In the **deviceContextDC** field on the deviceContext object, set a.dc from mdt.js response.
