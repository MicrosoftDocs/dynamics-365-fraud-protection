---
author: josaw1
description: This article describes how to set up a trial version of Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Set up a trial instance
---

# Set up a trial instance

This document guides you through setting up a trial version of Microsoft Dynamics 365 Fraud Protection. After you complete the tasks in this document, you'll be ready to use Fraud Protection to protect your business.

## Prerequisites

- To set up Fraud Protection and control user access to your data, you must have a Microsoft Entra tenant. If you don't already have an Microsoft Entra tenant, you can sign up for one.
- Before you can install a trial subscription of Fraud Protection, a Microsoft seller or partner must provide a promotion code to you. If you don't have a promotion code, contact Microsoft.

## Set up Fraud Protection in an existing Microsoft Entra tenant	

If your company already has an Microsoft Entra tenant, you can add Fraud Protection to it. Your IT organization can then centrally manage access. Although this approach requires intervention from the global administrator of the Microsoft Entra tenant, it's useful if you want to maintain states between a trial Fraud Protection environment and a paid Fraud Protection environment.

  > [!NOTE]
  > To set up Fraud Protection in an existing Microsoft Entra tenant, you must have **global administrator permissions**.


- If you have global administrator permissions, follow the instructions in the **Setup process for an existing Microsoft Entra tenant** section next in this article.	
- If you don't have global administrator permissions, find someone in your organization who does, so that they can help you with the setup process.	

## Setup process for an existing Microsoft Entra tenant	

1.	Select the sign-up link in your welcome email.	
2.	Enter your work email address, and then select **Verify**. The domain name in the email address must match your existing Microsoft Entra tenant.	
3.	Choose the first option by selecting **Sign-In** and entering the credentials for the global administrator of the Microsoft Entra tenant. 
4.	After you successfully sign in, the next page notifies you that you're about to redeem the promotion code to start your free trial of Dynamics 365 Fraud Protection.	

  	The promotion code and offer ID are automatically entered on the page when you complete your setup.	

4.	Review the trial agreement and privacy statements, and then select **Get started**.	
5.	On the next screen under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the **Data storage geography** value after you've set it.		

6.	The setup process starts and may take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
7.	After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
8.	The Fraud Protection portal opens.	
	

## Set up Fraud Protection in a new Microsoft Entra tenant	

If you don't have an existing Microsoft Entra tenant, or if you prefer to set up a new one, use the steps below.	

### Setup process for a new Microsoft Entra tenant 	

1.	Select the sign-up link in your welcome email.	
2.	Enter your work email address and then select **Verify**.	
3.	If your work email does not map to an existing Microsoft Entra domain, you're prompted to create a new tenant. Select **Click here to create an Azure tenant** and skip to step 6.
4.	If your work email maps to an existing Microsoft Entra domain, create a new Microsoft Entra tenant by selecting **Sign up** on the next page.
5.	Enter the required details in the signup flow and then select **Next**.	
6.	In the domain name field, enter a domain name and then select **Check availability** to see if the name is available. If the name isn't available , enter a different name.

  > [!NOTE]
  > You can't change the domain name after the tenant is created.	

7.	After you've successfully entered a domain name, select **Next** and then choose a username and password.
8.	Review the trial agreement and privacy statements, and then select **Sign up** to create your new Microsoft Entra tenant and start your free trial of Dynamics 365 Fraud Protection.
9.	Select **Get started**.	
10.	Select **Sign In** and enter the username and password you created in Step 7.
11.	Under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the **Data storage geography** value after you've set it.		

12. The setup process starts and may take a few minutes to run. If you prefer, you can sign out and then return after installation is completed.	
13. After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
14.	The Fraud Protection portal opens.	

## Next steps

For information about how to access and use features in Fraud Protection features, see the articles below.

- [Set up customer accounts](promocode-set-up-account-protection.md)
- [Set up purchase protection](promocode-set-up-purchase-protection.md)
- [Set up loss prevention](promocode-set-up-loss-prevention.md)
