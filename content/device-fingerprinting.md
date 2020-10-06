---
author: yvonnedeq
description: This topic explains how to implement device fingerprinting based on artificial intelligence.

ms.author: v-madeq
ms.service: fraud-protection
ms.date: 10/08/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Implement device fingerprinting
---

# Implement device fingerprinting

Microsoft Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI). This feature enables the identification of devices (computer, Xbox, tablet, and so on)  across multiple sessions or interactions that engage with your business and others' in the fraud network. Additionally, this feature allows the service to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud. Device fingerprinting runs on Microsoft Azure. It's cloud-scalable, reliable, and provides enterprise-grade security.
When you implement Fraud Protection device fingerprinting by integrating the script on your online services, you direct Microsoft to collect the following types of data from the devices interacting with such services:

- Device attributes such as plugins installed, processor class etc.
- Operating system attributes, such as OS Information.
- Browser-related attributes if applicable such as browser language, font etc.
- Network attributes, such as IP address, signature hash etc.


It is your responsibility to:

1. Inform your customers of your data processing practices, for example by disclosing the data you collect and how it is used. 
2. Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers. 
3. Comply with all laws and regulations applicable to its use of Fraud Protection, including data protection laws. 


The process of integrating device fingerprinting for Fraud Protection consists of the following tasks:

1. Set up Microsoft DNS.
1. Integrate device fingerprinting with your website.

## Set up DNS

1. Select a subdomain under your root domain. (For example, select **f.contoso.com**. Any prefix can be used.)
2. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

    **Example**

    - **Merchant website:** `www.contoso.com`
    - **DNS record:** `f.contoso.com`, which points to `fpt.dfp.microsoft.com`

3. For back-end onboarding, generate the Secure Sockets Layer (SSL) certificate for the selected subdomain.
4. To start the process of exchanging SSL certificates, contact <DFPHelp@microsoft.com>.

## Integrate device fingerprinting with your website or application

Your website or application should enable the device fingerprinting before it submits a transaction (such as a transaction for adding a payment instrument, sign-in, or checkout). Follow these steps to integrate device fingerprinting with your website.

1. Insert a **script** on the webpage/application where you want collect device fingerprinting information.   

    ```javascript
    <script src="https://fpt.<Your_Sub_Domain>.com/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Root\_Domain** – The root domain of the merchant website.
    - **session\_id** – The unique session identifier of the device created by the merchant. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). Although we recommend that you use a globally unique identifier (GUID) for the session ID, this approach isn't required.
    - **instance\_id** – A placeholder for the instance ID that represents you. Use the instance identifier (**instance\_id** value) listed on the **Account Information** dashboard tile in the Dynamics 365 Fraud Protection Evaluate experience. You must have this value to integrate device fingerprinting with your website.

    **Example**

    ```javascript
    <script src="https://Your_Sub_Domain/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here is an example of a response for mdt.js.

    ```javascript
   window.dfp={url:"https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};window.dfp.doFpt=function(doc){var frm,src;true&&(frm=doc.createElement("IFRAME"),frm.id="fpt_frame",frm.style.width="1px",frm.style.height="1px",frm.style.position="absolute",frm.style.visibility="hidden",frm.style.left="10px",frm.style.bottom="0px",frm.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px"),src="https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",frm.setAttribute("src",src),doc.body.appendChild(frm))};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```javascript
    window.dfp.doFpt(this.document);
    ```

3. When you submit transactions in the [Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection), set a session ID in the **deviceContextId** field.
4. Set the **'device.ipAddress'** field to the customer IP address that your website receives when the customer uses your site.

> [!NOTE]
> You can learn more about the Mobile Reference Implementation in the [DFP Mobile Reference Implementation Document](https://go.microsoft.com/fwlink/?linkid=2132646). A login is required.

## Verify device fingerprinting

1. Send a transaction, sign-up, sign-in, or other item to the Dynamics 365 Fraud Protection API. Include the device fingerprinting **deviceContextID** value.
2. Visit the [Fraud Protection portal](https://dfp.microsoft.com/).
3. In the left navigation, select **Graph Explorer**.
4. Search for the transaction, sign-up, sign-in, or other item that you submitted.
5. In the chart, select the **DeviceContext** node.
6. In the right pane, verify the additional details about your device (for example, the **UserAgent** value and operating system version).

    If you see additional details beyond what was submitted in the API call, you've set up device fingerprinting correctly.

