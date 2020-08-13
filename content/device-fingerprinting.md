---
author: v-davido
description: This topic explains how to implement device fingerprinting based on artificial intelligence.

ms.author: v-davido
ms.service: fraud-protection
ms.date: 03/05/2020


ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Implement device fingerprinting
---

# Implement device fingerprinting

Microsoft Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI). This feature enables the identification of devices (computer, Xbox, tablet, and so on)  across multiple sessions or interactions that engage with your business and others’ in the fraud network. Additionally, this feature allows the service to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud. Device fingerprinting runs on Microsoft Azure. It's cloud-scalable, reliable, and provides enterprise-grade security.
When you implement Fraud Protection device fingerprinting by integrating the script on your online services, you direct Microsoft to collect the following types of data from the devices interacting with such services:

- Device attributes such as plugins installed, processor class etc.
- Operating system attributes, such as OS Information.
- Browser related attributes if applicable such as browser language, font etc.
- Network attributes, such as IP address, signature hash etc.


It is your responsibility to:

1. Inform your customers of your data processing practices, for example by disclosing the data you collect and how it is used. 
2. Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers. 
3. Comply with all laws and regulations applicable to its use of Fraud Protection, including data protection laws. 


The process of integrating device fingerprinting for Fraud Protection consists of the following tasks:

1. Set up Microsoft Azure DNS.
1. Integrate device fingerprinting with your website.

## Set up Azure DNS

1. Select a subdomain under your root domain. (For example, select **f.contoso.com**. Any prefix can be used.)
2. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

    **Example**

    - **Merchant website:** `www.contoso.com`
    - **DNS record:** `f.contoso.com`, which points to `fpt.dfp.microsoft.com`

3. For back-end onboarding, generate the Secure Sockets Layer (SSL) certificate for the selected subdomain.
4. To start the process of exchanging SSL certificates, contact <DFPHelp@microsoft.com>.

## Integrate device fingerprinting with your website or Application

Your website or application should enable the device fingerprinting before it submits a transaction (such as a transaction for adding a payment instrument, sign-in, or checkout). Follow these steps to integrate device fingerprinting with your website.

1. Insert a **script** on the webpage/application where you want collect device fingerprinting information    

    ```javascript
    <script src="https://fpt.<Your_Root_Domain>.com/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Root\_Domain** – The root domain of the merchant website.
    - **session\_id** – The unique session identifier of the device created by the merchant. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). Although we recommend that a globally unique identifier (GUID) be used for the session ID, this approach isn't required.
    - **instance\_id** – A placeholder for the instance ID that represents you. Use the instance identifier (**instance\_id** value) listed on the **Account Information** dashboard tile in the Dynamics 365 Fraud Protection Evaluate experience. You must have this value to integrate device fingerprinting with your website.

    **Example**

    ```javascript
    <script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here is an example of a response for mdt.js.

    ```javascript
   window.dfp={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};window.dfp.doFpt=function(doc){var frm,src;true&&(frm=doc.createElement("IFRAME"),frm.id="fpt_frame",frm.style.width="1px",frm.style.height="1px",frm.style.position="absolute",frm.style.visibility="hidden",frm.style.left="10px",frm.style.bottom="0px",frm.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px"),src="https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",frm.setAttribute("src",src),doc.body.appendChild(frm))};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```javascript
    window.dfp.doFpt(this.document);
    ```

3. When you submit transactions in the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services), complete the following actions:

    1. In the **deviceContextId** field, set a session ID.
    1. In the **deviceContextDC** field on the deviceContext object, set the window.dfp.dc variable from mdt.js response.
