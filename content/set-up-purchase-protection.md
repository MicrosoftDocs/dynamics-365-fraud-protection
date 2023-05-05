---
author: cschlegel2
description: This article explains how to set up up Microsoft Dynamics 365 Purchase Protection.  
ms.author: cschlegel
ms.date: 04/25/2023
ms.topic: reference
search.audienceType:
  - Developer, IT PRO, Fraud Manager
title: Set Up Purchase Protection 
ms.custom:
---


# Set Up Purchase Protection 
This article provides an overveiw of how to set up Purchase Protection functionality in Dynamics 365 Fraud Protection. To help you get started, we have provided the steps below with related onboarding and integration document links for quick reference. Follow the links below to walk through the provisioning, integration, and key features.  

1. [Understand how purchase protection works](#understand) 
2. [Onboarding planning and implementation milestones](#onboard)
3. [Provisioning Fraud Protection in INT (Sandbox) and PROD](#provision)
4. [Configure user access and assign roles](#configure)
5. [Review APIs and data mapping](#review)
6. [Integrate purchase protection APIs](#purchase)  
7. [Integrate device fingerprinting](#device)
8. [Test and validate](#test)
9. [Setting up continuous operations and features](#continuous)

## Prerequisites 

Before you set up Purchase Protection, you must set up Dynamics 365 Fraud Protection. This is where you control user access to your data. You must have an Azure Active Directory (Azure AD) tenant. If you don't already have an Azure AD tenant, contact your authorized Microsoft seller or partner to sign up for one. 
Before you can install Fraud Protection, an authorized Microsoft seller or partner must provide a promotion code to you. If you do not have a promotion code, contact your authorized Microsoft seller or partner. For more information about Fraud Protection, and to understand the capabilities of Purchase Protection, Account Protection, and Loss Prevention, see the [Dynamics 365 Fraud Protection home page](index.md).

## <a name="understand"></a>  Understand how Purchase Protection works

To understand how purchase protection interacts with different entities, such as customers and banks, see [How purchase protection works](how-pp-works.md). This article also highlights purchase protection capabilities and APIs, to help you better understand risk assessment interactions. 

## <a name="onboard"></a> Onboarding planning and implementation milestones for Purchase Protection  

Onboarding planning helps you understand and plan for the project implementation milestones of Purchase Protection integration and onboarding. To learn more, see [Onboarding planning](pp-onboarding-planning-guide.md).

## <a name="provision"></a>  Provisioning Fraud Protection in INT (Sandbox) and Production 

Fraud Protection is provisioned into an Azure AAD (Azure Active Directory) tenant. You can provision Fraud Protection into your existing AAD tenant or a new AAD tenant. For more information, see [Set up a trial instance of Fraud Protection](promocode-set-up-dfp-trial-version.md)
and [Set up a purchased instance of Fraud Protection](promocode-set-up-dfp-purchased-version.md).

Fraud Protection provides the option to create multiple environments. This allows you to customize the setup in a way that meets your specific needs. This feature offers flexibility in establishing a hierarchy that is suitable for your requirements. To learn more, see [Manage environments](manage-psp-environments.md).

## <a name="configure"></a> Configure user access and assign roles  
 
You can grant users various levels of access to the service, based on logical or functional roles. To learn more about user roles, access, and how to configure them, see: 
 - [Configure user roles and access](configure-user-access.md)
 - [User roles and access](user-roles-access.md)
 - [Payment service provider user roles and access](psp-user-roles.md)
 
## <a name="review"></a>  Review APIs and data mapping for Purchase Protection 

Your authorized Microsoft partner should collaborate with you to check that your available data aligns with our APIs and provides sufficient information to run machine learning models and generate scores effectively. For more information, see [Integrate purchase protection APIs](integrate-real-time-api.md) and [Labels API](labels-api.md).

## <a name="purchase"></a>  Integrate Purchase Protection APIs 

Collaborate with your authorized Microsoft partner to confirm your questions are addressed and APIs are properly integrated. To learn more, see [Swagger UI](swagger.md).

## <a name="device"></a>  Integrate device fingerprinting  

Fraud Protection offers sophisticated Device fingerprinting functionality that significantly enhances your model scoring. Device fingerprinting can be integrated into either a partner's hosted page or a merchant's webpage. View our Swagger UI to visualize and interact with the API’s resource here, [Set up device fingerprinting](device-fingerprinting.md).

## <a name="test"></a>  Test and validate Purchase Protection  

As test traffic begins to flow into the Sandbox environment, contact your authorized Microsoft partner to confirm that your data is being received. When the validations have successfully completed, the integration process can proceed to its full implementation in production environments. Let your authorized Microsoft partner know that you have started sending traffic to confirm the data was received. 

## <a name="continuous"></a>  Continuous operations and features 

As you begin setting up your Purchase Protection features and operations, you can determine your own unique set of rules, velocities while leveraging other features as needed to best serve the needs of your business.  

### Transaction Acceptance Booster

The Transaction Acceptance Booster (TAB) helps you benefit from higher acceptance rates by sharing Transaction Trust Knowledge with banks. For more detailed information, see [Transaction acceptance booster (TAB)](transaction-acceptance-booster.md).

### Rules 

You can create rules that include features like velocities, lists, external calls, and DFP model scores to make decisions. To learn more about rules, see [Manage rules](rules.md).

### Velocities 

Velocity checks help you identify several types of event patterns.
- [Velocity checks](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/velocities)

### Lists 

You can use lists to manage the information that you use to fight fraud and enforce business policies. To learn more, see:
- [Lists Overview](lists-overview.md)
- [Manage support lists](manage-support-lists.md)
- [Manage custom lists](lists.md)

### Search 

You can use the **Search** to find and view details about events in Fraud Protection, based on specific filter values. For more information, see [Search](search.md) and [Risk support](risk-support.md).

### Case management 

Use case management to organize and access transactions, specify the level of ambiguity that will require review by human subject matter experts, and provide a feedback loop for the AI-based assessments. To learn more about how to work with case management, see: 
- [Case management overview](case-management-overview.md)
- [Case management for administrators](case-management-administrator.md)
- [Case management for manual reviewers](ase-management-manual-review.md)

### Reporting 

Reporting is available to display the impact of Dynamics Fraud Protection on your business. To learn more about reporting, see:
- [Key metrics](scorecard.md)
- [Virtual fraud analyst](virtual-fraud-analyst.md)
- [Fraud tracker tool](fraud-tracker.md)
- [Long term report](long-term-report.md)
- [Rule performance report](rule-performance-report.md)

### Event tracing and Event Hub

Event tracing offers the ability to track and audit events, providing you with the option to redirect your data to various destinations outside the Fraud Protection Portal. To use Event tracing functionality, you must have a subscription to additional Azure services such as Event Hub or Blob Storage. Contact your Microsoft Authorized Seller for details. If you have Azure global administrator credentials, log into the [Azure portal](https://ms.portal.azure.com) to determine available subscriptions. To learn more about Event tracing and Event Hubs in Fraud Protection, see [Event tracing](event-tracing.md) and [Set up extensibility via Event Hubs](extensibility-via-event-hubs-overview.md).

### External calls 

You can use external calls to ingest data from APIs outside of Fraud Protection and then use that data to make informed decisions in real time. For more details, see [External calls](external-calls.md).

### Upload historical data into Purchase Protection 

Data upload capabilities can be used to cold start models or provide continuous batched data like Chargeback. To learn more, see [Upload historical data](data-upload.md).
