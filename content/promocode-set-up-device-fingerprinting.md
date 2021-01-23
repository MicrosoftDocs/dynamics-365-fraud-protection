---
author: yvonnedeq
description: This topic describes how to set up device fingerprinting in Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 01/22/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Implement device fingerprinting
---

# Implement device fingerprinting

## Overview

A *device fingerprint*, also known as a *machine fingerprint*, contains information that is collected about a remote computing device, such as a computer, Xbox, tablet, or smartphone, for the purpose of identifying that device. Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address.

Microsoft Dynamics 365 Fraud Protection (Fraud Protection) provides a device fingerprinting feature that is based on artificial intelligence (AI). Therefore, device identification can be used as input to the process of fraud assessment. Additionally, this feature helps the Fraud Protection service track and link seemingly unrelated events in the fraud network, to help identify patterns of fraud. The data that is collected isn't just a static list of attributes but also includes data that is dynamically captured based on the evaluation of specific combinations of attributes, such as browser, system, network, and geo-location attributes. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device.

Device fingerprinting runs on Azure, and includes benefits from proven cloud scalability, reliability, and enterprise-grade security. To help you better understand the impact that device fingerprinting has on fraud detection, this document includes some results from a study that Microsoft did. The study compared six months' worth of data for various Microsoft businesses through two different models: one that used device fingerprinting and one that didn't.

In summary, the results showed that device fingerprinting has a significant positive impact on the model detection rate for all businesses. Because it reduces false negatives, less fraud is detected on approved transactions after the fact.

## Goals for this document

The purpose of this document is to help you complete the following steps in your own system and with your own data:

- Map a customer's journey to a risk assessment action (for example, a checkout process or an account creation page) by making a device fingerprinting call to trigger a profiling service. This call includes a Fraud Protection customer-defined session ID and customer ID.
- Receive a response from the profile service. This response includes a list of device data that Fraud Protection should collect from the event.
- Run the device fingerprinting script, collect the required information, and send it to Fraud Protection.
- Assess this user's transactions for fraud, make the appropriate assessment API call, and pass the session ID to Fraud Protection.
- Fraud Protection then associates the captured device fingerprint information with the transaction that is being assessed.

## Prerequisites

