---
author: yvonnedeq
description: This topic explains how to use event tracing.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/12/2020

ms.topic: conceptual
search.app:
  - FraudProtection
search.audienceType:
  - admin
title: Event tracing

---
# Event tracing

## Overview

*Event tracing* is a functionality in the Microsoft Dynamics 365 Fraud Protection portal that provides the ability to establish a real-time telemetry platform that is extensible and operational outside of the Fraud Protection portal. Each event is either scheduled or triggered by a user/system-level action. You will be able to subscribe to events of interest and forward the event payloads to Azure Event Hubs. You can also request events from multiple event tracing sessions simultaneously; the system will deliver the events to Event Hubs in chronological order.

Events can be aggregated and used to define metrics to monitor and manage your service costs and utilization. They can also be used to maintain system logs on actions taken in the portal (i.e., *user A* edited *list B* on *date C*) or develop custom reports using transactional data. When you use the Event Hubs connectors available in Power Automate and Logic Apps, you can also use the data you send to Event Hubs for alerting or highly customized workflows.

## Getting started

Here are the steps to start utilizing the event tracing functionality:

1. In the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Configuration** and then select **Event Tracing**.

1. Select **New subscription**.

1. Fill out the form to provide the Event Hubs instance connection string and select an event to forward to that Event Hubs instance. For more information, see [Get an Event Hubs connection string](https://docs.microsoft.com/azure/event-hubs/event-hubs-get-connection-string).

    You will see a description of the event as well as a sample of the schema/payload that is included before you save the form.

1. Events will then instantaneously be sent to your Event Hubs instance.

  Navigate back to the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal to view the Events/Second count and ensure that data is being sent to Event Hubs.

    1. The Events and Failures/Second metrics will display an average over the past 24 hours.
    1. For additional monitoring, navigate to the Azure Portal and set up metrics. For more information, see [Azure Event Hubs metrics in Azure Monitor](https://docs.microsoft.com/azure/event-hubs/event-hubs-metrics-azure-monitor).

1. (Optional) Set up your own ingress pipeline from Event Hubs to Microsoft Power BI. For information on how to begin developing custom reports, see [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-power-bi-dashboard).

1. (Optional) Connect to Event Hubs from Power Automate to define custom workflows. For more information, see [Event Hubs](https://docs.microsoft.com/connectors/eventhubs/).

## Event schemas

There are currently two supported classifications of events available in event tracing: *audit events* and *monitoring events*. Each event has a standardized schema with fields included in every event (namespace, event version, tenantId, and timestamp) as well as fields unique to each event classification.

### Audit events

Use audit events to track portal actions and develop an audit log. Currently supporting: EditList/Rule, NewList/Rule, and DeleteList/Rule operations.

#### Namespace: FraudProtection.Audit

```json
"audit": {
"entityId": "cde1518f-305e-42e8-8d05-9b955efe3f46",
"entityName": "Manual Review Rule",
"entityType": "Rule",
"operationName": "NewRule",
"userId": "user@contoso.com"
},
"name": "FraudProtection.Audit",
"version": "1.0",
"metadata": {
"tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
"timestamp": "2020-06-10T23:43:33.4526859Z"
}
```

### Monitoring events

Use metrics for metering/monitoring reporting outside of the Fraud Protection portal. Request counts and latency distribution events are sent every 20 seconds and include startTime and endTime fields to determine the aggregation period and dimension names and values to filter these metrics as needed.

#### Namespace: FraudProtection.Monitoring

#### [Requests sample payload]

```json
"name": "FraudProtection.Monitoring",
"version": "1.0",
"Metadata": {
"tenantId": "b271840c-c33d-4ba5-8d19-3db39dc8ab98",
"timestamp": "2020-05-08T00:22:00.000000Z"
},
"counterName": "Requests",
"dimensionValues": [
"Val1",
"Val2",
"Val3"
],
"dimensionNames": [
"Dim1",
"Dim2",
"Dim3"
],
"startTime": "2020-05-08T00:22:00.000000Z",
"endTime": "2020-05-08T00:22:20.000000Z",
"samples": 2,
"min": 1.0,
"max": 1.0,
"Numeric": {
 "value": 1.0
}
```

#### [Latency sample payload]

```json
"name": "FraudProtection.Monitoring",
"version": "1.0",
"Metadata": {
"tenantId": "b271840c-c33d-4ba5-8d19-3db39dc8ab98",
"timestamp": "2020-05-08T00:22:00.000000Z"
},

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

