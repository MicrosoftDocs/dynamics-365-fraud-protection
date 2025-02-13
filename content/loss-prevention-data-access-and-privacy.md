---
author: josaw1
description: This article explains how Microsoft Dynamics 365 Fraud Protection identifies anomalies and patterns to help store managers investigate in-store fraud.
ms.author: josaw
ms.date: 04/10/2024

ms.topic: conceptual
search.audienceType:
  - admin
title: Data access and privacy for loss prevention
---

# Data access and privacy for loss prevention

[!include[deprecation](includes/deprecation.md)]

The loss prevention feature in Microsoft Dynamics 365 Fraud Protection identifies anomalies and patterns to help store managers investigate in-store fraud. It uses adaptive artificial intelligence (AI) models to analyze historical data and identify patterns of anomalies. The reports that are generated from this analysis provide trend analysis, based on the return rate, the discount rate, and other key performance indicators (KPIs). Store managers can use these reports to focus on anomalies that, according to the risk scores that the adaptive AI models generate, might be associated with fraud.

> [!IMPORTANT]
> Before you turn on loss prevention for your organization, consult your Legal and Human Resources teams.

## What data does loss prevention process?

Loss prevention analyzes the historical data from transactions, sales, and payments from a point of sale (POS) system. This historical data is processed through the adaptive AI models and used to generate reports that show trends and anomalies. These reports provide actionable insights about the anomalies that the adaptive AI models detect, based on the historical events that have occurred in a retail store.

## How does loss prevention process data?

Loss prevention uses machine learning techniques to analyze the historical data that was mentioned earlier and generate insights. Loss prevention connects to the retail POS system to link the transactions, sales, and payments data feeds to the AI models. After outliers are detected, the adaptive AI models assign scores to rank them, based on their deviation from the average value in the overall data that was analyzed. A higher score indicates a higher probability that a meaningful anomaly is present. A store manager can consult these scores as part of an investigation. The reports provide an aggregated view of the anomalies.

## Who can view the loss prevention insights?

The outliers that the adaptive AI models referenced are presented as insights through interactive reports. Store managers can use these reports as part of an investigation of potential in-store fraud.


[!INCLUDE[footer-include](includes/footer-banner.md)]
