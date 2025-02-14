---
author: josaw1
description: This article provides an overview of the account protection experience in the Microsoft Dynamics 365 Fraud Protection system.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: overview
search.audienceType:
  - admin
title: Account protection overview

---

# Account protection overview

[!include[deprecation](includes/deprecation.md)]

Microsoft Dynamics 365 Fraud Protection provides merchants the capability to assess if the risk of attempts to create new accounts and attempts to log in on merchant’s ecosystem are fraudulent. Risk assessment in Fraud Protection can be used by the customer to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts.    

Account protection includes APIs for real-time risk assessment, rule, and list experience to optimize risk strategy as per your business needs, and monitoring dashboards to monitor fraud protection effectiveness and trends in your ecosystem.

## Account lifecycle event types

Account protection provides risk assessment on two types of account lifecycle events: 

- **Account creation** 
- **Account login**

### Layers of defense

Each event type has multiple layers of defense: 

- **Efficient bot detection:** Merchants can encounter automated attempts to create fake accounts or to compromise existing accounts using a list of compromised credentials or through brute force. As the first line of defense, Fraud Protection’s advanced, adaptive AI enables dynamic and robust bot detection by quickly providing the merchant with a score that maps to the probability that a bot is initiating the event. Merchants can use the score with the rules they’ve configured to block automated fraudulent account creation and login attempts or add another verification on suspicious attempts.

- **Real-time reinforced assessment:** As the next line of defense, Fraud Protection uses AI models to generate risk assessment scores for account creation and account login events. Merchants can apply this score in conjunction with the rules they’ve configured to approve, challenge, reject, or review these account creation and account login attempts based on custom business needs.

## Additional resources

- [Integrate account protection APIs](integrate-ap-api.md)
- [Manage lists](lists.md)
- [Manage rules](rules.md)
- [Account protection monitoring dashboards](monitoring-dashboards.md)
- [Account protection schemas](ap-schema.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
