---
author: josaw1
description: This article describes how to set up a purchased version of Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Set up a purchased instance
---

# Set up a purchased instance

[!include[deprecation](includes/deprecation.md)]

This document guides you through setting up a purchased version of Microsoft Dynamics 365 Fraud Protection. After you complete the tasks in this document, you'll be ready to use Fraud Protection to protect your business.

## Prerequisites

To set up Fraud Protection and control user access to your data, you must have a Microsoft Entra tenant. If you don't already have a Microsoft Entra tenant, you can sign up for one.

## Choose the correct Entra tenant

The following sign-in scenarios are intended for customers who purchased a license for Fraud Protection.
- When you purchase a license through a Microsoft Cloud Solution Provider (CSP), the CSP determines which Microsoft Entra tenant you'll use. To get started with that tenant, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.
- If you purchased a license through a Volume Licensing (VL) channel, follow the instructions in the email that you received to activate your subscription in the desired tenant. Then, to get started, go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/), and sign in by using global administrator credentials.


### Complete the setup process	

1.	Go to [Access your Dynamics 365 Fraud Protection account](https://dfp.microsoft.com/) and sign in as the Global administrator of the Microsoft Entra tenant.	
2.	On the next screen under the **Data storage geography** field, select the geographic region where you want to store your data, and then select **Start setup**.	

  > [!NOTE]
  > You can't change the **Data storage geography** value after you've set it.	

3.	The setup process starts and may take a few minutes to run. If you prefer, you can sign out, and then return after installation is completed.	
4.	After setup is completed, you're prompted to review important information about the Fair Credit Reporting Act (FCRA). After completing your review, select **I accept**.	
5.	The Fraud Protection portal opens.	

## Next steps

For information about how to access and use other features in Fraud Protection, see the articles below.

- [Set up customer account protection](promocode-set-up-account-protection.md)
- [Set up purchase protection](promocode-set-up-purchase-protection.md)
- [Set up loss prevention](promocode-set-up-loss-prevention.md)


## Configure access for additional users (Optional)

Fraud protection offers role-based access control (RBAC) for enhanced security and role management. Initial configuration of users and roles should be done by the global administrator of your Microsoft Entra tenant. After an **AllAreas_Admin** account is set up, you can use it to add additional users.
For more information about how to configure user access, see [Configure user access](configure-user-access.md).

## Usage Restrictions – Fair Credit Reporting Act

You may have read our licensing restrictions concerning the Fair Credit Reporting Act (FCRA). The FCRA is a federal privacy law that regulates the disclosure and use of consumer personal information to determine a consumer’s eligibility to obtain a product or service or otherwise engage in a transaction. For example, if you’ve applied for a credit card or loan recently, the bank probably obtained your credit report to determine whether you are a credit risk. The FCRA would apply to that. But what you might not know is that the FCRA also applies to the use of consumer personal information for non-credit related transactions, such as insurance, employment, and even retail purchases, where the consumer’s reputation or personal characteristics bear on eligibility. 

Fraud Protection evaluates fraud risk at the transaction level only, by evaluating your transaction against past transactions that were voided due to third party fraud. Third party fraud typically happens when a consumer’s credit card is lost or stolen and then used to make purchases that the consumer did not authorize and would not know about until the consumer reviewed their monthly statement.

Fraud Protection informs you of the risk that the transaction may have been initiated by a fraudster, and not whether the specific purchaser has a history of committing fraud. Fraud Protection was not designed to analyze on the purchaser’s reputation or past behavior, and the use of Fraud Protection could impact Microsoft if it is ever abused to assess the personal characteristics of any given purchaser for the purposes restricted by the law. If the FCRA were to apply, customers and Microsoft could be exposed to a number of notice, disclosure and other onerous legal requirements.

For this purpose, we protect usage of our application by informing customers of these restrictions during their first-run experience. A system-set notice-and-consent routine is presented to every environment administrator, preceded by a short video, where customers are required to read and attest their consent to usage in accordance with certain licensing restrictions that prohibit the use of Fraud Protection for the purposes restricted under the FCRA. This notice and consent experience is renewed on an annual basis, and it is automatically triggered when users are granted administration privileges. If your Fraud Protection instance has multiple child environments, all users granted administrator privileges are subject to our FCRA notice-and-consent routine during their first first-run experience with the application. 

Fraud Protection is a powerful technology that must be used with care. We urge you to use it responsibly.
