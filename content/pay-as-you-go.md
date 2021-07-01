---
author: josaw1
description: This topic explains how to enable Pay as you go billing for Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 07/08/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Pay as you go billing
---

# Pay as you go billing

This topic describes how to get started with Pay as you go billing for Dynamics 365 Fraud Protection. With Pay as you go billing, you can use Fraud Protection as much or as little as you need, and you pay only for what you use. Service interruptions will be minimized and you won't overpay as a result of forecasted transaction volumes.


## Pricing

If you are an existing Fraud Protection customer and want to switch to Pay as you go billing, contact your Microsoft partner to discuss updated pricing.

With Pay as you go, your total bill amount every month is determined based on how many Fraud Protection transactions you processed that month per capability. Prices become more favorable as your monthly usage grows. The tables below provide detailed pricing for each capability of Fraud Protection.

**Fixed Monthly fee:** $12 per month per AAD tenant.

### Pricing tiers for account protection

| Transactions | Cost|
|-----------------------------|--------------------------------------------------|
| < 100,000 transactions per month | $0.01  per transaction |
| 100,000 - 1,300,000 transactions per month | $0.0075 per transaction |
| >= 1,300,000 transactions per month | $0.005 per transaction |

### Pricing tiers for loss prevention

| Transactions | Cost|
|-----------------------------|--------------------------------------------------|
| < 20,000 transactions per month | $0.05 per transaction |
| 20,000 - 160,000 transactions per month | $0.0375 per transaction |
| >= 160,000 transactions per month | $0.025 per transaction |

### Pricing tiers for purchase protection

| Transactions | Cost|
|-----------------------------|--------------------------------------------------|
| < 10,000 transactions per month | $0.1  per transaction |
| 10,000 - 300,000 transactions per month | $0.075 per transaction |
| >= 300,000 transactions per month | $0.05 per transaction |

## Prerequisites

To enable Pay as you go billing, you need the following subscriptions. 
- Monthly subscription for the Fraud Protection Pay as you go SKU.
- Active Azure subscription.

You also need the following permissions.
- Global administrator permissions for Fraud Protection in an existing AAD tenant.
- Contributor permissions for an Azure subscription.

## Enable Pay as you billing

To enable Pay as you go billing, complete the steps below.

1. Set up a monthly subscription for Fraud Protection.
    1. Go to the [Fraud Protection website](https://dynamics.microsoft.com/ai/fraud-protection/) and select **Buy Now**.
    1. Sign in as the global administrator of the same AAD tenant that you want to use with Fraud Protection. If you don’t have an AAD tenant, you can sign up for one by following the instructions on the page.
    1. Complete the steps in the purchase flow. You’ll receive confirmation that your monthly subscription for Fraud Protection Pay as you go is successfully set up. You'll then be redirected to the Fraud Protection portal. 

2. Set up your Fraud Protection environment.
    1. On the [Fraud Protection portal](https://dfp.microsoft.com/), sign in as the global administrator of the AAD tenant that you used in Step 1 above.
    1. If you already set up your Fraud Protection environment for your free trial, the Fraud Protection portal loads after you sign in and you can proceed to the next step. If you haven't set up your environment, follow the instructions in the [Set up a purchased version of Dynamics 365 Fraud Protection](promocode-set-up-dfp-purchased-version.md#complete-the-setup-process) topic.

3. Configure an Azure subscription for Fraud Protection billing.
    1. In a new browser tab, go to the [Azure portal](https://portal.azure.com/) and sign in with the same credentials you used in Step 2. 
    1. Search for "Subscriptions" in the **Search** field, and then select **Subscriptions** to go the page that lists all of the Azure Subscriptions that you have access to. If no subscriptions are displayed, you can create a new one. To create a subscriptions, select **Add**. For more information on the subscription options, see [Create an additional Azure subscription](/azure/cost-management-billing/manage/create-subscription.md).
    1. Select the subscription you want to use for Fraud Protection billing.
    1. Select **Resource group** under **Settings** in the left menu. Select **Create** to create a new resource group.
    1. On the **Create a resource group** page, select a name and Azure region.
    1. Select **Review + create** in the bottom left corner. After Azure validates the information, select **Create** to create the resource group. 
    1. You’ll receive a notification in the Azure portal confirming that the resource group was successfully created. Make a note of the name of the Azure subscription and resource group because you'll need them to set up Pay as you go billing in the next step. 

4. Enable Pay as you go billing.
    1. Return to the [Fraud Protection portal](https://dfp.microsoft.com/) and on the home page, select **Enable**.
    1. Select the Azure subscription and resource group you configured in Step 3 and select **Enable**. You’ll receive confirmation that setup for Pay as you go was successful. 
    
To learn more about what type of Fraud Protection usage is billable, see the [Assessment usage and metering](metering.md) topic.
