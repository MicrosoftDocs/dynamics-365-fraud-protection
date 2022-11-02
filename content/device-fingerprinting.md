---
author: josaw1
description: This article explains how to set up device fingerprinting in Microsoft Dynamics 365 Fraud Protection.

ms.author: josaw
ms.date: 11/02/2022
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up device fingerprinting
---

# Set up device fingerprinting

This article explains how to set up device fingerprinting in Microsoft Dynamics 365 Fraud Protection.

A *device fingerprint*, also known as a *machine fingerprint*, contains information that is collected about a remote computing device, such as a computer, Xbox, tablet, or smartphone, for the purpose of identifying that device. Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address.

Fraud Protection provides a device fingerprinting feature that is based on artificial intelligence (AI) so that device identification can be used as input to the process of fraud assessment. This feature helps the Fraud Protection service track and link seemingly unrelated events in the fraud network to help identify patterns of fraud. The data collected is not just a static list of attributes but also includes data that is dynamically captured based on the evaluation of specific combinations of attributes, such as browser, system, network, and geo-location attributes. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device.

Device fingerprinting runs on Azure, and includes benefits from proven cloud scalability, reliability, and enterprise-grade security. To help you better understand the impact that device fingerprinting has on fraud detection, this document includes some results from a study that Microsoft did. The study compared six months' worth of data for various Microsoft businesses through two different models: one that used device fingerprinting and one that did not.

In summary, the results showed that device fingerprinting has a significant positive impact on the model detection rate for all businesses. Because it reduces false negatives, less fraud is detected on approved transactions after the fact.

## Goals 

The purpose of this set up guide is to help you understand how you can: 

- Call the Fraud Protection device fingerprinting service. 
- Collect the required data and send it to Fraud Protection. 
- Include device fingerprinting session ID information in the subsequent risk assessment API call to Fraud Protection (for example, for an online purchase or new user account creation). 

## Prerequisites

Before you begin the tasks in this document, you must set up Fraud Protection in an Azure Active Directory (Azure AD) tenant, as described in [Set up a trial version of Fraud Protection](promocode-set-up-dfp-trial-version.md) and [Set up a purchased version of Fraud Protection](promocode-set-up-DFP-purchased-version.md).

It is your responsibility to:

1. Inform your customers of your data processing practices, for example by disclosing the data you collect and how it is used. 
2. Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers. 
3. Comply with all laws and regulations applicable to its use of Fraud Protection, including data protection laws. 

### Important notice regarding data collection

When you implement Fraud Protection device fingerprinting by integrating the script on your online services, you direct Microsoft to collect the following types of data from the devices interacting with such services:

- Device attributes such as plugins installed, processor class, etc.
- Operating system attributes, such as OS Information.
- Browser-related attributes if applicable such as browser language, font, etc.
- Network attributes, such as IP address, signature hash, etc.

## Set up device fingerprinting

To set up device fingerprinting, follow these steps.

1. Configure the DNS SSL certificate and upload it to the Fraud Protection portal.
1. Implement device fingerprinting (on web or mobile app). 

The sections below provide detailed instructions on these steps. Please note that the first step is only needed once, but the second step needs to be repeated once for each website or mobile app where device fingerprinting is to be enabled. 

### Step 1: Setup DNS and provide an SSL certificate

To set up DNS and provide an SSL certificate, follow these steps.

1. Select a subdomain under your root domain.For example, select **f.contoso.com**. Any prefix can be used.
2. For the selected subdomain, create a canonical name (CNAME) that points to **fpt.dfp.microsoft.com**.For example, **Merchant website**: www.contoso.com, **DNS record**: f.contoso.com, which points to fpt.dfp.microsoft.com.

To set up the Secure Sockets Layer (SSL) certificate, follow these steps.

1. For back-end onboarding, generate the SSL certificate for the selected subdomain. You can add all the subdomains in **Certificate’s Subject Alternative Name** and create one SSL Certificate.
2. Go to the Fraud Protection portal [portal](https://dfp.microsoft.com) and navigate to the **Integration** page from left hand menu. 
3. Select **Edit** and then select **Next** on the following page to reach the page titled Upload SSL certificate. 
4. Click **Select Certificate** button and upload the SSL Certificate generated in Step a) . If your certificate has a password, then enter it in the text box below and then select **Upload**. 

> [!NOTE]
> Only .pfx files are supported. It may take a few minutes for certificate to propagate to the device fingerprinting servers. 

## Step 2: Implement device fingerprinting

Your website or application needs to initiate device fingerprinting requests a few seconds before a transaction is sent to Fraud Protection for risk evaluation (such as a transaction for adding a payment instrument, sign-in, or checkout). This would ensure that Fraud Protection has received all the data necessary to make an accurate assessment. The below sections provide detailed instructions to enable device fingerprinting on websites and mobile Apps. 

Follow these steps on your website.

- Insert a **javascript** on the webpage/application where you want collect device fingerprinting information.   

    ```JavaScriptCopy
    <script src="https://fpt.<Your_Sub_Domain>.com/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Root\_Domain** – The root domain of the merchant website.
    - **session\_id** – The unique session identifier of the device created by the merchant. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). Although we recommend that you use a globally unique identifier (GUID) for the session ID, this approach isn't required.
    - **instance\_id** – A placeholder for the instance ID that represents you. Use the instance identifier (**instance\_id** value) listed on the **Account Information** dashboard tile in the Dynamics 365 Fraud Protection evaluate experience. You must have this value to integrate device fingerprinting with your website.

    **Example**

    ```JavaScriptCopy
    <script src="https://Your_Sub_Domain/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here is an example of a response for mdt.js.

    ```JavaScriptCopy
   window.dfp={url:"https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};window.dfp.doFpt=function(doc){var frm,src;true&&(frm=doc.createElement("IFRAME"),frm.id="fpt_frame",frm.style.width="1px",frm.style.height="1px",frm.style.position="absolute",frm.style.visibility="hidden",frm.style.left="10px",frm.style.bottom="0px",frm.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px"),src="https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",frm.setAttribute("src",src),doc.body.appendChild(frm))};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```JavaScriptCopy
    window.dfp.doFpt(this.document);
    ```

3. When you submit transactions in the Dynamics 365 Fraud Protection API, set a session ID in the **deviceContextId** field.
4. Set the **'device.ipAddress'** field to the customer IP address that your website receives when the customer uses your site.

## To enable fingerprinting on a mobile app: 

For mobile apps, device fingerprinting integration supports Android, iOS and React Native platforms via SDK integration. You can learn more about the mobile reference implementation in the following documents:  

- [Dynamics 365 Fraud Protection mobile SDK for Android](mobile-sdk-android.md) 
- [Dynamics 365 Fraud Protection mobile SDK for iOS](mobile-sdk-ios.md) 
- [Dynamics 365 Fraud Protection mobile SDK for React Native](mobile-sdk-react-native.md)

## Mobile device fingerprinting

You can learn more about the mobile reference implementation in [Dynamics 365 Fraud Protection mobile SDK for Android](mobile-sdk-android.md) and [Dynamics 365 Fraud Protection mobile SDK for iOS](mobile-sdk-ios.md).

## Additional resources

[Implement device fingerprinting in Dynamics 365 Fraud Protection](/training/modules/device-fingerprint-fraud-protection/).

[!INCLUDE[footer-include](includes/footer-banner.md)]
