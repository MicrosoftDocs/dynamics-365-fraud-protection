---
author: josaw1
description: This article explains how to use event tracing in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/02/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: Event tracing

---

# Event tracing

The *event tracing* functionality in Microsoft Dynamics 365 Fraud Protection lets you establish a real-time telemetry platform that is extensible and operational outside the portal. Each event is scheduled or triggered by a user-level or system-level action. You can subscribe to events that you're interested in and forward the event payloads to Azure Event Hubs or Blob Storage. You can also request events from multiple event tracing sessions at the same time. The system will then deliver the events in chronological order.

Events can be aggregated and used to define metrics that you can use to monitor and manage your service costs and utilization. Events can also be used to develop custom reports that use transactional data or to maintain system logs for actions taken in the Fraud Protection portal. For example, *user A* edited *list B* on *date C*. When you use the Event Hubs connectors that are available in Power Automate and Logic Apps, you can also use the data that you send to Event Hubs for alerting or highly customized workflows. Similarly, with Blob Storage you can create a new subscription that will copy all historical data into your cold storage account for further analysis.

If your Fraud Protection instance has multiple environments, event tracing for each environment can be found by using the environment switcher. If the environment has child environments, event tracing that is subscribed to for the parent environment will automatically include the same events for all the child environments. 

> [!NOTE]
> Event tracting customers must have a subscription to additional Azure services such as Event Hub or Blob Storage. Contact your Microsoft Account Executive for details. If you have Azure global administrator credentials, log into the [Azure portal](https://ms.portal.azure.com/#home) to determine available subscriptions.

## Getting started

Follow these steps to start to use the event tracing functionality.

1. In the [Fraud Protection](https://dfp.microsoft.com/) portal, select **Data**, and then select **Event Tracing**.
  
1. Select **New subscription**.
   
1. Enter a subscription display name.
   
1. Select a storage location:
   
   1. **For Event Hubs**: Enter the connection string for the Event Hubs instance in Azure Key Vault. The Azure Key Vault should reside in the same tenant as your Fraud Protection subscription. Grant **Get Secret Access** to the Fraud Protection app to the Azure Key Vault. Enter the **Secret Identifier URL** from your Azure Key Vault in the Fraud Protection portal.  For more information, see [Get an Event Hubs connection string](/azure/event-hubs/event-hubs-get-connection-string).

   1. **For Blob Storage**: Enter the connection string for the Azure Blob Storage account in Azure Key Vault. The Azure Key Vault should reside in the same tenant as your Fraud Protection subscription. Grant **Get Secret Access** to the Fraud Protection app to the Azure Key Vault. In the Fraud Protection portal, enter the secret identifier URL from your Azure Key Vault and a container name where your event tracing data will reside. For more information, see [View account access keys](/azure/storage/common/storage-account-keys-manage?tabs=azure-portal#view-account-access-keys).

1.	Select **Test connection**. Once the connection is successfully tested, account-related information that was extracted from the connection string in the Azure Key Vault will be displayed. For Azure Event Hubs, this read-only information will include **Event Hub Namespace** and **Event Hub Name**. For Azure Blob Storage, **Storage account name** will be displayed. Verify that this information matches the storage account you intend to use. Without a successful connection test, the **Create** button will not be enabled.
    
1.	Select an event and review the description and sample of the JSON payload. Then save the subscription by selecting **Create**.
   
  Events are instantaneously sent to your Event Hubs instance from that point in time. If you selected Blob Storage, the copy process to write all historical data will begin and all events will be published to your container every 30 minutes.  
     
1.	Go back to the [Fraud Protection](https://dfp.microsoft.com/) portal to view the count for the **Events/Hr.** metric and make sure that data is being sent to Event Hubs and Blob Storage.

    The **Events/Hr** and **Failures/Hr** metrics show an average over the past 24 hours.

    > [!TIP]
    > For additional monitoring for Event Hubs, go to the Azure portal, and set up metrics. For more information, see [Azure Event Hubs metrics in Azure Monitor](/azure/event-hubs/event-hubs-metrics-azure-monitor).

1. Optional: Set up your own ingress pipeline from Event Hubs to Power BI. For information about how to start to develop custom reports, see [Work with Power BI](./extensibility-with-power-bi.md).

1. Optional: Connect to Event Hubs from Power Automate to define custom workflows. For more information, see [Work with Logic Apps or Power Automate](./extensibility-with-power-automate.md).

## Event schemas

Five supported classifications of events are currently available in event tracing: *transactional events*, *trace events*, *assessment events*, *audit events*, and *monitoring events*.

### Transactional events
Use transactional events to create custom scorecards and automated workflows using the data available in your assessment and non-assessment API calls. Using blob storage, you can also copy the data from historical API calls to create a data warehouse for your business. The payload for this event includes the entire request and response for each API call.

##### Namespace: FraudProtection.Observe.\<API Name\> or FraudProtection.Assessment.\<API Name\>

```json
{
    "uniqueId": "unique event id and used to deduplicate events",
    "request": {
        //API request payload
    },
    "response": {
        //API response payload
    },
    "name": "FraudProtection.Observe.AccountLabel",
    "version": "1.0",
    "metadata": {
        "tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
        "timestamp": "2020-09-25T03:46:53.3716978Z"
    }
}
```

### Trace events

You use trace events to report and monitor the performance for all rules that include the Trace() return type. The payload for this event includes standardized fields such as the name of the rule that triggered the event, the event type that correlates to the assessment type for that rule, correlation ID, etc. You can then send custom attributes using key:value pairs in the Trace() return type to include variables from the sample payload, the risk score, and custom fields. For more information on how to use Trace() in your rules to trigger these events, see [Observation functions](fpl-lang-ref.md#observation-functions) in the Rules language guide.

##### Namespace: FraudProtection.Trace.Rule.

```json
{
    "name": "FraudProtection.Trace.Rule",
    "version": "1.0",
    "metadata":
{
    "tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
    "timestamp": "2020-06-10T23:43:33.4526859Z" 
}
    "ruleName": "Risk Score Policy",
    "eventType": "Purchase",
    "correlationId": "e49319e6-0bea-4567-9f3e-c9f873fc958a",
    "eventId": "e75e703c-1e54-4d41-af4b-a4c1b8866f02",
    "attributes":
{
      "example": "ManualReview” //key:value pairs defined in the Trace() return type
} 

    }
```

### Assessment events

Assessment and associated label and observation events can be traced to event hubs and blobs.

##### Namespace: FraudProtection.Assessments.

```json
{
    "request": "",
    "response": "",
    "eventId": "uniqueId",
    "assessmentApiName": "<your assessment api name>",
    "assessmentName": "<your assessment name>"
}
```

##### Namespace: FraudProtection.Observations.

```json
{
    "request": "",
    "primaryEventId": "<assessment event id>",
    "observationApiName": "<your observation api name>",
    "observationName": "<your observation name>",
    "observationEventId": "<your observation event id>",
    "assessmentApiName": "<your assessment api name>",
    "assessmentName": "<your assessment name>"
}
```

##### Namespace: FraudProtection.Labels.

```json
{
    "request": "",
    "labelEventId": "",
    "assessmentApiName": "<your assessment api name>",
    "assessmentName": "<your assessment name>"
}
```

### Audit events

You use audit events to track portal actions and develop an audit log. Audit events currently support new/edit/delete operations on rules, lists, velocities, and external calls.

##### Namespace: FraudProtection.Audit.

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

### Audit log access

There are two ways that you can access audit logs. You can set up event tracing, or you can request an auto-generated audit log be sent by creating a Customer support ticket. If you decide not to use event tracing and instead submit a support ticket, the support ticket is routed to the Fraud Protection engineering team. The team extracts the logs and provides them back to you. Audit logs are captured and stored in the same geo that you have chosen to provision an environment. The logs can't be edited after they are captured and the log retention period is 365 days. Logs older than 365 days are automatically deleted.

There are five events generated that can be tracked by using the audit logs. Those events are:

- A user is assigned to a Fraud Protection role for the first time.
- An existing user's role is updated.
- All role assignments are removed for a specific user.
- A user accepts the FCRA consent.
- A user updates the Transaction acceptance booster (TAB) settings. Any change to these settings is considered an update.

### Activity logs events

You use activity logs events to eventsd to get detailed record of who did what, when, and where for some actions in DFP, such as who made the last change to a rule matching Activity logs content.

##### Namespace: FraudProtection.ActivityLog.

```json
"eventId": "6d28c8d2-d120-4a09-bb68-e36d88357dbb",
"operationType": "Create",
"resourceType": "Decision rule",
"resourceId": "a50bd4e9-cc41-4fdc-8b63-169399c73109",
"resourceName": "Rule Test",
"userId": "9234e81d-f5f2-4385-8172-56b37d63bb8d",
[Followed by operation type specific fields]
}
```
### Monitoring events

You can use monitoring events for custom reporting and alerting on your API and external calls performance in conjunction with the reporting available in the Fraud Protection portal. Each of the events below will provide insight into the latency and errors for each service.

##### Namespace: FraudProtection.Monitoring.RequestLatencyMsDistribution.

For API calls, request counts and latency distributions (in ms) are sent every 20 seconds in this event. These events include startTime and endTime fields that determine the aggregation period and dimension names and values that can be used to filter the metrics as required.

```json

{
"Index": [
             1
],
"BucketSamples": [
             2
],
"NumberOfBuckets": 10000,
"BucketSize": 10,
"MinimumValue": 0,
"CounterName": "RequestLatencyMsDistribution",
"DimensionNames": [
   "EnvironmentId",
   "TenantId",
   "ApiName",
   "ExperienceType",
   "IsTestRequest",
   "RequestType",
   "HttpRequestStatus",
   "HttpStatusCode"
],
"DimensionValues": [
   "63f55d63-9653-4ed9-be77-294da21202ae",
   "63f55d63-9653-4ed9-be77-294da21202ae",
   "v1.0/Observe/Create",
   "N/A",
   "False",
   "REALTIME",
   "Success",
   "200"
],
"StartTime": "2020-06-22T23:43:20",
"EndTime": "2020-06-22T23:43:40",
"Samples": 2,
"Min": 3,
"Max": 7,
"name": "FraudProtection.Monitoring.RequestLatencyMsDistribution",
"version": "1.0",
"metadata": {
   "tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
   "timestamp": "2020-06-22T23:43:20.0947542Z"
}
}

```

The *Samples* field represents the request count per API.

**Namespace: FraudProtection.Monitoring.ExternalCalls**

This event includes the latency (in ms) and HTTP status code of each external call \<link to external call doc\> which is triggered from a rule. Additional dimensions for the rule and clause triggering the call are also provided.

For external calls, latency (in ms) and http status code metrics are sent with each request in this event. Additional dimensions for the rule triggering the call are also provided to improve the troubleshooting experience if you were interested in investigating the performance of an individual call.

```json

{
    "name": "FraudProtection.Monitoring.ExternalCalls",
    "version": "1.0",
    "metadata": {
        "tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
        "timestamp": "2020-06-10T23:43:33.4526859Z"
    },
    "externalCallName": "SampleExternalCall",
    "requestStatus": "Success",
    "httpStatusCode": 200,
    "correlationId": "50BFA0D6-1E3D-4700-A2B3-1DD01162C08A",
    "latencyMs": 123,
    "assessment": "PURCHASE",
    "rule": "SampleRule",
    "clause": "SampleClause"
}

```

**Namespace: FraudProtection.Errors.ExternalCalls**

This event logs errors for each failed external call, and can be useful for debugging any issues you may see with your external call performance. The full request and response for the call will be logged, as well as the latency, and the rule and clause the call were triggered from.

```json

{
    "name": "FraudProtection.Errors.ExternalCalls",
    "version": "1.0",
    "metadata": {
        "tenantId": "63f55d63-9653-4ed9-be77-294da21202ae",
        "timestamp": "2020-06-10T23:43:33.4526859Z"
    },
    "externalCallName": "SampleExternalCall",
    "requestStatus": "ResponseFailure",
    "httpStatusCode": 404,
    "correlationId": "50BFA0D6-1E3D-4700-A2B3-1DD01162C08A",
    "latencyMs": 123,
    "assessment": "PURCHASE",
    "rule": "SampleRule",
    "clause": "SampleClause",
    "response": "{}",
    "requestUri": "https://samplewebsite/sample",
    "requestBody": "{}"
}

```



[!INCLUDE[footer-include](includes/footer-banner.md)]
