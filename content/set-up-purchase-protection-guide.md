author: cschlegel2
description: This document guides you through setting up Microsoft Dynamics 365 Purchase Protection.  
ms.author: cschlegel
ms.date: 04/25/2023
ms.topic: reference
search.audienceType:
  - Developer, IT PRO, Fraud Manager
title: Set Up Purchase Protection Onboarding Guide
ms.custom:
---


# Set Up Purchase Protection Onboarding Guide
This document guides you through setting up Microsoft Dynamics 365 Purchase Protection. Customers can look forward to a smooth onboarding process by following the steps and links outlined in this onboarding guide below. Below is a summary of the steps in this guide.  

 
 1. Overview of Fraud Protection capabilities  
 2. Understand how purchase protection works 
 3. Onboarding planning and implementation milestones 
 4. Provisioning Fraud Protection in INT (Sandbox) and PROD  
 5. User access and assign roles 
 6. Review APIs and data mapping  
 7. Integrate purchase protection APIs  
 8. Integrate device fingerprinting 
 9. Test and validate  
10. Setting up continuous Operations & Features 


## Prerequisites 

To set up Fraud Protection and control user access to your data, you must have an Azure Active Directory (Azure AD (Active Directory)) tenant. If you do not already have an Azure AD tenant, please contact your authorized Microsoft seller or partner to sign up for one. 
Before you can install Fraud Protection, an authorized Microsoft seller or partner must provide a promotion code to you. If you do not have a promotion code, contact your authorized Microsoft seller or partner.

To help you get started with setting up Purchase Protection, we have provided the steps below with related onboarding and integration document links from this site for quick reference. Follow the doc links below to walk through the provisioning, integration, and key features.  


## Onboarding & Integration Steps with Doc Links

### Step 1: Overview of Dynamics Fraud Protection

Understanding Purchase Protection, Account Protection, and Loss Prevention capabilities. 

- [Dynamics 365 Fraud Protection home page](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/)

### Step 2: Understand How Purchase Protection Works

Follow the link below to understand how purchase protection interacts with different entities, such as customers and banks. This doc also highlights purchase protection capabilities and APIs, to help you better understand risk assessment interactions. 
 
- [How purchase protection works](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/how-pp-works)

### Step 3: Onboarding Planning and Implementation Milestones for Purchase Protection  

Onboarding planning will help you understand and plan for the project implementation milestones of purchase protection integration and onboarding. Follow this link to learn more.  
- [Onboarding planning](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/pp-onboarding-planning-guide)

### Step 4: Provisioning Fraud Protection in INT (Sandbox) and PROD 

Fraud protection is provisioned into an Azure AAD (Azure Active Directory) Tenant. You can either provision Dynamics 365 Fraud Protection into your existing AAD tenant or a new AAD tenant. Follow these links for more information. 
- [Set up a trial instance of Fraud Protection](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/promocode-set-up-dfp-trial-version)
- [Set up a purchased instance of Fraud Protection](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/promocode-set-up-dfp-purchased-version)

Managing Environments (for partners or customers with multiple Fraud Protection environments) Microsoft Dynamics Fraud Protection provides the option for partners and customers to create multiple environments, allowing for customization of their setup in a way that meets their specific needs. This feature offers flexibility in establishing a hierarchy that is suitable for their requirements. 
- [Manage environments](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/manage-psp-environments)

### Step 5: Configure User Access and Assign Roles  
 
You can grant users various levels of access to the service, based on logical or functional roles.  
 - [Configure user roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/configure-user-access)
 - [User roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/user-roles-access)
 - [Payment service provider user roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/psp-user-roles)
 
### Step 6: Review APIs and Data Mapping for Purchase Protection 

In this step, your authorized Microsoft partner should collaborate with you to check that your available data aligns with our APIs and provides sufficient information to run machine learning models and generate scores effectively.  
- [Integrate purchase protection APIs](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/integrate-real-time-api)
- [Labels API](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/labels-api)

### Step 7: Integrate Purchase Protection APIs 

Collaborate with your authorized Microsoft partner, to confirm your questions are addressed and APIs are properly integrated, as outlined in this guide.
- [Swagger UI](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/swagger)

### Step 8: Integrate Device Fingerprinting  

Dynamics Fraud Protection offers a sophisticated Device Fingerprinting functionality that significantly enhances our model scoring. Device fingerprinting can be integrated into either the partner's hosted page or the merchant's webpage. Please visit our Swagger UI (user interfaces) to visualize and interact with the API’s resource which can be found in this link
- [Set up device fingerprinting](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/device-fingerprinting)

### Step 9: Test and Validate Purchase Protection  

In this stage, as test traffic begins to flow into our Sandbox environment, please contact your authorized Microsoft partner to confirm that your data is being received. Upon successful completion of these validations, the integration process can then proceed to its full implementation in production environments. Please let your authorized Microsoft partner know that you have started sending traffic to confirm the data was received. 

 
### Step 10: Continuous Operations and Features 

At this stage, you will begin setting up your purchase protection features and operations. Customers can determine their own unique set of rules, velocities, and leverage other features as needed to best serve the needs of their business.  


### Transaction Acceptance Booster

TAB (Transaction Acceptance Booster) helps you benefit from higher acceptance rates by sharing Transaction Trust Knowledge with banks. 
- [Transaction acceptance booster (TAB)](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/transaction-acceptance-booster)

### Rules 

Writing Rules, which can use features like Velocities, Lists, External cCalls, and DFP model scores to make decisions. 
- [Manage rules](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/rules)

### Velocities 

Velocity checks help you identify several types of event patterns.
- [Velocity checks](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/velocities)

### Lists 

Lists help you manage information that you use to fight fraud and enforce business policies. 
- [Lists Overview](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/lists-overview)
- [Manage support lists](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/manage-support-lists)
- [Manage custom lists](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/lists)

### Search 

The Search page helps you find and view details about events in Microsoft Dynamics 365 Fraud Protection, based on specific filter values. 
- [Search](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/search)
- [Risk support](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/risk-support)

### Case Management 

Case management lets you organize and access transactions and specify the level of ambiguity that will require review by human subject matter experts. It also includes functionality that lets you provide a feedback loop for the AI-based assessments. 
- [Case management overview](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/case-management-overview)
- [Case management for administrators](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/case-management-administrator)
- [Case management for manual reviewers](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/case-management-manual-review)

### Reporting 

Reporting is available to display the impact of Dynamics Fraud Protection to your business.
- [Key metrics](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/scorecard)
- [Virtual fraud analyst](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/virtual-fraud-analyst)
- [Fraud tracker tool](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/fraud-tracker)
- [Long term report](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/long-term-report)
- [Rule performance report](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/rule-performance-report)


### Event Tracing & Event Hub 

Event Tracing offers you the ability to track and audit events, providing you with the option to redirect your data to various destinations outside the Fraud Protection Portal. To use Event tracing functionality, customers must have a subscription to additional Azure services such as Event Hub or Blob Storage. Contact your Microsoft Authorized Seller for details. If you have Azure global administrator credentials, log into the [Azure portal](https://ms.portal.azure.com) to determine available subscriptions.  
- [Event tracing](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/event-tracing)
- [Set up extensibility via Event Hubs](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/extensibility-via-event-hubs-overview)

### External Calls 

External calls let you ingest data from APIs outside Microsoft Dynamics 365 Fraud Protection and then use that data to make informed decisions in real time. 
- [External calls](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/external-calls)

### Upload Historical Data into Purchase Protection 

Data upload capabilities can be used to cold start our models or provide continuous batched data like Chargeback.
- [upload historical data](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/data-upload)
