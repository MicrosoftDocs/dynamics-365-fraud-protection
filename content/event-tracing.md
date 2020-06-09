---
author: yvonnedeq
description: This topic explains how to use event tracing.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/09/2020

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
Events can be aggregated and used to define metrics to monitor and manage your service costs and utilization. They can also be used to maintain system logs on actions taken in the portal (i.e., *user A* edited *list B* on *date C*) or develop custom reports using transactional data. When you use the Event Hubs connectors available in Power Automate and Logic Apps, you can also use the data you send to Event Hubs for alerting or highly customized workflows.

## Getting started

Here are the steps to start consuming some of our available events:

1. In the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Configuration** and then select **Event Tracing**.

1. Select **New subscription**.

1. Fill out the form to provide the Event Hubs instance connection string and select an event to forward to that Event Hubs instance. For more information, see [Get an Event Hubs connection string](https://docs.microsoft.com/azure/event-hubs/event-hubs-get-connection-string).

    You will see a description of the event as well as a sample of the schema/payload that is included before you save the form.

1. After 24 hours, navigate back to the portal to view the Events/Second count and ensure that data is being sent to Event Hubs.

    1. The Events and Failures/Second metrics will display an average over the past 24 hours.
    1. For additional monitoring, navigate to the Azure Portal and set up metrics. For more information, see [Azure Event Hubs metrics in Azure Monitor](https://docs.microsoft.com/azure/event-hubs/event-hubs-metrics-azure-monitor).

1. (Optional) Set up your own ingress pipeline from Event Hubs to Power BI. For information on how to begin developing custom reports, see [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-power-bi-dashboard).

1. (Optional) Connect to Event Hubs from Power Automate to define custom workflows. For more information, see [Event Hubs](https://docs.microsoft.com/connectors/eventhubs/).

## Event schemas

There are currently three supported classifications of events available in event tracing. Each event has a standard Part A and Part B schema, where Part A is consistent for all events (including event version, namespace, etc.), and Part B is unique to each event category.

### Audit events

Use audit events to track portal actions and develop an audit log. Currently supporting: EditList/Rule, NewList/Rule, and DeleteList/Rule operations

#### Namespace: FraudProtection.Audit

#### Sample Payload

```json
{
"id": "ab40fbf1-d1a2-46b3-916c-0ed4a25c7067",
"namespace": "FraudProtection.Audit",
"description": "Rule and List Audit Events",
"schema": {
"version": "string",
"tenantId": "string",
"timestamp": "DateTime",
"userId": "string",
"entityType": "string",
"entityId": "string",
"operationName": "string"
},
"example": {
"version": "1.0",
"tenantId": "0a26b900-0a28-4ceb-ac38-de71b4775d6d",
"timestamp": "2020-06-09T02:42:02.8878236Z",
"userId": "userId",
"entityType": "List or Rule",
"entityId": "f73e52fa-2095-4857-a46e-a04dde1d78b3",
"operationName": "NewRule or EditRule or DeleteRule"
}
}
```

### Monitoring events

Use metrics for metering/monitoring reporting outside of the Fraud Protection portal. Request counts and latency distribution events are sent every 20 seconds and include **startTime** and **endTime** fields to determine the aggregation period and dimension names and values to filter these metrics as needed.

#### Namespace: FraudProtection.Monitoring

#### Requests Sample Payload

```json
{
version:
timestamp:
name: "FraudProtection.Monitoring"
counterName: "Request"
dimVals: ["Val1", "Val2", "Val3"]
dimNames: ["Dim1", "Dim2", "Dim3"]
startTime: "",
endTime: "",
samples: 2,
min: 1.0,
max: 1.0,
numeric
    {
        value: 1.0,
        }
}
```

#### Latency Sample Payload

```json
{
version:
timeStamp:
name: "FraudProtection.Monitoring”
counterName: "Latency"
dimVals: ["Val1", "Val2", "Val3"]
dimNames: ["Dim1", "Dim2", "Dim3"]
startTime: "",
endTime: "",
samples: 2,
min: 1.0,
max: 1.0,
distribution
    {
    "index": [1,2,3,4]
    "samples": [100, 200, 300, 400]
    "numberOfBuckets": 10000,
    "minimumValue": 0,
    "bucketSize": 10,
}
}
```

### Transactional events

Use transactional events to create conditions in power automate and logic apps as well as custom scorecards. Each payload contains a **subset** of every existing API request and response.

#### Namespace: FraudProtection.PurchaseProtection.\<APINAME\>.Evaluation *or* FraudProtection.AccountProtection.\<APINAME\>.Evaluation

#### Sample Payload

```json
{
version:
apiversion:
request
        {
        //unique per API-preview a sample in the portal
        }
response
        {
        //unique per API-preview a sample in the portal
        }
}
```
