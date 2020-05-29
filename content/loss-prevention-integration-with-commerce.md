---
author: yvonnedeq
description: Integrating loss prevention with Commerce
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 05/28/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Integrate loss prevention with Dynamics 365 Commerce

---


# Integrate loss prevention with Dynamics 365 Commerce

In Microsoft Dynamics 365 Fraud Protection, loss prevention is a cloud-based solution designed to help retailers like you decrease in-store fraud costs and improve operational efficiencies and revenue.  It allows you to combat fraud associated with returns, discounts, merchandise mishandling, and inventory turn-over.

To integrate loss prevention with Dynamics 365 Commerce (Commerce), perform the following steps:

- Enable the Azure Data Lake Storage (ADLS) service for the Commerce environment.
- Enable loss prevention in the Commerce environment.
- Subscribe to Fraud Protection.
- Configure loss prevention settings in Fraud Protection. 


## 1.	Enable ADLS for your Commerce environment

For information on how to enable the ADLS data service for your Commerce environment, see [Enable ADLS in a Dynamics 365 Commerce environment](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fdynamics365%2Fcommerce%2Fenable-adls-environment&data=02%7C01%7CVenkat.Ganesan%40microsoft.com%7Ccf5b733b8bfe4b0a8a5808d7f9bba9cd%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637252456709418649&sdata=yyr87Ca7vxWSiaHT9b5v6zqKsD1MTs3zORC%2B0UZFaRo%3D&reserved=0).

## 2.	Turn on the loss prevention feature in your Commerce environment

Only one step is required to enable loss prevention integration. 

- Select **Feature management**, and then select **Dynamics 365 Fraud Protection (DFP) Loss Prevention**. 

## 3.	Subscribe to Fraud Protection

Next, register the Fraud Protection application ID.

1. Select **Finance and Operations Preview**, and then select **Azure Active Directory applications**.
1. To create a new first party app identity for the Fraud Protection, select **New**, and then add **bf04bdab-e06f-44f3-9821-d3af64fc93a9** as the **Client ID**.
1. Assign the **User Id** to **RetailServiceAccount**.

## 4.	Configure Loss Prevention in DFP

After configuring the ADLS environment and turning on loss prevention, the next step is to set up the Fraud Protection environment and configure the loss prevention settings to connect to ADLS in the Commerce environment. 

1. Navigate to the Fraud Protection portal. 
1. To connect to the **Finance and Operations** environment, select **Connect to data**.
2. In the **Connect to Dynamics 365 Commerce** dialog, enter the URL for the Commerce environment.

    The URL is stored in the **Backend Configuration** service for your Fraud Protection environment.

For more information on integration with Fraud Protection's loss prevention, see [Dynamics 365 Fraud Protection integration with Dynamics 365 Commerce](https://docs.microsoft.com/dynamics365/commerce/dev-itpro/DFP#loss-prevention-in-commerce).


