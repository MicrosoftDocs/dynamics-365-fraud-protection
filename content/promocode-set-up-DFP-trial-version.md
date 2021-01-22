---
author: yvonnedeq
description: This topic describes how to set up a trial version of Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 01/22/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Set up a trial version of Fraud Protection
---



# Set up a trial version of Fraud Protection

## Protect your business from fraudulent activity

Microsoft Dynamics 365 Fraud Protection (Fraud Protection) is a sophisticated technology stack that uses connected big data across multiple lines of business and applies cutting-edge artificial intelligence (AI) to help provide more accurate decisions in real time.
Here are some examples of the innovative and advanced ways that Fraud Protection can help protect your business:

- AI and insights from the fraud protection network
- Device fingerprinting
- A rules engine and virtual fraud analyst
- A graph explorer and scorecard
- A transaction acceptance booster

## Goals for this document

This document guides you through the process of setting up a trial version of Fraud Protection.
After you complete the tasks in this document, you will be ready to use Fraud Protection to protect your business.

## Prerequisites for setting up Fraud Protection

- To set up Fraud Protection and control user access to your data, you must have an Azure Active Directory (Azure AD) tenant. If you don't already have an Azure AD tenant, you can sign up for one.
- Before you can install a trial subscription of Fraud Protection, a Microsoft seller or partner must provide a PromoCode provided to you. If you don't have a PromoCode, contact Microsoft.

## Set up Fraud Protection in an existing Azure AD tenant

If your company already has an Azure AD tenant, you can add Fraud Protection to it. Your IT organization can then centrally manage access.  Although this approach requires intervention from the global administrator of the Azure AD tenant, it's useful if you want to maintain states between a trial Fraud Protection environment and a paid Fraud Protection environment.

  > [!NOTE]
  > To set up Fraud Protection in an existing Azure AD tenant, you must have **global administrator permissions**.

- If you have global administrator permissions, follow the instructions in the [Setup process in an existing Azure AD tenant](https://github.com/MicrosoftDocs/dynamics-365-fraud-protection-pr/new/promocode/content#set-up-fraud-protection-in-an-existing-azure-ad-tenant) section later in this topic.
- If you don't have global administrator permissions, find someone in your organization who does, so that they can help you with the setup process.

## Setup process for an existing AAD tenant

1.	Select the sign-up link that was included in your welcome email.
2.	Enter your email address, and then select **Next**. The domain name in the email address must match your existing Azure AD tenant.
3.	After you successfully sign in, the next page notifies you that you're about to redeem the PromoCode to start your **free trial of Dynamics 365 Fraud Protection**.

  	The PromoCode and offer ID are automatically be entered on the page when you complete your setup.

    (image)

4.	Select **Get started**.
5.	To review the Terms of Use, select **Microsoft Online Subscription Agreement**.
6.	To accept the Terms of Use, select **I accept**.
7.	In the **Geographic data storage region** field, select the region where you want to store your data, and then select **Next**.

    You can't change the region after you've set it.

8.	The setup process is started and might take up to 20 minutes to run. If you prefer, you can sign out and then return after installation is completed.
9.	After setup is completed, the **Congratulations** screen appears.
10.	Select **Continue**.
11.	You're prompted to review important information about the Fair Credit Reporting Act (FCRA). After you've completed your review, select **I accept**.
12.	The Fraud Protection portal is opened.

    (image)

Congratulations! You've successfully completed the setup process and are ready to use Fraud Protection to protect your business.

## Set up Fraud Protection in a new Azure AD tenant

If you don't have an existing AAD tenant, or if you prefer to set up a new one, use this process.

### Setup process for a new AAD tenant 

1.	Select the sign-up link that was included in your welcome email.
2.	Enter an email address that has a unique domain name (that is, the domain name of the new tenant that you want to set up).

    For example, enter *admin@<your choice of domain name>.onmicrosoft.com*

3.	Select **Verify**.
4.	If the tenant name is already being used, you're prompted to create a new tenant. In this case, repeat steps 2 and 3
5.	If the tenant name is accepted, select **Click here to create an Azure tenant**.

    (image)

6.	Enter the required details, and then select **Next**.

    You can use any valid work or school email address. It doesn't have to be the same one that you used in step 2.

7.	In the username field, enter the username from the email address you entered in step 2.
8.	In the company name field, enter the domain name from that email address. Then select **Next**.

    You can't change the company name after the tenant is created.

9.	After you've entered the company name and a green check mark appears, enter a password, and then select **Create my account**.

    (image)

10.	Select the **Sign in** link below the text box.
11.	In the **Sign in** dialog box, enter your credentials, and then select **Next**.

    (image)

    After you successfully sign in, the next page notifies you that you're about to redeem the PromoCode to start your **free trial of Dynamics 365 Fraud Protection**.
  
    The PromoCode and offer ID is automatically entered on the page.
  
    (image)

12.	Select **Get started**.
13.	To review the Terms of Use, select **Microsoft Online Subscription Agreement**.
14.	To accept the Terms of Use, select **I accept**.
15.	In the **Geographic data storage region** field, select the region where you want to store your data, and then select **Next.** 

    You can't change the region after you've set it.
    
    The setup process is starts and might take up to 20 minutes to run. If you prefer, you can sign out and then return after installation is completed.
    
    After setup is completed, the **Congratulations** screen appears.

16.	Select **Continue**.
17.	You're prompted to review important information about the Fair Credit Reporting Act (FCRA). After you've completed your review, select **I accept**.

    The Fraud Protection portal opens.

    (image)

    Congratulations! You've successfully completed the setup process and are ready to use Fraud Protection to protect your business.

### Next steps

For information about how to access and use Fraud Protection's features, see the following documents:

- [Protect customer accounts with Fraud Protection]()
- [Protect customer purchases with Fraud Protection]()
- [Manage loss prevention with Fraud Protection]()

