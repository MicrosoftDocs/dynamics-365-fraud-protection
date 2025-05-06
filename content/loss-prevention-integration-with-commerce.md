---
author: josaw1
description: This article explains how to integrate loss prevention with Microsoft Dynamics 365 Commerce.
ms.author: josaw
ms.date: 04/10/2024

ms.topic: article
search.audienceType:
  - admin
title: Loss prevention integration with Dynamics 365 Commerce
---

# Loss prevention integration with Dynamics 365 Commerce

[!include[deprecation](includes/deprecation.md)]

In Microsoft Dynamics 365 Fraud Protection, the loss prevention capability is a cloud-based solution that helps protect revenue by identifying potential fraud on returns and discounts that arise from omni-channel purchases. Therefore, store managers and investigators can quickly take action to mitigate losses.

To integrate the loss prevention capability with Dynamics 365 Commerce, you must complete these tasks:

1. [Turn on the Azure Data Lake Storage service for your Commerce environment](#turn-on-the-azure-data-lake-storage-service-for-your-commerce-environment).
1. [Turn on the loss prevention feature in your Commerce environment](#turn-on-the-loss-prevention-feature-in-your-commerce-environment).
1. [Add a service account and subscribe to Fraud Protection in your Commerce environment](#add-a-service-account-and-subscribe-to-fraud-protection-in-your-commerce-environment).
1. [Configure loss prevention settings in Fraud Protection](#configure-loss-prevention-settings-in-fraud-protection).

## Turn on the Azure Data Lake Storage service for your Commerce environment

For information about how to turn on the Azure Data Lake Storage service for your Commerce environment, see [Enable Azure Data Lake Storage in a Dynamics 365 Commerce environment](/dynamics365/commerce/enable-adls-environment).

## Turn on the loss prevention feature in your Commerce environment

**To turn on loss prevention integration:**

- Select **Feature management**, and then select **Dynamics 365 Fraud Protection (DFP) Loss Prevention**.

## Add a service account and subscribe to Fraud Protection in your Commerce environment

Next, you must add a service account by registering the application ID for Fraud Protection in the Commerce environment.

1. Select **Finance and Operations Preview**, and then select **Microsoft Entra applications**.
1. To create a new first-party app identity for Fraud Protection, select **New**.
1. In the **Client ID** field, enter ** bf04bdab-e06f-44f3-9821-d3af64fc93a9**.
1. In the **RetailServiceAccount** field, enter the user ID.

## Configure loss prevention settings in Fraud Protection

The next step is to configure the settings so that the loss prevention capability can connect to Azure Data Lake Storage in the Commerce environment.

1. Go to the [Fraud Protection](https://dfp.microsoft.com/) portal, and sign in.
1. In the left navigation, select **Data**, and then select **Data upload**.
1. On the **Data upload** page, on the **Loss prevention** tab, select **Select data source**.
1. Select **Dynamics 365 Commerce** as the data source, and then enter the URL for your Commerce environment.
1. Select **Connect**.

    The URL is stored in the Backend Configuration service for your Fraud Protection environment.

For more information about how to integrate Fraud Protection's loss prevention capability with Commerce, see [Loss prevention in Commerce](/dynamics365/commerce/dev-itpro/DFP#loss-prevention-in-commerce).


[!INCLUDE[footer-include](includes/footer-banner.md)]
