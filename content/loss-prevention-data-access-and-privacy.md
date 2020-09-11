---
author: yvonnedeq
description: This topic explains how Microsoft Dynamics 365 Fraud Protection identifies anomalies and patterns to assist store managers in investigating in-store fraud.
ms.author: v-madeq 
ms.service: fraud-protection
ms.date: 09/11/2020

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Data access and privacy for loss prevention
---

# Data access and privacy for loss prevention

The loss prevention feature in Microsoft Dynamics 365 Fraud Protection identifies anomalies and patterns that can assist store managers in investigating in-store fraud. The loss prevention feature uses adaptive artificial intelligence (AI) models to analyze historical data and identify patterns of anomalies. Reports are then generated from this analysis, providing trend analysis based on the return rate, the discount rate, and other key performance indicators (KPIs). Store managers can use the reports to focus on anomalies that, according to the risk scores that the adaptive AI models generate, might be associated with potential fraud. 

> [!IMPORTANT]  
> Consult with your legal and human resources teams before enabling loss prevention for your organization.

## What data does loss prevention process?

Loss prevention analyzes the historical data from transactions, sales, and payments from a POS system. The historical data is processed through the adaptive AI models and used to generate reports that show trends and anomalies. These reports provide actionable insights about the anomalies that the adaptive AI models detect, based on the historical events that have happened in a retail store.

##How does loss prevention process data?

Loss prevention uses machine learning techniques to analyze the historical data referenced above and generate insights. Loss prevention connects to the retail POS system to link the transactions, sales, and payments data feeds to the AI models. Once the outliers are detected, the adaptive AI models rank them by assigning scores based on the deviation of such outliers from the average value in the overall data analyzed. A higher score means that the adaptive AI models indicate a higher probability that a meaningful anomaly is present, which a store manager can consult as part of an investigation. The reports provide an aggregated view of these anomalies. 

## Who gets to see the loss prevention insights?

The outliers inferenced by the adaptive AI models are then presented as insights through interactive reports. These reports may be used by store managers as part of an investigation of potential in-store fraud. 
