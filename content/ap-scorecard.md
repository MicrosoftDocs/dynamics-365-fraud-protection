---
author: zhuoche
description: This topic explains the scorecard capability of Dynamics 365 Fraud Protection account protection.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 02/20/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin


title: Learn from the account protection scorecard
---


# Learn from the account protection scorecard


Dynamics 365 Fraud Protection with account protection helps protect your e-commerce business from fraud related to fake accounts and account compromise. Your account protection scorecard shows you, in real-time, how Account Protection is working. For example, the scorecard shows you how many events are high risk. You can use the scorecard to make well-informed risk management decisions for your online business. 

## Account protection assessment type

You can select the account protection assessment type by clicking the **tab** menu on the top of the page. The following types are available:

- Account Creation 
- Account Login

## Customize your view

You can use the drop-down menus to filter your view of the interactive charts. The following option is available:

- **Event time**: Show event data by time. You can select to view events within last hour or last 24 hours. 

## Key performance indicators (KPI) charts

The scorecard shows metrics in the following sections:

### Bot model score

The Bot model provides insights about how bots are engaging your e-commerce platform. The bot score is a number between 0 to 999 that indicates the probability that a bot, rather than a person, is attempting to create a new account or log-in to an account. A higher score indicates high probability that a bot is initiating the event. Elements you can analyze:

- **Bot score distribution**: The Bot score distribution chart shows the event volume aggregated by bot model score. 
- **Top bot countries and regions**: Top bot countries graph shows the geographic view of the five countries and regions initiating the highest number of bot encounters, defined as percentage of total events initiated from that country or region that have a bot score higher than 900.

### Risk model score

Risk model score, between 0 to 999, indicates the likelihood that an event is fraudulent. A low score indicates low probability of fraud. You can analyze the following:

- **Risk score distribution**: Risk score distribution chart shows the event volume aggregated by risk model score. 
- **Top risk countries and regions**: Top risk countries graph shows the geographic view of the five countries and regions with the highest bot encounter rates, defined as events with a risk score higher than 900.

### Rule decision

Risk decision section shows metrics from the automated decision rules you’ve created. You can define rules to automate your decisions about accepting or rejecting an event based on your business need. The following metrics are available:

- **Rule decision trend**: Rule decision trend chart shows percentage of Approved, Rejected, Challenged, and Reviewed decisions by rules. 
- **Top rules**: List of rules that triggered the highest volume of automated decisions.

To learn more about rules, view rules documentation (link TBD)

## Related topics: (link tbd)
- Account protection overview
- View Account Protection Schemas
- Manage Rules and Lists
