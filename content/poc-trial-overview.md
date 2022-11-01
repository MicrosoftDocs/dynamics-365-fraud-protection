---
author: cschlegel2
description: This article explains proof of concept options in Microsoft Dynamics 365 Fraud Protection.
ms.author: cschlegel
ms.date: 11/01/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Administrator
  - IT Pro
title: Proof of concept options 
ms.custom:
---

# Proof of concept options 

This article explains proof of concept options in Microsoft Dynamics 365 Fraud Protection.

Fraud Protection provides you with the ability to try a proof of concept (POC) to determine if a proposed fraud solution can meet your business needs. The POC includes a free 90-day trial period of Fraud Protection for evaluation before making a purchase decision.  

## Prerequisites

- To participate in a POC of Fraud Protection, a customer must have an Azure Active Directory (Azure AD) tenant. If you do not already have an Azure AD tenant, you can sign up for one.  
- To start a POC for Fraud Protection, Microsoft or a Microsoft authorized partner must first provide you with a promotion code. If you do not have a promotion code, see [Get started with Fraud Protection](https://dynamics.microsoft.com/get-started/?appname=fraudprotection) to contact a partner and request one.

## POC examples 

Below are the different examples to participate in the POC trial depending on the Microsoft Dynamics 365 Fraud Protection solution that you are interested in exploring. 

| Fraud Protection capability | POC type | Requirements  | Estimated time for completion |
| ------------- |-------------| -----| ------ |
| [Account protection](#account-protection-online-POC) | Online POC | API integration | 6-8 weeks |
| Purchase protection | Offline POC | Historical data | 2 weeks |
| Purchase protection | Online POC | API integration | 6-8 weeks |
| Purchase protection | Online POC with Dynamics 365 Commerce | API integration | 4-6 weeks |
| Loss prevention | Offline POC | Historical data | 2 weeks |
| Loss prevention | Offline POC with Dynamics 365 Commerce | Historical data | 1 week |

<!--![Representation of available POC options](media/poc-options-image.png)-->

### Account protection (online POC)

The online POC requires API integration to set up the Account Protection solution for either Account Create, Account Login or both. This POC process typically takes about six weeks for results depending on your speed to integrate, but provides the most accurate results and authentic experience to using the solution. You can gain a thorough understanding of the cutting-edge AI, robust features, reporting dashboards, how the solution would address your specific fraud challenges within the product portal, and how your team and customers could potentially interact with the solution. If you decide to move forward with purchasing the solution, then it is already set up to use. **Note:** There is only the online POC option for Account Protection.  

### Purchase Protection (offline POC)

The offline POC is the fastest way to understand Purchase Protection with results being shared back in typically two weeks depending on data quality. You would need to provide Microsoft Dynamics Fraud Protection with a minimum of three months of transaction data, two months of this data having chargebacks/labels, and the last month of data just being the transaction details, no chargebacks or labels needed. The Microsoft team will run this data through our Machine Learning Models and come back to you with a presentation and supporting files illustrating the results related to your fraud risk scenarios. Offline POC results are guidelines as to what you can expect with real-life results. Actual results may differ due to additional fraud signals captured (such as device fingerprinting) and are also influenced by the latest fraud trends. 

### Purchase Protection (online POC)

The online POC for Purchase Protection is similar to the Account Protection Online POC process (see above) where API integration is required. This online POC typically takes about six to eight weeks to see results depending on your pace of integration and the quality of the data you provide. You can gain a thorough understanding of the innovative AI, robust features, reporting dashboards, how the solution would address your specific fraud challenges within the product portal, and how your team and customers could potentially interact with the solution. 

### Purchase Protection (Dynamics 365 Commerce & Fraud Protection Online POC)

If you are an existing Dynamics 365 Commerce customer, then the connection between Dynamics 365 Commerce and Dynamics 365 Fraud Protection allows you to get a jumpstart on running an online POC for Purchase Protection. The process is faster than a typical online POC and some of the required D365 Fraud Protection API integrations can be done with just a few configuration changes in D365 Commerce. D365Commerce customers can simply go to the D365 Fraud Protection portal, set up D365 Fraud Protection, and get started. For more information to get started refer to [set up purchased instance](promocode-set-up-dfp-purchased-version.md)

### Loss Prevention (Offline POC)

Loss prevention requires you to map historical data and upload it in the Fraud Protection portal. The Dynamics 365 Fraud Protection team can work with you to understand the results of your data and instruct you on how to use the Loss Prevention solution to address specific challenges related to potential fraud risk scenarios. 

### Loss Prevention (Dynamics 365 Commerce & Fraud Protection Offline POC)

If you are a D365 Commerce customer, you can easily import your data and generate Loss Prevention reports from the D365 Fraud Protection portal with just a few clicks. The Dynamics 365 Fraud Protection team can work with you to understand the results of your data and instruct you on how to use the Loss Prevention solution to address specific challenges related to potential fraud risk scenarios. To conduct this POC, refer to [Loss Prevention in Commerce](/dynamics365/commerce/dev-itpro/dfp#loss-prevention-in-commerce) to get started with the POC. 
