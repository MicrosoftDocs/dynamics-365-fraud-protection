---
author: josaw1
description: This article provides information about how you can boost bank acceptance rates.
ms.author: josaw
ms.date: 3/14/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Boost bank acceptance rates
---

# Boost bank acceptance rates

[!include[deprecation](includes/deprecation.md)]

One feature that sets Microsoft Dynamics 365 Fraud Protection apart from other products in the market is the transaction acceptance booster. This feature helps you benefit from higher acceptance rates by sharing trust knowledge with banks. You can choose to share Fraud Protection's assessments directly with participating issuing banks and networks through the acceptance booster service. 

## Acceptance booster service

With participating issuing banks and networks for contextual transaction data, the acceptance booster service provides a direct communication channel called *transaction trust knowledge* and selects other raw attributes about the transaction. This transmission occurs at the time of transaction assessment by Fraud Protection. If the payment instrument used in that transaction was issued by a bank or network participating in the program, Fraud Protection will transmit transaction trust knowledge to that bank or network. 


#### To enable the acceptance booster service:

1. Select **Settings**, and then select **Transaction acceptance booster**. 
2. On the **Opt in** tab, select **Acceptance booster service** to consent to share transaction trust knowledge with participating banks and networks. 
3. Once you've opted-in, you can choose to transmit only the standard transaction trust knowledge or, in addition, share select raw attributes about the transaction. 
4. Select **Consent** to review details about the terms and a list of participants in the program. 
5. Select **Save** to confirm your choice.


### TAB for multi-hierarchy

If your Fraud Protection instance has multiple environments, you can control the TAB settings from each environment individually. The following user roles have permissions to edit these settings: 

- Product admin
- Global admin
- PSP admin
- All areas admin

When the TAB settings are changed in the parent environment, the TAB settings of all its children will be overwritten. Current and future descendants of the parent environment are included in this change. The parent environment's settings take precedence. 

When you modify the TAB settings in a parent environment, you can view the list of child environments that TAB settings will be overwritten for. You can then confirm the changes. The TAB settings page for each child will show a notification about the changes that were made by the parent. You can modify the settings in the parent or child environment multiple times. 

[!INCLUDE[footer-include](includes/footer-banner.md)]
