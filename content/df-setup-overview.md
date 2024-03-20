---
author: josaw1
description: This article describes how to set up and implement device fingerprinting in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/20/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Set up and implement device fingerprinting
---

# Set up and implement device fingerprinting

The setup of device fingerprinting is done in two phases.

1. Configure the Domain Name Server (DNS) Secure Sockets Layer (SSL) certificate, and upload it to the Fraud Protection portal.
1. Implement device fingerprinting (on a website or a mobile app).

This section provides detailed instructions for both these phases. The first phase has to be completed only once. However, the second phase must be repeated once for each website or mobile app where device fingerprinting is implemented.

## Set up DNS and generate an SSL certificate

Complete the following procedures to set up DNS and generate an SSL certificate.

### Set up DNS

To set up DNS, follow these steps.

1. Select a subdomain under your root domain, such as `fpt.contoso.com`. Any prefix can be used.
1. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

### Generate and upload an SSL certificate

To generate and upload an SSL certificate, follow these steps.

1. For back-end onboarding, generate the SSL certificate for the selected subdomain. You can create one SSL certificate and add all the subdomains in the **Certificate's Subject Alternative Name** field.
2. Go to the [Fraud Protection portal](https://dfp.microsoft.com), and then, in the left navigation pane, select **Integration**.
3. On the **Integration** page, select **Edit**, and then, on the next page, select **Next** to open the **Upload SSL certificate** page.
4. Select **Select Certificate**, and then upload the SSL certificate that you generated. If your certificate has a password, enter it in the text box. Then select **Upload**.

> [!NOTE]
> Only .pfx files are supported. Propagation of the certificate to the device fingerprinting servers might take a few minutes. 

## Implement device fingerprinting

Your website or application must initiate device fingerprinting requests a few seconds before a transaction is sent to Fraud Protection for risk evaluation (such as a transaction for adding a payment instrument, sign-in, or checkout). This requirement ensures that Fraud Protection receives all the data that it requires to make an accurate assessment. This section provides detailed instructions for implementing device fingerprinting on websites and mobile apps. 

To implement device fingerprinting, follow these steps.

1. Modify the following JavaScript script code, and insert it on the webpage or in the application where you want to collect device fingerprinting information.

    ```JavaScript
    <script src="https://<Your_Sub_Domain>/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Sub\_Domain** – The subdomain under your root domain.
    - **session\_id** – The unique session identifier of the device that was created by the client. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). The session ID should contain at least 16 bytes of randomly generated data. When using hexadecimal encoding, this translates to 32 hexadecimal characters. Although Microsoft recommends that you use a globally unique identifier (GUID) for the session ID, it isn't required.
    - **instance\_id** – This is a required value to integrate your website with device fingerprinting. Use the **Device fingerprinting ID** value that's listed on the **Current environment** tile on the **Integration** page of the corresponding environment in the Fraud Protection portal.

    **Example**

    ```JavaScript
    <script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here's an example of a response for mdt.js.

    ```JavaScript
    window.dfp={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};window.dfp.doFpt=function(doc){var frm,src;true&&(frm=doc.createElement("IFRAME"),frm.id="fpt_frame",frm.style.width="1px",frm.style.height="1px",frm.style.position="absolute",frm.style.visibility="hidden",frm.style.left="10px",frm.style.bottom="0px",frm.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px"),src="https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",frm.setAttribute("src",src),doc.body.appendChild(frm))};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```JavaScript
    window.dfp.doFpt(this.document);
    ```

3. When you submit transactions in the Fraud Protection API, set a session ID in the **deviceContextId** field. For Assessments, set a session ID in the **deviceFingerprinting.id** field.
4. Set the **device.ipAddress** field to the customer IP address that your website receives when a customer uses your site. For Assessments, set the customer IP address in the **deviceFingerprinting.ipAddress** field. This field is optional and doesn't need to be set if you don't have it.
