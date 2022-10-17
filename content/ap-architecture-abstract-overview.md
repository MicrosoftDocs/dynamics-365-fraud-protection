author: cschlegel2
description: This article is a visual abstract of how Dyanmics 365 Fraud Protection Account Protection Works
ms.author: cschlege2
ms.date: 10/17/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Admin
  - IT Pro
title: Abstract Diagram of How Dynamics 365 Fraud Protection - Account Protection Works
ms.custom:

This article provides visual abstract representation and description of how Microsoft Dynamics 365 Fraud Protection – Account Protection interacts with our customers to support their users. Microsoft Dynamics 365 Fraud Protection provides merchants the capability to assess if the risk of attempts to create new accounts and attempts to log in on merchant’s ecosystem are fraudulent. Risk assessment in Fraud Protection can be used by the customer to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts. The diagram below highlights some of the product capabilities and APIs (Application Programming Interfaces) to help you better understand these interactions. Particularly for Account Create and Account Login scenarios.


![overview](media/architecture-abstract1-overview.png)

- **1.Device Fingerprinting:** Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address. This feature is based on artificial intelligence (AI) and can be used as input to the process of fraud assessments. A Java-based web SDK (software development kits) and iOS, Android and React Native SDKs for mobile applications are available.

- **2.Account Payload:** Information our customers pass along to Dynamics Fraud Protection related to the Account Creation or Account Login. This data is then compared to data already within our fraud protection network where our machine learning will look for linkages. 

- **3.Risk Assessment:** The machine learning model can then return a score to you for bot and risk scores. The scoring can tell you the probability of fraud risk, or the likelihood of possible fraud that you may want to review or reject.  
