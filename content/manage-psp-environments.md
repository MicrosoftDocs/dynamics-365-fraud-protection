---
author: josaw1
description: This article explains how payment service providers (PSPs) can manage environments in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/08/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Manage environments
---

# Manage environments

By creating additional new environments, customers can have greater flexibility and enhance the functionality that's provided by Microsoft Dynamics 365 Fraud Protection to scale the solution to support their other business units. For example, customers can create organizations or divisions as root environments, and configure their child environments as different departments, business, or product types. In this way, rules, user access, configuration, and other fraud protection settings can be inherited from the parent level. Transaction data and reports will then be aggregated at the parent environment, so that business leaders can get an overview of an organization's or division's performance.

## Create a new environment

To create a new environment, or switch between environments, select **Manage environments** under the environment switcher in the upper right of the Fraud Protection portal page. 

> [!NOTE]
> A root environment is an environment that's at the top level of the Fraud Protection tenant and that has no parent environment. There can be multiple root environments in the Fraud Protection tenant. The **Product admin** role is required to create a new root environment. For more information, see [Configure user access](configure-user-access.md).

To create a new environment, select **New environment** at the top, and then enter the following information: 

- **Data storage geography** – Select the geography where your customer data resides. For more information about data residency, see [Data residency FAQ](faq/data-residency-faq.md).
- **Name** – Enter the name of the environment that you want to create.
- **Description (optional)** – You can add some information to help identify the environment.
- **Tags (optional)** – You can use tags to specify any generic information that's related to the environment, such as the industry vertical.
- **Microsoft Entra application ID (optional)** – If you want an existing Microsoft Entra application ID to access the environment, paste the application ID here. This approach is recommended if you plan to reuse API access credentials across two or more environments. For a list of available applications, go to **Create Microsoft Entra applications** or **Microsoft Entra ID** on the **Integration** page.
- **Create API ID (optional)** – You can enter an identifier that should be used instead of the Fraud Protection environment ID when events are sent to Fraud Protection.

> [!NOTE]
> To create a Microsoft Entra application, the user must also be assigned the Application Administrator, Cloud Application Administrator, or Global Administrator role in your Microsoft Entra tenant. For more information about Microsoft Entra applications and integration, see [Integrate purchase protection API](integrate-real-time-api.md) and [Integrate account protection APIs](faq/data-residency-faq.md). 
>
> After you create the environment, you can't change the customer API ID.

An environment that's created under another environment is known as a child environment. The environment that's on top of another environment in the hierarchy is known as the parent environment. By default, some settings and configurations of child environments follow the parent environment. By default, the child environment also inherits the user access configuration of the parent environment. 

To create a child environment under another environment, follow these steps. 

1. Select the ellipsis (**...**) next to the environment, and then select **New child environment** on the menu. 
2. Enter the information for the child environment. For a child environment, the **Data storage geography** value must match the value of the root environment. 
3. Select **Create**.

## View environments

To view a list of all the environments under your tenant, select **Manage environment** under the environment switcher. 

You can favorite an environment by selecting the star symbol next to it. In this way, you can access the environment under **Favorites** in the environment switcher. You can then export the list of environments from the **Manage environment** page. 

## Edit an existing environment

To edit an environment, follow these steps.

1. Select **Manage environment** under the environment switcher.
2. Select the ellipsis (**...**) next to the environment, and then select **Edit** on the menu.

Only the **Name**, **Description**, and **Tags** fields can be edited. 

## Delete an environment

To delete and environment, follow these steps.

1. Select **Manage environment** under the environment switcher.
2. Select the ellipsis (**...**) next to the environment, and then select **Delete** on the menu.

When an environment is deleted, the transactions, rules, cases, and other data that's associated with it is deleted. However, usage data, the transaction count, and the aggregated report is retained. 

If you delete a child environment, the metering report in the parent environment still shows the assessment usage that's associated with the deleted environment. In a similar way, the key metrics and summary data of the parent environment still contain the transactions that are associated with the deleted environment. If you delete all the child environments of a root environment and then delete the root environment, you can no longer access the assessment usage data, key metrics, and summary data of the deleted environments. However, the metering report for the whole tenant always shows the assessment usage for the whole Fraud Protection tenant, regardless of whether the environments are deleted.

You can delete an environment only if it has no child environments. If you want to delete a parent that has active child environments, first delete the child environments, and then delete the parent.

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
