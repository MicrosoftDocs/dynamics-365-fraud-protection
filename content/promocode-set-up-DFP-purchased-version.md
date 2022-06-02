---
author: josaw1
description: This article describes how to set up a purchased version of Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 06/04/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up a purchased instance
---



# Set up a purchased instance
This document guides you through setting up a purchased version of Microsoft Dynamics 365 Fraud Protection. After you complete the tasks in this document, you'll be ready to use Fraud Protection to protect your business.

## Prerequisites

To set up Fraud Protection and control user access to your data, you must have an Azure Active Directory (Azure AD) tenant. If you don't already have an Azure AD tenant, you can sign up for one.

## Choose the correct Azure tenant

The following sign-in scenarios are intended for customers who purchased a license for Fraud Protection.
- When you purchase a license through a Microsoft Cloud Solution Provider (CSP), the CSP determines which Azure AD tenant you'll use. To get started with that tenant, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.
- If you purchase a license through a Volume Licensing (VL) channel, follow the instructions in the email that you received to activate your subscription in the desired tenant. Then, to get started, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.


### Complete the setup process	

1.	Go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/) and sign in as the Global administrator of the Azure AD tenant.	
2.	On the next screen under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the **Data storage geography** value after you've set it.	

3.	The setup process starts and may take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
4.	After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
5.	The Fraud Protection portal opens.	

## Next steps

For information about how to access and use other features in Fraud Protection, see the articles below.

- [Set up customer account protection](promocode-set-up-account-protection.md)
- [Set up purchase protection](promocode-set-up-purchase-protection.md)
- [Set up loss prevention](promocode-set-up-loss-prevention.md)


## Configure access for additional users (Optional)

Fraud protection offers role-based access control (RBAC) for enhanced security and role management. Initial configuration of users and roles should be done by the global administrator of your Azure AD tenant. After an **AllAreas_Admin** account has been set up, you can use it to add additional users.
For more information about how to configure user access, see [Configure user access](configure-user-access.md).
