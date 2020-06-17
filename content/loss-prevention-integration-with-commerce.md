---
author: yvonnedeq
description: This topic explains how to integrate loss prevention with Microsoft Dynamics 365 Commerce.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/11/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Loss prevention integration with Dynamics 365 Commerce

---

# Loss prevention integration with Dynamics 365 Commerce

In Microsoft Dynamics 365 Fraud Protection, the loss prevention capability is a cloud-based solution that helps protect revenue by identifying potential fraud on returns and discounts that arise from omni-channel purchases. Therefore, store managers and investigators can quickly take action to mitigate losses.

To integrate the loss prevention capability with Dynamics 365 Commerce, you must complete these tasks:

1. [Turn on the Azure Data Lake Storage service for your Commerce environment](#turn-on-the-azure-data-lake-storage-service-for-your-commerce-environment).
1. [Turn on the loss prevention feature in your Commerce environment](#turn-on-the-loss-prevention-feature-in-your-commerce-environment).
1. [Add a service account and subscribe to Fraud Protection in your Commerce environment](#add-a-service-account-and-subscribe-to-fraud-protection-in-your-commerce-environment).
1. [Configure loss prevention settings in Fraud Protection](#configure-loss-prevention-settings-in-fraud-protection).

## Turn on the Azure Data Lake Storage service for your Commerce environment

For information about how to turn on the Azure Data Lake Storage service for your Commerce environment, see [Enable Azure Data Lake Storage in a Dynamics 365 Commerce environment](https://docs.microsoft.com/dynamics365/commerce/enable-adls-environment).

## Turn on the loss prevention feature in your Commerce environment

Follow this step to turn on loss prevention integration.

- Select **Feature management**, and then select **Dynamics 365 Fraud Protection (DFP) Loss Prevention**.

## Add a service account and subscribe to Fraud Protection in your Commerce environment

Next, you must add a service account by registering the application ID for Fraud Protection in the Commerce environment.

1. Select **Finance and Operations Preview**, and then select **Azure Active Directory applications**.
1. To create a new first-party app identity for Fraud Protection, select **New**.
1. In the **Client ID** field, enter **bf04bdab-e06f-44f3-9821-d3af64fc93a9**.
1. Assign the **User Id** to **RetailServiceAccount**.

## Configure loss prevention settings in Fraud Protection

The next step is to configure the settings so that the loss prevention capability can connect to Azure Data Lake Storage in the Commerce environment.

1. Go to the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, and sign in.
1. To connect to the Finance and Operations environment, select **Connect to data**.
1. In the **Connect to Dynamics 365 Commerce** dialog box, enter the URL of the Commerce environment.

    The URL is stored in the Backend Configuration service for your Fraud Protection environment.

For more information about how to integrate Fraud Protection's loss prevention capability with Commerce, see [Loss prevention in Commerce](https://docs.microsoft.com/dynamics365/commerce/dev-itpro/DFP#loss-prevention-in-commerce).
