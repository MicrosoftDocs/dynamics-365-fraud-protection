---
author: zhuoche
description: This topic explains the scorecard capability of Dynamics 365 Fraud Protection account protection.
ms.author: zhuoche
ms.service: fraud-protection
ms.date: 1/30/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin


title: Account protection Scorecard
---


# Learn from the scorecard


Your top-four key performance indicators (KPIs) are summarized across the top of the page to provide a snapshot of your performance. You can fully investigate these metrics in the charts.

You can use the scorecard reports to review your key metrics and understand the recent performance of your account protection efforts. 

Your account protection scorecard reflects the real-time performance of Account Protection as our system of record. After evaluating the data presented in the scorecard, you can use the knowledge that you gain to make well-informed risk management decisions for your online business.

## Account Protection Assessment Type

You can select the Account Protection assessment type by clicking the tab menu on the top of the page. The following types are available:

- **Account Creation** 
- **Account Login**

## Customize your view

You can use the drop-down menus to filter your view of the interactive charts. The following option is available:

- **Transaction time** – Show transaction data by time. You can select to view transactions within last hour or last 24 hours. 

## KPI charts

The scorecard shows metrics in the following sections:

### Bot Model Score

Bot model score section shows insights from the bot ML model. The bot score is a number within the range of 0 to 999, where lower score indicates low probability of bot attack and higher score indicates high probability of bot attack. The following metrics are available:

- **Bot score distribution** – Bot score distribution chart shows the transaction volume aggregated by bot model score. 
- **Top bot countries** – Top bot countries graph shows the geographic view of top 5 countries with a high percentage of bot attack, defined as a bot score higher than 900.

### Risk Model Score

Risk model score section shows insights from the fraud risk ML model. The risk score is a number within the range of 0 to 999, where lower score indicates low probability of fraud attack and higher score indicates high probability of fraud attack. The following metrics are available:

- **Risk score distribution** – Risk score distribution chart shows the transaction volume aggregated by risk model score. 
- **Top risk countries** – Top bot countries graph shows the geographic view of top 5 countries with a high percentage of fraud attack, defined as a risk score higher than 900.

### Rule Decision

Risk decision section shows metrics from the automated decision rules. The rules are defined by the merchant to make automated decisions based on the business need such as policies, bot and fraud risk tolerance, etc. To learn more about rules, view rules documentation (link TBD) The following metrics are available:

- **Rule decision trend** – Rule decision trend chart shows percentage of Approved, Rejected and Challenged decisions by rules. 
- **Top rules** – Top rules shows a list of rules with highest volume of automated decisions.

## Related topics:
- Account protection
- Account protection API
- Rules
- Bot detection
