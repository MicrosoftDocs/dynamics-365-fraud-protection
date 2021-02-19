---
author: yvonnedeq
description: This topic describes how to set up a purchased version of Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 02/19/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up a purchased version of Fraud Protection
---



# Set up a purchased version of Fraud Protection

This document guides you through the prerequisites of setting up a purchased version of Fraud Protection.
After you complete the tasks in this document, you will be ready to use Fraud Protection to protect your business.

## Prerequisites for setting up Fraud Protection

To set up Fraud Protection and control user access to your data, you must have an Azure Active Directory (Azure AD) tenant. If you don't already have an Azure AD tenant, you can sign up for one.

## Choose the correct Azure tenant

The following sign-in scenarios are intended for customers who purchased a license for Fraud Protection.
- When you purchase a license through a Microsoft Cloud Solution Provider (CSP), the CSP determines which Azure AD tenant you will use. To get started with that tenant, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.
- If you purchase a license through a Volume Licensing (VL) channel, follow the instructions in the email that you received to activate your subscription in the desired tenant. Then, to get started, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.


### Complete the setup process	

1.	Go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/) and sign in as the Global administrator of the Azure AD tenant.	
2.	To review the **Terms of Use**, select **Microsoft Online Subscription Agreement**.	
3.	To accept the **Terms of Use**, select **I accept**.	
4.	In the **Geographic data storage region** field, select the region where you want to store your data, and then select **Next**.	

 	  > [!NOTE]	
 	  >You can't change the region after you've set it.	
    	
 	 The setup process is started and might take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
   
   After setup is completed, the **Congratulations** page appears.	
    	
5.	Select **Continue**.	
6.	You're prompted to review important information about the Fair Credit Reporting Act (FCRA). After you've completed your review, select **I accept**.	

   	The Fraud Protection portal is opened.	

![Data flow](media/promocode-images/DFP-Portal.png)	

Congratulations! You've successfully completed the setup process and are ready to use Fraud Protection to protect your business.


## Next steps

For information about how to access and use Fraud Protection's other capabilities, see the following documents:

- [Protect customer accounts with Fraud Protection](promocode-set-up-account-protection.md)
- [Protect purchases with Fraud Protection](promocode-set-up-purchase-protection.md)
- [Prevent loss with Fraud Protection](promocode-set-up-loss-prevention.md)


## Configure access for additional users (Optional)

Fraud protection offers role-based access control (RBAC) for enhanced security and role management. Initial configuration of users and roles should be done by the global administrator of your Azure AD tenant. After an **AllAreas_Admin** account has been set up, you can use it to add additional users.
For more information about how to configure user access, see [Configure user access to Fraud Protection](https://docs.microsoft.com/dynamics365/fraud-protection/configure-user-access) in the Fraud Protection documentation.
