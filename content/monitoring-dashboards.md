---
author: zhangleoMS
description: This article provides information about monitoring dashboards in Dynamics 365 Fraud Protection.
ms.author: zhangleo
ms.date: 10/12/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Monitoring
ms.custom: bap-template
---
# Monitoring
Monitoring of Dynamics 365 Fraud Protection provides a set of metrics that refresh close to real-time. These monitors assist fraud professionals in detecting unusual transaction patterns or anomalies in observation events, such as fraud attacks and faulty rule releases.

The metrics in these monitors are measured by the count of received transactions or observation events. The time stamp on the monitors shows the time when the monitor was last updated, in Coordinated Universal Time (UTC). You can switch between percentage view and absolute volume view of the distribution metrics by toggling the "Show absolute volume" button. Since the charts are updated near real-time, the last bar is lightly colored to signify that the metrics for the most recent minute's transactions or percentage are being aggregated and not finalized yet.

In a multi-hierarchy environment, where a parent environment has child environments, the near real-time monitors aggregate transactions and observation events for both the parent environment and all its children environments. 

The time-series metrics can be viewed in different timescales: 
- **Last 1 hour** - Shows transactions or observation events based on their received time per minute for the last 1 hour.
- **Last 48 hours** - Shows transactions or status events based on their received time per 15 minutes for the last 48 hours.
- **Last 8 days** - Shows transactions or status events based on their received time per hour for the last 8 days.

## Transaction monitor
The monitor shows volume and distribution metrics of assessment events such as Account Creation, Account Login, Purchase, and other assessment requests. On a selected timescale: 
### Key performance indicators
- **Transaction volume** – The transaction volume by count assessed by Dynamics 365 Fraud Protection.
- **Rule approved rate** – The percentage of assessed transactions by count that was approved.
- **Rule rejected rate** – The percentage of assessed transactions by count that was rejected.
- **Manual review rate** – The percentage of assessed transactions by count that was manually reviewed.
- **Rule challenged rate** – The percentage of assessed transactions by count that was challenged.
### Time series charts
- **Transaction volume** – The transaction volume by count assessed by Dynamics 365 Fraud Protection.
- **Risk score distribution** – The distribution of pre-defined risk score buckets.
- **Rule decision distribution** - The rule decision percentage.
- **Decision rule/clause distribution** - The distribution of the decision rule/clauses. It only shows the top 20 decision rule/clauses. The rest are grouped into “others”.
- **Device country/region code distribution** – The distribution of device country/region codes. It is available only when device fingerprinting from Dynamics 365 Fraud Protection is enabled. It only shows the top 20 device country/region codes. The rest are grouped into “others”.
- **Bot score distribution** - The distribution of pre-defined bot score buckets. It is only available for Account Creation, Account Login and Device Fingerprinting.

## Observation events monitor
The monitor shows volume and distribution metrics of observation events such as status, bank event, chargeback and label by received date. On a selected timescale:

### Observation event volume
- **Status volume** – The status event volume received. Status includes purchase status, account create status, account login status, and assessment status. 
- **Bank event volume** – The bank event volume received.
- **Chargeback volume** – The chargeback event volume received.
- **Label volume** – The label event volume received.

### Time series charts
- **Status events** by received date:
  - **Volume chart** – The status event volume received shown in time series.
  - **Distribution chart** – The status distribution of status events received shown in time series.
- **Bank events** by received date:
  - **Volume chart** - The bank event volume received shown in time series.
  - **Distribution chart** - The status distribution of bank events received shown in time series.
- **Chargeback events** by received date:
  - **Volume chart** - The chargeback event volume received shown in time series.
  - **Distribution chart** - The status distribution of chargeback events received shown in time series.
- **Label events** by received date:
  - **Volume chart** - The label event volume received shown in time series.
  - **Distribution chart** - The status distribution of label events received shown in time series.

