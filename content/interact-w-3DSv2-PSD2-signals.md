---
author: yvonnedeq
description: This topic explains 1) how the DFP machine learning model interacts with 3DSv2/PSD2 signals, and 2) offers suggestion to  merchants using 3DSv2.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/13/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: How the DFP machine learning model interacts with 3DSv2/PSD2 signals
---

# How the DFP machine learning model interacts with 3DSv2/PSD2 signals (FAQ)

## Summary 

Any transactions go through PSD2 pipeline, **in theory**, Liability will be shifted to bank. To merchant, it basically means bank can't send merchant fraud chargeback request anymore. PSD2 provides the capability for merchant to share more information to bank. Each transaction goes through 3DSv2 Pipeline will experience two steps: Authentication and Authorization. The bank makes the decision whether the authentication will be frictionless or be challenged with strong customer authentication (SCA).  Microsoft has adopted PSD2/3DSv2 and has been working extensively various players in the PSD2 realm from very early on.  We have set up various performance metrics to measure industry readiness for PSD2/SCA.   

## Why "in Theory"?

Even 3DSv2 was due last year, but industry from bank to merchant are not ready for this yet, so it was extended another 18 months. So many details need to be polished and further defined under the 3DS2 framework. Due to the regulation and attitude from each country are different, even bank today can say they are not ready for this yet, so the liability shift will not happen too soon till entire industry is ready for this.

## What Microsoft think about 3DSv2?

Liability shift sounds like a good idea for merchant, that will reduce fraud loss significantly from merchant side.  However, this might lead to the big change on bank industry, to avoid fraud loss, bank will set very strict rules to reject more transactions. This will for sure impact the revenue gain on merchant side. Based on our experience, we see a lot more monetary impact while bank auth rate improved, in comparison with chargeback reduction gain. Today, we are still observing and not really pushing forward this change, as we think that there is more negative impact than positive one.

Due to Microsoft global scale and product offers, we are in a unique position to gauge the industry readiness. In Microsoft today, roughly 1% global transactions currently are going through 3DS2 Pipeline (5% PSD2 markets transactions). Here are a few of our observations: Challenge success rates are low to very low; Customer abandon checkout at high rate when challenged; Issuers rely heavily on Visa/Mastercard for authentication stand-in and authentication approval rates worsen in this case. As such, we think the ecosystem is not likely to be ready by the end of 2020. Strict enforcement will hurt the consumers and businesses. The European Commission and/or National competent authorities should consider an enforcement delay.

## Where are DFP standing on PSD2 and 3DSv2?

Microsoft as a merchant is working with many banks for 3DSv2 implementation. We are very confident to say that we are the pioneer company in the industry.  3DSv2 is an payment industry requirement, which involves in many players such as merchant, payment processers, payment service provider, payment networks etc. across many different countries, and in each player group, it requires many companies to make changes to align with PSD2 and 3DSv2 . The deadline of enforcing PSD2 had been moved from last September 2019 to Dec 2020. At this moment, we are not sure whether this date will be further moved or not. From our observation, there are still many issues/bugs in the payment flow from each player group and many companies. But the bottom line is that we are working very closely with Microsoft related teams on PSD2 and 3DSv2.

One of DFP offers, TAB, can help merchants to share risk assessment and information with issue banks which can help banks to reduce false positive and therefore reduce customer frictions. It also can help issuer banks to identify more frauds. Control fraud risk at lower level is always right direction for merchants no matter with or without PSD2. DFP can help merchants to reach this goal.

DFP currently do not request additional information from merchants for 3DSv2 transactions. Merchants will continue to send standard bank status and purchase status for every assessment event (purchase transactions) for DFP machine learning models. We would inform you if anything changed.
