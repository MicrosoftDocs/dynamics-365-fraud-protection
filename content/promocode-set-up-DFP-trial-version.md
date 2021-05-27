---
author: yvonnedeq
description: This topic describes how to set up a trial version of Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.date: 04/27/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up a trial version of Dynamics 365 Fraud Protection
---

# Set up a trial version of Dynamics 365 Fraud Protection

This document guides you through the prerequisites of setting up a trial version of Microsoft Dynamics 365 Fraud Protection. After you complete the tasks in this document, you will be ready to use Fraud Protection to protect your business.

## Prerequisites for setting up Fraud Protection

- To set up Fraud Protection and control user access to your data, you must have an Azure Active Directory (Azure AD) tenant. If you don't already have an Azure AD tenant, you can sign up for one.
- Before you can install a trial subscription of Fraud Protection, a Microsoft seller or partner must provide a promotion code provided to you. If you don't have a promotion code, contact Microsoft.

## Set up Fraud Protection in an existing Azure AD tenant	

If your company already has an Azure AD tenant, you can add Fraud Protection to it. Your IT organization can then centrally manage access.  Although this approach requires intervention from the global administrator of the Azure AD tenant, it's useful if you want to maintain states between a trial Fraud Protection environment and a paid Fraud Protection environment.

  > [!NOTE]
  > To set up Fraud Protection in an existing Azure AD tenant, you must have **global administrator permissions**.


- If you have global administrator permissions, follow the instructions in the **Setup process for an existing Azure AD tenant** section next in this topic.	
- If you don't have global administrator permissions, find someone in your organization who does, so that they can help you with the setup process.	

## Setup process for an existing AAD tenant	

1.	Select the sign-up link that was included in your welcome email.	
2.	Enter your work email address, and then select **Verify**. The domain name in the email address must match your existing Azure AD tenant.	
3.	Choose the first option, by clicking Sign-In button and entering the credentials for Global Administrator of this Azure AD tenant. 
4.	After you successfully sign in, the next page notifies you that you're about to redeem the promotion code to start your **free trial of Dynamics 365 Fraud Protection**.	

  	The promotion code and offer ID are automatically entered on the page when you complete your setup.	

4.	You can review the trial agreement and privacy statements, and then Click **Get started**.	
5.	On the next screen under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the region after you've set it.	

6.	The setup process starts and might take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
7.	After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
8.	The Fraud Protection portal opens.	

Congratulations! You've successfully completed the setup process and are ready to use Fraud Protection to protect your business.	

## Set up Fraud Protection in a new Azure AD tenant	

If you don't have an existing AAD tenant, or if you prefer to set up a new one, use this process.	

### Setup process for a new AAD tenant 	

1.	Select the sign-up link that was included in your welcome email.	
2.	Enter your work email address and click 'Verify'.	
3.	If your work email does not map to an existing Azure AD domain, you're prompted to create a new tenant. Select **Click here to create an Azure tenant** and move to step 6
4.	If your work email maps to an existing Azure AD domain, you can create a new Azure AD tenant by clicking **Sign up** option on the subsequent page

5.	In the signup flow, enter the required details and then select **Next**.	
6.	In the domain name field, enter the domain name of your choice and click **Check availability** to see if the name is available. If not, choose a new one 

  > [!NOTE]
  > You can't change the domain name after the tenant is created.	

7.	After you've entered a domain name that's available, click **Next** and then choose a username and password.
8.	After you have reviewed the trial agreement and privacy statements, click **Sign up** to create your new Azure AD tenant and start your **free trial of Dynamics 365 Fraud Protection**

9.	Select **Get started**.	
10.	On the next screen click Sign In and enter the username and password you created in Step 7.
11.	Under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the region after you've set it.	

12. The setup process starts and might take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
13. After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
14.	The Fraud Protection portal opens.	

Congratulations! You've successfully completed the setup process and are ready to use Fraud Protection to protect your business.	

## Next steps

For information about how to access and use Fraud Protection's features, see the following documents:

- [Protect customer accounts with Dynamics 365 Fraud Protection](promocode-set-up-account-protection.md)
-	[Protect purchases with Dynamics 365 Fraud Protection](promocode-set-up-purchase-protection.md)
-	[Prevent loss with Dynamics 365 Fraud Protection](promocode-set-up-loss-prevention.md)
