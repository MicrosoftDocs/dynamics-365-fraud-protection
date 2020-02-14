---
author: amirat
description: This topic provides an overview of AP Preview offering.
ms.author: amirat
ms.service: fraud-protection
ms.date: 2/14/2020


ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Account Protection Overview
---
# Account Protection Overview

Dynamics 365 Fraud Protection (DFP) provides merchants the capability to assess the risk that attempts to create new accounts and attempts to login on merchant’s ecosystem are fraudulent. DFP’s risk assessment can be used by the customer to block or challenge suspicious attempts to create new fake accounts or to compromise existing accounts.    

Account Protection includes APIs for real time risk assessment, rule and list experience to optimize risk strategy as per your business needs, and a scorecard to monitor fraud protection effectiveness and trends in your ecosystem.

Account Protection capability provides risk assessment on two types of Account lifecycle events: 

- **Account Creation** 

- **Account Login** 

For each event type there are multiple layers of defense: 

- **Efficient bot detection:** Merchants can encounter automated attempts to create fake accounts or to compromise existing accounts using a list of compromised credentials or through brute force. As the first line of defense, DFP’s advanced, adaptive AI enables dynamic and robust bot detection by quickly providing the merchant with a score that maps to the probability that a bot is initiating the event. merchants can use the score in conjunction with the rules they’ve configured to block automated fraudulent account creation and login attempts or add additional verification on suspicious attempts.

- **Real time Reinforced Assessment:** as the next line of defense, DFP uses AI models to generate risk assessment scores for Account Creation and Account Login events. Merchant can leverage this score in conjunction with the rules they’ve configured to approve, challenge, reject or review these Account Creation and Account Login attempts based on custom business needs.

Learn more about the following features used in account protection: 

- Integrate account protection APIs (link to Kelsie's new AP doc on APIs) 

- Manage account protection rules & lists (link to Lena's new AP doc on Rules ) 

- Learn from Account Protection Scorecard (link to Lena's new AP doc on Scorecard) 
