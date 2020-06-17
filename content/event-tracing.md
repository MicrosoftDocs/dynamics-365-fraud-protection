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

The *event tracing* functionality in the Microsoft Dynamics 365 Fraud Protection portal lets you establish a real-time telemetry platform that is extensible and operational outside the portal. Each event is either scheduled or triggered by a user-level or system-level action. You can subscribe to events that you're interested in and forward the event payloads to Azure Event Hubs. You can also request events from multiple event tracing sessions at the same time. The system will then deliver the events to Event Hubs in chronological order.

Events can be aggregated and used to define metrics that that you can use to monitor and manage your service costs and utilization. Events can also be used to maintain system logs for actions that are taken in the Fraud Protection portal (for example, *user A* edited *list B* on *date C*) or to develop custom reports that use transactional data. When you use the Event Hubs connectors that are available in Power Automate and Logic Apps, you can also use the data that you send to Event Hubs for alerting or highly customized workflows.

## Getting started

Follow these steps to start to use the event tracing functionality.

1. In the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Configuration**, and then select **Event Tracing**.
1. Select **New subscription**.
1. Provide the connection string for the instance of Event Hubs, and select an event to forward to that instance. For more information, see [Get an Event Hubs connection string](https://docs.microsoft.com/azure/event-hubs/event-hubs-get-connection-string).

    Before you save the page, you will see a description of the event and a sample of the schema/payload that is included.

1. Events are instantaneously sent to your Event Hubs instance. Go back to the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal to view the count for the **Events/Second** metric and make sure that data is being sent to Event Hubs.

    The **Events/Second** and **Failures/Second** metrics show an average over the past 24 hours.

    > [!TIP]
    > For additional monitoring, go to the Azure portal, and set up metrics. For more information, see [Azure Event Hubs metrics in Azure Monitor](https://docs.microsoft.com/azure/event-hubs/event-hubs-metrics-azure-monitor).

1. Optional: Set up your own ingress pipeline from Event Hubs to Power BI. For information about how to start to develop custom reports, see [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-power-bi-dashboard).
1. Optional: Connect to Event Hubs from Power Automate to define custom workflows. For more information, see [Event Hubs](https://docs.microsoft.com/connectors/eventhubs/).

## Event schemas

Two supported classifications of events are currently available in event tracing: *audit events* and *monitoring events*. Each event has a standardized schema that includes both fields that are included in every event (for example, **namespace**, **event version,** **tenantId**, and **timestamp**) and fields that are unique to the event classification.

### Audit events

You use audit events to track portal actions and develop an audit log. Audit events currently support EditList/EditRule, NewList/NewRule, and DeleteList/DeleteRule operations.

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

You use metrics for metering and monitoring reporting outside the Fraud Protection portal. Request counts and latency distribution events are sent every 20 seconds. These events include **startTime** and **endTime** fields that determine the aggregation period, and dimension names and values that can be used to filter the metrics as required.

#### Namespace: FraudProtection.Monitoring

##### [Requests sample payload]

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

##### [Latency sample payload]

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
```