Before you begin the tasks in this document, you must set up Fraud Protection in an Azure Active Directory (Azure AD) tenant, as described in [Set up a trial version of Fraud Protection](https://microsoft.sharepoint.com/:w:/t/DynDoc/EfPwl9fixxFMqGQS4HFNWD0BbK4Nqbs86YMozJ14nE_uPw?e=HfnVYC).

## How device fingerprinting affects your business

### Example 1: Cloud computing service

(image)

- Figure 1.1 shows that device fingerprinting contributed an impact of about 25.14 percent for this business, compared to an identical model that didn't use device fingerprinting (shown by the dotted line).
- Figure 1.2 shows that the model that uses device fingerprinting features can detect fraud at a false positive rate of 1 percent.
- The impact of device fingerprinting on the false negative rate can help reduce fraud.

### Example 2: Retail service

(image)

- Figure 2.1 shows that device fingerprinting contributes 15.32 percent of the total information in an assessment, compared to the same model that doesn't use device fingerprinting (shown by the dotted line).
- Figure 2.2 shows that the model that uses device fingerprinting can detect more fraud at a false positive rate, compared to the same model that doesn't use device fingerprinting.
- The impact of device fingerprinting on the false negative rate can help reduce fraud.

### Example 3: Online advertising service

(image)

- Figure 3.1 shows that device fingerprinting contributes 6.79 percent of the total information in an assessment, compared to the same model that doesn't use fingerprinting (shown by the dotted line). 
- Figure 3.2 shows that, at a false positive rate of 0.2 percent, the model that uses device fingerprinting can detect 4.34 percent more fraud than the same model that doesn't use device fingerprinting.
- The impact of device fingerprinting on the false negative rate can help reduce fraud.

### Collect and store device information

The device fingerprinting collects device information and then associates that information to a transaction. The system goes through the following multi-step process:

1.	On a page in the customer's journey to a risk assessment action (for example, a check out process or account creation page), a device fingerprinting call is made to trigger a profiling service. This call includes a Fraud Protection customer-defined session ID and customer ID.
2.	The profile service responds with a list of information that the device data Fraud Protection should collect from the event.
3.	The device fingerprinting script runs, collects the required information, and sends it to Fraud Protection.
4.	When it's time to assess this user's transactions for fraud, the Fraud Protection customer makes the appropriate assessment API call and passes the session ID to Fraud Protection. Fraud Protection then associates the captured device fingerprint information with the transaction being assessed.

The following screenshot shows the device fingerprinting call sequence.

(image)

The system receives this information and adds it to the graph in near-real-time.

**To view this information in a graph:**

- While you're viewing a transaction in the Fraud Protection graph explorer, select the **DeviceContext Node** pane.

(image)

## Deploy device fingerprinting in your system

Here are the six steps that you follow in Fraud Protection to deploy device fingerprinting in your system:

Step 1: Map the customer's journey.

Step 2: Identify where device fingerprinting calls should be placed.

Step 3: Set up Azure DNS for device fingerprinting.

Step 4: Add device fingerprinting calls to the pages that are being monitored.

Step 5: Confirm that Fraud Protection is receiving fingerprint information.

Step 6: Check for latency throughout the system.

### Step 1: Map the customer's journey

There are two primary scenarios where a customer can use device fingerprinting: for purchase protection and foraccount protection. In both cases, there are two implementation methods, depending on what is being protected:

- When a *web-based portal (e-commerce)* is being protected, Fraud Protection sends device fingerprinting information via a JavaScript tag.
- When a *mobile app-based portal (m-commerce)* is being protected, Fraud Protection sends API calls to the device fingerprinting software development kit (SDK).

To determine where device fingerprinting should be deployed, develop a customer *journey map*. The journey map shows the following information:

- Where critical information is collected during a customer's engagement
- When API calls are made to assess risk

A typical customer journey map might resemble the following illustration.

(image)

Note: To develop your own experience, map a customer environment that you're familiar with.

### Step 2: Identify where device fingerprinting calls should be placed

Next, use the journey map from the previous step and the following guidance to identify where device fingerprinting calls should be placed.

- Identify pages where critical actions are occurring.

  - These pages might include, for example, payment information, checkout, sign-up, and sign-in pages, and any page where there is a reasonably long dwell time (longer than five seconds, if possible).
  - If the dwell time on a candidate page is shorter, select an earlier page in the user flow. Keep in mind that traffic on earlier pages might have a higher drop-off rate.

- Implement device fingerprinting calls before risk assessment calls are made.

  - In this way, you ensure that the risk assessment activity uses fingerprinting information.

- The following pages are recommended for fingerprint tagging:

   - The checkout page for purchase protection   
   - The sign-up or sign-in page for account protection

#### Example

Use the sample journey map from step 1 to identify the best pages for the device fingerprinting calls. The following illustration shows our recommendation.

(image)

### Step 3: Set up Azure DNS for device fingerprinting

Although you can use any system for Domain Name System (DNS) management, this document uses Azure DNS.

1.	Select a subdomain under your root domain.

    You can use any prefix, for example, select **f.contoso.com**.

2.	For the selected subdomain, create a canonical name (CNAME) that points to **fpt.dfp.microsoft.com**. For example:

    - Merchant website: **www.contoso.com**
    - DNS record: f.contoso.com, which points to > #fpt.dfp.microsoft.com#

3.	Generate the Secure Sockets Layer (SSL) certificate for the selected subdomain. 
4.	To start the process of exchanging SSL certificates, contact [Fraud Protection Help@microsoft.com](mailto:Fraud%20Protection%20Help@microsoft.com).

### Step 4: Add device fingerprinting calls to the pages that are being monitored

Next, add calls to the sample application.

1.	On the server side, construct the fingerprinting tag as shown in the following example:

    URI: https://ftp.contoso.com/mdt.js?session_id=<guid>&instanceId=<tenantId>&pageId=<ID>

| URI parameter	 | Supported values |
|----------------|------------------|
| session_id 	   | A globally unique identifiable string, usually a globally unique identifier (GUID) |
| instanceId 	   | The Azure AD tenant ID (GUID)    |
| pageId         | <p>SI – Sign In</p><p>SU – Sign Up</p><p>P – Purchase</p><p>tst – Test</p>       |

2.	On the server side, construct the fingerprinting tag as shown in the following example:

    <script src="https://ftp.contoso.com/mdt.js?session_id=20270d15-d27f-4a77-b94f-4df46be5c540&instanceId=80d509fb-a258-449a-9c06-a2c550a40b17&pageId=P" type="text/javascript"></script>

  	The system returns a response that resembles the following sample mdt.js call:

(image)

3.	After the page is completely loaded, call the fingerprinting code as shown in the following example:

    window.dfp.doFpt(this.document);

4.	In the Fraud Protection API, submit transactions that include the following information:

    - In the **deviceContextId** field, set a session ID.
    - In the **deviceContextDC** field on the **deviceContext** object, set the **window.dfp.dc** variable from **mdt.js response**.

### Step 5: Confirm that Fraud Protection is receiving fingerprint information

There are two ways to check whether your device fingerprinting implementation is successful:

- When you implement device fingerprinting on a webpage, you will see a response for the mdt.js call. If the response is empty, at least one parameter isn't valid. Try again.
- For customers who use purchase protection, if device fingerprinting is correctly implemented, the values of portal device attributes will start to fill in the **DeviceContext** node in Fraud Protection, as shown in the following screenshot.

(image)

#### Troubleshooting tips

If you're having trouble determining whether your device fingerprinting calls are successful, try these steps:

1.	Check for any network issues that might be blocking the communication. For example, check the firewall configuration.
2.	Make sure that you inject a new session ID on each fingerprinting call.

     - When an assessment call is sent to Fraud Protection, the same session ID must also be sent, so that the two session IDs can be matched.
     - When a match occurs, Fraud Protection uses the information that > device fingerprinting gathered in the risk assessment.

If you're still having trouble after trying these steps, contact your Microsoft representative, or email [dfphelp@microsoft.com](mailto:dfphelp@microsoft.com).

### Step 6: Check for latency throughout the system

Most Fraud Protection customers are concerned that incremental latency might affect end-to-end transaction speed. Check your system to make sure that significant latency hasn't inadvertently been introduced. We recommend that you check the latency between the following events:

- The initial page load (fully hydrated) 
- The fingerprint tagging request
- User selection of the Submit or Purchase button


We also strongly recommend that you reuse SSL connections to help avoid additional latency.

(image)

Congratulations! You've successfully completed the training and are ready to use your free trial of Fraud Protection's device fingerprinting capabilities.

## Next steps

For information about how to access and use other Fraud Protection capabilities, see the following documents:

- Protect customer accounts with Fraud Protection
- Protect customer purchases with Fraud Protection
- Manage loss prevention with Fraud Protection
