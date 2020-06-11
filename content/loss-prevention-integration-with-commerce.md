---
author: yvonnedeq
description: Integrating loss prevention with Commerce
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

In Microsoft Dynamics 365 Fraud Protection, the loss prevention capability is a cloud-based solution that helps protect revenue by identifying potential fraud on returns and discounts arising from omni-channel purchases, enabling store managers and investigators to quickly take action to mitigate losses.

To integrate loss prevention capability with Dynamics 365 Commerce (Commerce), perform the following steps:

1. [Enable the Azure Data Lake Storage (ADLS) service for the Commerce environment.](loss-prevention-integration-with-commerce.md#1enable-adls-for-your-commerce-environment)
1. [Enable loss prevention in the Commerce environment.](loss-prevention-integration-with-commerce.md#2turn-on-the-loss-prevention-feature-in-your-commerce-environment)
1. [Add a service account and subscribe to Fraud Protection in the Commerce environment.](loss-prevention-integration-with-commerce.md#3add-a-service-account-and-subscribe-to-fraud-protection)
1. [Configure loss prevention settings in Fraud Protection.](loss-prevention-integration-with-commerce.md#4configure-loss-prevention-in-fraud-protection) 


## 1.	Enable ADLS for your Commerce environment

For information on how to enable the ADLS data service for your Commerce environment, see [Enable ADLS in a Dynamics 365 Commerce environment](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fdynamics365%2Fcommerce%2Fenable-adls-environment&data=02%7C01%7CVenkat.Ganesan%40microsoft.com%7Ccf5b733b8bfe4b0a8a5808d7f9bba9cd%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637252456709418649&sdata=yyr87Ca7vxWSiaHT9b5v6zqKsD1MTs3zORC%2B0UZFaRo%3D&reserved=0).

## 2.	Turn on the loss prevention feature in your Commerce environment

Only one step is required to enable loss prevention integration. 

- Select **Feature management**, and then select **Dynamics 365 Fraud Protection (DFP) Loss Prevention**. 

## 3.	Add a service account and subscribe to Fraud Protection

Next, add a service account by registering the Fraud Protection application ID in the Commerce environment.

1. Select **Finance and Operations Preview**, and then select **Azure Active Directory applications**.
1. To create a new first party app identity for the Fraud Protection, select **New**.
1. In the **Client ID** box, enter *bf04bdab-e06f-44f3-9821-d3af64fc93a9*.
1. Assign the **User Id** to **RetailServiceAccount**.

## 4.	Configure loss prevention in Fraud Protection

After configuring the ADLS environment and turning on the loss prevention capability, the next step is to set-up and configure the loss prevention capability settings to connect to ADLS in the Commerce environment. 

1. Navigate to the [Fraud Protection]( https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal and sign in. 
1. To connect to the Finance and Operations environment, select **Connect to data**.
1. In the **Connect to Dynamics 365 Commerce** dialog, enter the URL for the Commerce environment.

    The URL is stored in the **Backend Configuration** service for your Fraud Protection environment.

For more information on how to integrate Commerce with with Fraud Protection's loss prevention capability, see [Dynamics 365 Fraud Protection integration with Dynamics 365 Commerce](https://docs.microsoft.com/dynamics365/commerce/dev-itpro/DFP#loss-prevention-in-commerce).


