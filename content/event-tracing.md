---
author: yvonnedeq
description: This topic explains how to use event tracing.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/08/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Event tracing 

---
# Event tracing

## Overview

*Event tracing* gives you the ability to establish a real-time telemetry platform that will be extensible and operational outside the portal. You can subscribe to events for monitoring, metering, auditing, and transactional data and then send these events to Azure Event Hubs. You can also request events from multiple event tracing sessions simultaneously and the system delivers these events to Event Hubs in chronological order.
Events can be aggregated and used to define metrics to monitor and manage your service costs and utilization. They can also be used to maintain system logs on actions taken in the portal (i.e., *user A* edited *list B* on *date C*) or develop custom reports using transactional data. When you use the Event Hubs connectors available in power automate and logic apps, you can also use the data you send to Event Hubs for alerting or highly customized workflows.

## Getting started
Here are the steps to start consuming some of our available events:

1.	In the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Configuration** and then select **Event Tracing**.

1.	Select **New subscription**.

1.	Fill out the form to provide the Event Hubs instance connection string and select an event to forward to that Event Hubs instance. For more information, see [Get an Event Hubs connection string](https://docs.microsoft.com/azure/event-hubs/event-hubs-get-connection-string).  

    - When you see a description of the event and a sample of the schema/payload that is included, select **Save**. 

1.	After one minute, check the portal to view the **Events/Min count** to ensure that data is being sent to Event Hubs. 

    - For additional monitoring, navigate to the Azure Portal and set up **Metrics**. For more information, see [Azure Event Hubs metrics in Azure Monitor](https://docs.microsoft.com/azure/event-hubs/event-hubs-metrics-azure-monitor).
    
1.	(Optional) Set up your own ingress pipeline from Event Hubs to Power BI. For information on how to begin developing custom reports, see [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-power-bi-dashboard).

1.	(Optional) Connect to Event Hubs from power automate to define custom workflows. For more information, see [Event Hubs](https://docs.microsoft.com/connectors/eventhubs/).

## Event schemas

There are currently four supported classifications of events available in Event Tracing. Each event includes the event version (ver: ) as well as the API version (apiver: ), if applicable.

### Audit events

Use audit events to track portal actions and develop an audit log.

| Event Namespace| Payload    |
|---------|-------------|
|Lists.All.Audit          |<p>```json</p><p>{</p><p>  ver: </p><p>  userID: </p><p>   tenantID: </p><p>  timestamp: </p><p>  eventname: NewList, EditList, DeleteList</p><p>   listname: </p><p>}</p>             |
|PurchaseProtection.All.Audit          |<p>```json</p><p>{</p><p>  ver: </p><p>  userID: </p><p>   tenantID: </p><p>  timestamp: </p><p>  eventRule: NewRule, EditRule, DeleteRule</p><p>   Rulename: </p><p>}</p>             |
|AccountCreation.All.Audit          |<p>```json</p><p>{</p><p>  ver: </p><p>  userID: </p><p>   tenantID: </p><p>  timestamp: </p><p>  eventname: NewRule, EditRule, DeleteRule</p><p>   Rulename: </p><p>}</p>             |
|AccountLogin.All.Audit          |<p>```json</p><p>{</p><p>  ver: </p><p>  userID: </p><p>   tenantID: </p><p>  timestamp: </p><p>  NewRule, EditRule, DeleteRule</p><p>   Rulename: </p><p>}</p>             |
|UserAccess.PermissionsUpdate.Audit          |<p>```json</p><p>{</p><p>  ver: </p><p>  userID: </p><p>   tenantID: </p><p>  timestamp: </p><p>  eventname: PermissionsUpdate</p><p>   updateduser: </p>><p>   updatedperm: </p><p>}</p>            |



### Metering/monitoring events

Use metering/monitoring events for metering/monitoring reporting outside of the DFP portal. 

| Event Namespace| Payload    |
|---------|-------------|
|<p>PurchaseProtection.<**API NAME**>.Monitoring</p><p>AccountProtection.<**API NAME**>.Monitoring</p><p>PurchaseProtection.<**API NAME**>.Metering</p><p>AccountProtection.<**API NAME**>.Metering</p><p>API NAME: Purchase, PurchaseStatus, BankEvent, Chargeback, Refund, UpdateAccount, Label, SignUp, SignUpStatus, Label, etc.</p>        |<p>```json</p><p>{  </p><p>  name: "Sparta.Metric"</p><p>  ver: "1.0",</p><p>  TenantInfo:</p><p>  {</p><p>    environmentId:</p><p>    namespace: </p><p>    severity: "" </p><p>  }</p><p>PartB:  </p><p>{  </p><p>  name: "Monitoring"</p><p>  counterName: "Monitoring"</p><p>  dimVals: ["Val1", "Val2", "Val3"]</p><p>  dimNames: ["Dim1", "Dim2", "Dim3"]</p><p>  startTime: "",</p><p>  endTime: "",</p><p>  samples: 2,</p><p>  min: 1.0,</p><p>  max: 1.0,</p><p>  numeric</p><p>  {</p><p>    value: 1.0,</p><p>  }</p><p>}  </p><p>  PartC:</p><p>  {</p><p>  ["Key": "Value"]</p><p>  }</p><p>}  </p>             |


### Transactional events

Use transactional events to create conditions in power automate as well as custom scorecards. Each payload will contain a subset of every existing API request and response.

| Event Namespace| Payload    |
|---------|-------------|
|<p>PurchaseProtection.<**API NAME**>.Evaluation</p> <p>AccountProtection.<**API NAME**>.Evaluation</p>         |<p>```json</p><p>{</p><p>  ver: </p><p>  apiver: </p><p>  request:{ </p><p>  }</p><p>  response{</p><p>  }</p><p>}</p>             |
 
