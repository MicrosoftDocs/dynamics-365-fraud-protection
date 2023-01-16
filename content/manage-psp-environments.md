---
author: josaw1
description: This article explains how payment service providers (PSPs) can manage environments in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 01/16/2023
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Manage environments
---

# Manage environments


By creating additional new environments, customers can have greater flexibility and enhance the functionality provided by Fraud Protection to scale the solution to support their other business units. For example, customers can create organizations or divisions as root environments and configure their child environments as different departments, business, or product types. This allows for rules, user access, configuration, and other fraud protection settings to then be inherited from the parent level. Transaction data and reports will tehn be aggregated at the parent environment so business leaders can get an overiew of how an organization or division is performing.

## Create a new environment

To create a new environment, or switch between environments, select **Manage environments** under the environment picker in the upper right of the Microsoft Dynamics 365 Fraud Protection portal page. 

> [!NOTE]
> A root environment is an environment on the top level of the Fraud Protection tenant, with no parent environment. There can be multiple root environments in the Fraud Protection tenant. The **Product admin** role is required to create a new root environment. To learn more, see [NEED A LINK]().

To create a new environment, select **New environment** on the top and enter the following information: 

- **Data storage geography** – Select the geography where your customer data resides. To learn more about data residency, see [Data residency FAQ](faq/data-residency-gdpr-faq.md).
- **Name** – Provide the name of the environment that you want to create.
- **Description (optional)** – You can add some information to help identify the environment.
- **Tags (optional)** – You can use tags to specify any generic information that is related to the environment, such as the industry vertical.
- **Azure AD application ID**(optional) - If you want an existing Azure AD applciation ID to access the environment, paste the Azure AD application ID here. This is recommended if you plan to reuse API access credentials across two or more environments. For a list of available applications, on the **Integration** page, go to **Create Azure AD applications** or **Azure AD**.
- **Create API ID**(optional) - You can enter an identifier in this field to use when sending events to Fraud Protection instead of using the Fraud Protection instead of using the Graud Protection Environment ID.

> [!NOTE]
> You need the Global Admin role to access Create Azure AD applications. To learn more about Azure AD application and integration, view [Integrate purchase protection API](integrate-real-time-api) and [Integrate account protection APIs](faq/data-residency-gdpr-faq.md). 
>
> After you you create the environment, you can't change the customer API ID.

An environment that is created under another environment is called a child environment. The environment on top of another environment in the hierarchy is called the parent environment. By default, some settings and conigurations of child environments will follow the parent environment. The child environment also inherits the user access configuration of the parent environment by default. 

To create a child environment under another environment, complete the following steps. 

1. Select the ellipses next to the environment and then select **New child environment** from the menu. 
2. Enter the information for the child environment. For a child environment, the **Data storage geography** must match the root environment. 
3. Select **Create**.

## View environments

To view a list of all the environments under your tenant, select **Manage environment** under the environment picker. 

You can favorite an environment by clicking teh star icon next to it. This allows you to access the environment under the **Favorites** section in the **Environment switcher**. You can then export the list of environments from the **Manage environment** page. 

## Edit an existing environment
To edit an environment, complete the following steps.

1. Select **Manage environment** under the environment picker.
2. Select the ellipses next to the environment and then select **Edit**. Only the **Name**, **Description**, and **Tags** field can be edited. 

## Delete and environment
To delete and environment, from the environment picker, select **Manage environment**, select the ellipses next to the environment, and then select **Delete**.

When an environment is deleted, the transactions, rules, cases, and other data associated with it will be deleted. Usage data, transaction count, and aggregated report will be retained after an environment is deleted. 

When you delete a child environment, the metering report at parent environment still shows the assessments usage associated with the deleted environment. Similarly, the key metrics and summary data of the parent environment still contain the transactions associated with teh deleted environment. If you delete all the child environments of a root environment and then delete the root environment, you can no onger access teh assessment usage data, key metrics, and summary data of all the deleted environments. However, the metering report for the entire tenantwill always contain assessment usage for the entire tenant of Fraud Protection, no matter whether the environments are deleted are not.

You can only delete an environment that has no child environment. If you want to delete a parent that has active child environments, first delete the child environments and then delete the parent.

> [!IMPORTANT]
> You must have at least one environment in your tenant.

## Additional resources

[Payment service provider enablement](psp-overview.md)

[Integrate purchase protection APIs](integrate-real-time-api.md)

[Labels API](labels-api.md)

[Set up device fingerprinting](device-fingerprinting.md)

[View purchase protection schemas](view-purchase-protection-schemas.md)

[Manage rules](rules.md)

[Fraud tracker tool](fraud-tracker.md)
