---
author: cschlegel2
description: This article explainss how to evaluate proof of concept options in Microsoft Dynamics 365 Fraud Protection.
ms.author: cschlegel
ms.date: 11/01/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - Administrator
  - IT Pro
title: Evaluate proof of concept options 
ms.custom:
---

# Evaluate proof of concept options 

This article explains how to evaluate proof of concept options in Microsoft Dynamics 365 Fraud Protection.

Fraud Protection provides you with the ability to evaluate a proof of concept (POC) to determine if a proposed fraud solution can meet your business needs. The POC includes a free Fraud Protection 90-day trial period that you can assess before making a purchase decision.  

## Prerequisites

- To participate in a Fraud Protection POC, you must have an Azure Active Directory (Azure AD) tenant. If you do not already have an Azure AD tenant, you can sign up for one.  
- To start a Fraud Protection POC, Microsoft or a Microsoft authorized partner must first provide you with a promotion code. If you do not have a promotion code, see [Get started with Fraud Protection](https://dynamics.microsoft.com/get-started/?appname=fraudprotection) to contact a partner and request one.

## Fraud Protection POC capabilities 

The following table lists Fraud Protection POC capabilities and their POC types, requirements, and estimated times for completion.

| Fraud Protection capability | POC type | Requirements  | Estimated time for completion |
| ------------- |-------------| -----| ------ |
| [Account protection](#account-protection-online-poc) | Online POC | API integration | 6-8 weeks |
| [Purchase protection](#purchase-protection-offline-poc) | Offline POC | Historical data | Two (2) weeks |
| [Purchase protection](#purchase-protection-online-poc) | Online POC | API integration | 6-8 weeks |
| [Purchase protection](#purchase-protection-dynamics-365-commerce-and-fraud-protection-online-poc) | Online POC with Dynamics 365 Commerce | API integration | 4-6 weeks |
| [Loss prevention](#loss-prevention-offline-poc) | Offline POC | Historical data | Two (2) weeks |
| [Loss prevention](#loss-prevention-dynamics-365-commerce-and-fraud-protection-offline-poc) | Offline POC with Dynamics 365 Commerce | Historical data | One (1) week |

<!--![Representation of available POC options](media/poc-options-image.png)-->

## POC examples 

Below are the different examples of how to participate in a POC trial, depending on the Fraud Protection solution that you are interested in exploring.

### Account protection (online POC)

The account protection online POC requires API integration to set up the account protection solution for account creation, account sign-in, or both. This POC provides an authentic experience with the most accurate results, and typically takes about six weeks to obtain results, depending on your integration speed. With this POC, you can gain a thorough understanding of Fraud Protections artificial intelligence (AI), robust features, and reporting dashboards. You can also learn how the solution would address your specific fraud challenges within the product portal, and how your team and customers could potentially interact with the solution. If you decide to move forward with purchasing the solution, it is already set up for you to use. 

> [!NOTE]
> Account protection only has the online POC option.  

### Purchase protection (offline POC)

The purchase protection offline POC is the fastest way to understand purchase protection, with results typically obtained in two weeks, depending on data quality. To use this POC, you must provide Fraud Protection with a minimum of three months of transaction data. Two months of this data must have chargebacks/labels, with the third month of data just having transaction details. The Fraud Protection team will then run the data through machine learning models and return a presentation with supporting files that illustrates the results related to your fraud risk scenarios. Offline POC results are guidelines as to what you can expect with real-life results. Actual results may differ due to additional fraud signals (such as device fingerprinting) being captured, and are also influenced by the latest fraud trends. 

### Purchase protection (online POC)

The purchase protection online POC is similar to the [account protection online POC process](#account-protection-online-poc), where API integration is required. This online POC typically takes about six to eight weeks to obtain results, depending on your pace of integration and the quality of the data you provide. With this POC, you can gain a thorough understanding of the innovative AI, robust features, and reporting dashboards. You can also learn how the solution would address your specific fraud challenges within the product portal, and how your team and customers could potentially interact with the solution. 

### Purchase protection (Dynamics 365 Commerce and Fraud Protection online POC)

If you are an existing Dynamics 365 Commerce customer, then the connection between Dynamics 365 Commerce and Dynamics 365 Fraud Protection allows you to get a jumpstart on running a purchase protection online POC. The process is faster than a typical online POC, and some of the required Fraud Protection API integrations can be done with just a few configuration changes in Commerce. To get started, Commerce customers can go to the Fraud Protection portal to set up Fraud Protection. For more information on getting started, see [Set up a purchased instance](promocode-set-up-dfp-purchased-version.md).

### Loss prevention (Offline POC)

The loss prevention offline POC requires you to map historical data and upload it to the Fraud Protection portal. The Fraud Protection team can then work with you to understand the results of your data and guide you how to use the loss prevention offline POC solution to address specific challenges related to potential fraud risk scenarios. 

### Loss prevention (Dynamics 365 Commerce and Fraud Protection offline POC)

If you are a Dynamics 365 Commerce customer, you can easily import your data and generate loss prevention reports from the Fraud Protection portal. The Fraud Protection team can work with you to understand the results of your data and guide you on how to use the loss prevention offline POC solution to address specific challenges related to potential fraud risk scenarios. To get started, see [Loss prevention in Commerce](/dynamics365/commerce/dev-itpro/dfp#loss-prevention-in-commerce). 
