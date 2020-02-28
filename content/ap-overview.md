---
author: v-davido
description: This topic provides an overview of the account protection experience in the Microsoft Dynamics 365 Fraud Protection system.
ms.author: amirat
ms.service: fraud-protection
ms.date: 03/01/2020


ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account protection overview
---

# Account protection overview

[!include [banner](includes/preview-banner.md)]

Dynamics 365 Fraud Protection provides merchants the capability to assess the risk that attempts to create new accounts and attempts to login on merchant’s ecosystem are fraudulent. Rish assessment in Fraud Protection can be used by the customer to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts.    

Account protection includes APIs for real-time risk assessment, rule and list experience to optimize risk strategy as per your business needs, and a scorecard to monitor fraud protection effectiveness and trends in your ecosystem.

Account protection capability provides risk assessment on two types of account lifecycle events: 

- **Account Creation** 

- **Account Login**.

For each event type there are multiple layers of defense: 

- **Efficient bot detection:** Merchants can encounter automated attempts to create fake accounts or to compromise existing accounts using a list of compromised credentials or through brute force. As the first line of defense, Fraud Protection’s advanced, adaptive AI enables dynamic and robust bot detection by quickly providing the merchant with a score that maps to the probability that a bot is initiating the event. Merchants can use the score in conjunction with the rules they’ve configured to block automated fraudulent account creation and login attempts or add additional verification on suspicious attempts.

- **Real-time reinforced assessment:** as the next line of defense, Fraud Protection uses AI models to generate risk assessment scores for account creation and account login events. Merchants can leverage this score in conjunction with the rules they’ve configured to approve, challenge, reject or review these account creation and account login attempts based on custom business needs.

## Additional resources

- [Integrate account protection APIs](integrate-ap-api.md)

- [Manage account protection rules and lists](ap-rulesandlists.md)

- [Learn from the account protection scorecard](ap-scorecard.md)
