---
author: yvonnedeq
description: This topic explains 1) how the DFP machine learning model interacts with 3DSv2/PSD2 signals, and 2) offers suggestion to  merchants using 3DSv2.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 09/09/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: How the DFP machine learning model interacts with 3DSv2/PSD2 signals
---

# How the DFP machine learning model interacts with 3DSv2/PSD2 signals (FAQ)

## Summary 

Since ,  all  transactions go through the Payment Services Directive 2 (PSD2) pipeline, **in theory**, the liability has shifted to the banks involved instead of with the merchants.

To the merchant, this basically means the bank can no longer send merchant fraud chargeback requests. The Revised Payment Services Directive (PSD2) provides the merchant with the capability to share more information with the bank. Each transaction that goes through the 3DSecure 2 (3DSv2) pipeline experiences two steps: *authentication* and *authorization*. The bank decides if the authentication will be challenged with strong customer authentication (SCA), or if it will be allowed to continue.  

From very early on, Microsoft adopted the PSD2/3DSv2 protocols, and has been working extensively with various players in the PSD2 realm,.  We have set up various performance metrics to measure industry readiness for PSD2/SCA. 

## Why say the liability has shifted to the banks "in theory"?

3DSv2 was due to be released last year, but since neither the banking industry nor the merchants were ready for this, it was extended another 18 months. Many details have yet to be polished and further defined under the 3DS2 framework. And since the regulations and attitudes of each country are different, even today, banks can’t say when they will be ready to shift the liability until the entire banking industry is ready.

## What Microsoft thinks of 3DSv2

A liability shift sounds like a good idea for the merchant, since it significantly reduces fraud loss from the merchant side.  However, this could lead to a big change on bank industry. To avoid fraud loss, banks will have to set very strict rules and will also have to reject more transactions. This will have an impact on the revenue gain on merchant side. 

Based on our experience, we see a greater monetary impact while the bank authorization rate improved, compared with chargeback reduction gain. Today, we are still observing and not really pushing forward with this change, since we think that there is a greater negative impact rather than a positive one.

Due to Microsoft’s global scale and product offers, we are in a unique position to gauge the industry’s readiness. In Microsoft today, approximately 1% of global transactions currently go through the 3DS2 pipeline (5% PSD2 markets transactions). These are a some of our observations: 

-  Challenge success rates are low to very low.
-  Customers abandon checkouts at a high rate when they are challenged.
-  Issuers rely heavily on Visa/Mastercard for authentication stand-in and authentication approval rates worsen in this case. 

Given these issues, we think the ecosystem is not likely to be ready by the end of 2020. Strict enforcement will hurt consumers and businesses. The European Commission and/or National competent authorities should consider an enforcement delay.

## How Microsoft Dynamics 365 Fraud Protection (DFP) stands on PSD2 and 3DSv2

As a merchant and pioneer company in the industry, Microsoft  works with many banks on 3DSv2 implementation. 3DSv2 is a payment industry requirement which involves many players (for example, merchants, payment processers, payment service providers, payment networks, etc.) across many different countries. Each player group requires many companies to make changes to align with PSD2 and 3DSv2 . 

Due to these requirements, the deadline of enforcing PSD2 moved from September 2019 to Dec 2020, and we are not sure whether this date will be moved out further . We’ve observed that there are still many issues/bugs in the payment flow from each player group and from many companies. But the bottom line is that we are working very closely with Microsoft related teams to implement PSD2 and 3DSv2. 

TAB, one of DFP’s offers, helps merchants share risk assessment and information with issue banks. This helps banks to reduce false positive results and reduce customer frictions (challenges). This can also help issuer banks to identify more frauds. Controlling fraud risks at the lower level is always the correct direction for merchants to take, with or without PSD2, and DFP can help merchants to reach this goal.

DFP currently does not request additional information from merchants for 3DSv2 transactions. Merchants can continue to send standard bank status and purchase status for every assessment event (purchase transactions) for DFP machine learning models. We will inform you if this arrangement changes. .
