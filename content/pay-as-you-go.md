---
author: josaw1
description: This article explains how to enable Pay as you go billing for Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Pay as you go billing
---

# Pay as you go billing

This article = how to get started with Pay as you go billing for Dynamics 365 Fraud Protection. With Pay as you go billing, you can use Fraud Protection as much or as little as you need, and you pay only for what you use. Service interruptions will be minimized and you won't overpay as a result of forecasted transaction volumes. If Pay as you go billing option is chosen, then it applies to all the environments in the Fraud Protection tenant.

## Pricing

If you are an existing Fraud Protection customer and want to switch to Pay as you go billing, contact your Microsoft partner to discuss updated pricing.

With Pay as you go, your total bill amount every month is determined based on how many Fraud Protection transactions you processed that month per capability. Prices become more favorable as your monthly usage grows. The following tables provide detailed pricing for each capability of Fraud Protection.

**Fixed monthly fee:** $12 per month per Microsoft Microsoft Entra tenant.

### Pricing tiers for account protection

| Transactions | Cost per transaction |
|-----------------------------|--------------------------------------------------|
| Less than 100,000 transactions per month | $0.01  |
| 100,000 to 1,300,000 transactions per month | $0.0075 |
| Greater than 1,300,000 transactions per month | $0.005  |

### Pricing tiers for loss prevention

| Transactions | Cost per transaction |
|-----------------------------|--------------------------------------------------|
| Less than 20,000 transactions per month | $0.05 |
| 20,000 to 160,000 transactions per month | $0.0375 |
| Greater than 160,000 transactions per month | $0.025 |

### Pricing tiers for purchase protection

| Transactions | Cost per transaction|
|-----------------------------|--------------------------------------------------|
| Less than 10,000 transactions per month | $0.1  |
| 10,000 to 300,000 transactions per month | $0.075  |
| Greater than 300,000 transactions per month | $0.05  |

## Prerequisites

To enable Pay as you go billing, you need the following subscriptions. 

- Monthly subscription for the Fraud Protection Pay as you go SKU.
- Microsoft Entra subscription.

You also need the following permissions.

- Global administrator permissions for Fraud Protection in an existing Microsoft Entra tenant.
- Contributor permissions for a Microsoft Azure subscription.

## Enable Pay as you go billing

To enable Pay as you go billing, complete the following steps.

1. Set up a monthly subscription for Fraud Protection.

    1. Open [this page](https://signup.microsoft.com/get-started/signup?products=3cec0759-69e5-4cc4-940c-0760556f4b80) in an inPrivate browser tab.
    1. Sign in as the global administrator of the same Microsoft Entra tenant that you want to use with Fraud Protection. If you don't have an Microsoft Entra tenant, you can sign up by following the instructions on the page.
    1. Complete the steps in the purchase flow. You'll receive confirmation that your monthly subscription for Fraud Protection Pay as you go is successfully set up. You'll then be redirected to the Fraud Protection portal. 

2. Set up your Fraud Protection environment.

    1. In the [Fraud Protection portal](https://dfp.microsoft.com/), sign in as the global administrator of the Microsoft Entra tenant that you used in step 1.
    1. If you've already set up the Fraud Protection environment for your free trial, the Fraud Protection portal will be loaded after you sign in. You can then move on to the next step. If you haven't set up your environment, follow the instructions in [Set up a purchased version of Dynamics 365 Fraud Protection](promocode-set-up-dfp-purchased-version.md#complete-the-setup-process).

3. Configure an Azure subscription for Fraud Protection billing.

    1. In a new browser tab, go to the [Azure portal](https://portal.azure.com/) and sign in with the same credentials that you used in step 2. 
    1. Search for "Subscriptions" in the **Search** field, and then select **Subscriptions** to go the page that lists all of the Azure subscriptions that you have access to. If no subscriptions are displayed, you can create a new one. To create a subscription, select **Add**. For more information, see [Create an additional Azure subscription](/azure/cost-management-billing/manage/create-subscription).
    1. Select the subscription that you want to use for Fraud Protection billing.
    1. Select **Resource group** under **Settings** in the left menu. Select **Create** to create a new resource group.
    1. On the **Create a resource group** page, select a name and Azure region.
    1. Select **Review + create** in the lower left. After the information is validated, select **Create** to create the resource group. 
    1. You'll receive a notification in the Azure portal confirming that the resource group was successfully created. Make a note of the name of the Azure subscription and the resource group. You'll need this information to set up Pay as you go billing in the next step. 

4. Enable Pay as you go billing.

    1. Return to the [Fraud Protection portal](https://dfp.microsoft.com/). You must have the Global admin role or Product admin role. On the home page, select **Enable**.
    1. Select the Azure subscription and resource group that you configured in step 3 and select **Enable**. You'll receive confirmation that setup for Pay as you go was successful. 

To learn more about what type of Fraud Protection usage is billable, see [Assessment usage and metering](metering.md).
