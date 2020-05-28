---
author: yvonnedeq
description: Loss prevention - integration with Commerce
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 05/18/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Integration with Commerce

---


# Integration with Commerce


## Enabling the Loss Prevention integration with Commerce

### 1.	Enable ADLS for your Commerce environment
For the data to be available in ADLS, the service must be enabled for the Dynamics 365 Commerce environment. For details on enabling ADLS for your Commerce environment, see [Enable ADLS in a Dynamics 365 Commerce environment](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fdynamics365%2Fcommerce%2Fenable-adls-environment&data=02%7C01%7CVenkat.Ganesan%40microsoft.com%7Ccf5b733b8bfe4b0a8a5808d7f9bba9cd%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637252456709418649&sdata=yyr87Ca7vxWSiaHT9b5v6zqKsD1MTs3zORC%2B0UZFaRo%3D&reserved=0).

### 2.	Turn on the Loss Prevention feature
The Loss Prevention integration can be enabled through the Feature Management workspace in Commerce. The feature is called "Dynamics 365 Fraud Protection (DFP) Loss Prevention". This is the only setup step within Commerce that is required to enable the integration.

### 3.	Subscribe to DFP
The retailer needs to register the DFP app id inside of F&O by going to the Azure Active Directory Applications form and creating a new entry for the Dynamics Fraud Protection first party app id (bf04bdab-e06f-44f3-9821-d3af64fc93a9) and assign it a User Id of "RetailServiceAccount"


### 4.	Configure Loss Prevention in DFP

Once the ADLS environment has been configured and the Loss Prevention feature is turned on, the merchant can then proceed to set up the Fraud Protection environment, where the Loss Prevention settings can be configured to connect to the ADLS of the Commerce environment. The merchant would navigate to the DFP portal and connect their F&O environment to their DFP environment. This URL will be stored in the DFP Backend Configuration service configuration for the retailer's DFP environment. 

For more information on integration with Fraud Protection's loss prevention, see [Dynamics 365 Fraud Protection integration with Dynamics 365 Commerce](https://docs.microsoft.com/en-us/dynamics365/commerce/dev-itpro/DFP).


