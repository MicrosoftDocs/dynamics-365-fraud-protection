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
Events can be aggregated and used to define metrics to monitor and manage your service costs and utilization. They can also be used to maintain system logs on actions taken in the portal (i.e., *user A* edited *list B* on *date C*) or develop custom reports using transactional data. When you use the Event Hubs connectors available in power automate and logic apps, you can also use the data you send to Event Hubs for alerting or highly customized workflows.

## Getting started
Here are the steps to start consuming some of our available events:

1.	In the [Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Configuration** and then select **Event Tracing**.

1.	Select **New subscription**.

1.	Fill out the form to provide the Event Hubs instance connection string and select an event to forward to that Event Hubs instance. For more information, see [Get an Event Hubs connection string](https://docs.microsoft.com/azure/event-hubs/event-hubs-get-connection-string).  

    You will see a description of the event as well as a sample of the schema/payload that is included before you save the form. 

1. After 24 hours, navigate back to the portal to view the **Events/Min count** and ensure that data is being sent to Event Hubs. 

    1. The **Events and Failures/Second metrics** will display an average over the past 24 hours.
    1. For additional monitoring, navigate to the Azure Portal and set up **Metrics**. For more information, see [Azure Event Hubs metrics in Azure Monitor](https://docs.microsoft.com/azure/event-hubs/event-hubs-metrics-azure-monitor).
    
1.	(Optional) Set up your own ingress pipeline from Event Hubs to Power BI. For information on how to begin developing custom reports, see [Stream Analytics and Power BI: A real-time analytics dashboard for streaming data](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-power-bi-dashboard).

1.	(Optional) Connect to Event Hubs from power automate to define custom workflows. For more information, see [Event Hubs](https://docs.microsoft.com/connectors/eventhubs/).

## Event schemas

There are currently four supported classifications of events available in Event Tracing. Each event includes the event version (ver: ) as well as the API version (apiver: ), if applicable.

### Audit events

Use audit events to track portal actions and develop an audit log.

#### Namespace: FraudProtection.Audit
#### Sample Payload:

'''json
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
'''




### Metering/monitoring events

Use metering/monitoring events for metering/monitoring reporting outside of the DFP portal. 




### Transactional events

Use transactional events to create conditions in power automate as well as custom scorecards. Each payload will contain a subset of every existing API request and response.


