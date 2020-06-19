---
author: yvonnedeq
description: This topic explains the scorecard capability of the account protection feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/01/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin


title: Learn from the account protection scorecard
---

# Learn from the account protection scorecard

Microsoft Dynamics 365 Fraud Protection includes an account protection feature to help protect your e-commerce business from fraud that is related to fake accounts and account compromise. Your account protection scorecard shows you, in real time, how account protection is working. For example, the scorecard shows how many events are high-risk events. You can use the scorecard to make well-informed risk management decisions for your online business.

## Account protection assessment type

You can select the type of account protection assessment by using the **Tab** menu at the top of the page. The following types are available:

- Account Creation
- Account Login

## Customize your view

You can use the drop-down menus to filter your view of the interactive charts. The following option is available:

- **Event time** – Show event data by time. You can select whether to view events from the last hour or the last 24 hours.

## Key performance indicator charts

The scorecard shows metrics (key performance indicators \[KPIs\]) in the following sections.

### Bot model score

The bot model score provides insight into how bots are engaging your e-commerce platform. This score is a number between 0 and 999 that indicates the probability that a bot, not a person, is trying to create a new account or sign into an account. The higher the score, the higher the probability that a bot is initiating the event. You can analyze the following elements:

- **Bot score distribution** – The **Bot score distribution** chart shows the event volume, aggregated by bot model score.
- **Top bot countries and regions** – The **Top bot countries and regions** chart shows a geographic view of the five countries and regions that initiate the most bot encounters. That figure is defined as the percentage of total events that are initiated from a specific country or region, and that have a bot score that is above 900.

### Risk model score

The risk model score indicates the likelihood that an event is fraudulent. This score is a number between 0 and 999. The lower the score, the lower the probability of fraud. You can analyze the following elements:

- **Risk score distribution** – The **Risk score distribution** chart shows the event volume, aggregated by risk model score.
- **Top risk countries and regions** – The **Top risk countries and regions** chart shows a geographic view of the five countries and regions that have the highest bot encounter rates. This figure is defined as events that have a risk score that is above 900.

### Rule decision

The **Risk decision** section shows metrics from the automated decision rules that you've created. You can define rules to automate decisions about whether an event should be accepted or rejected, based on your business needs. The following metrics are available:

- **Rule decision trend** – The **Rule decision trend** chart shows the percentage of decisions that have been approved, rejected, challenged, and reviewed by rules.
- **Top rules** – The **Top rules** list shows the rules that triggered the highest volume of automated decisions.

For more information about rules, see the [rules documentation](rules.md).

## Custom assessment scorecard
The scorecard shows metrics (key performance indicators [KPIs]) in the **Risk decision** section.

- Select the **Scorecard** tab to view the scorecard for your custom assessment. 


### Rule decision

The **Risk decision** section shows metrics from the automated decision rules that you've created. You can define rules to automate decisions about whether an event should be accepted or rejected based on your business needs. The following metrics are available:

- **Rule decision trend** – The **Rule decision trend** chart shows the percentage of decisions that have been approved, rejected, challenged, and reviewed by rules.
- **Top rules** – The **Top rules** list shows the rules that triggered the highest volume of automated decisions.


## Related topics

- [Account protection overview](ap-overview.md)
- [View account protection schemas](new-ap-schema.md)
- [Custom assessment](custom-assessment.md)


