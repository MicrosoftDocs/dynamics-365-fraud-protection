---
author: yvonnedeq
description: How to use Event Hubs with Power BI to extend Fraud Protection functionality and incorporate Fraud Protection data into an organization’s processes and workflows.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 09/11/2020
ms.topic: conceptual
search.app:
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Working with Power BI

---
# Working with Power BI

Working with event data from Fraud Protection is customizable and easy using [Power BI](https://docs.microsoft.com/power-bi/). It allows you to produce informative and interactive data visualizations. 

### Getting started

To get Fraud Protection event data into Power BI, you can use either event data inside CDS or click **Stream Analytics** to send data from **Event Hubs** straight into **Power BI.**

For more information, refer to the following decision tree:
![decision tree](media/eventhubs/decision-tree.png)

To setup **CDS**, see [Storing event data in the CDS database](extensibility-with-power-automate.md#storing-event-data-in-the-common-data-service-cds-database-optional).

#### To setup Stream Analytics:
1. Go to the [Azure Portal](https://portal.azure.com/).
2. Enter `stream analytics` in the search box, and then click **Stream Analytics jobs** in the list of results.
3. Add a new job.
4. Create your new job with the name, subscription, resource group, etc., that you want.
5. Once the job has been deployed, click **Inputs**  in the left navigation, click **Add stream input** and then click **Event Hub**.
6. Name the **Input alias** whatever you’d like and setup the fields to point to the **Event Hub** from which you want to get data. 
You can select the **Use existing** radio button for most of these options. You can leave the rest of the options to their defaults. 
7. Click **Save** to create the **Input**.
8. Click **Outputs** in the left navigation, click **Add** and then click **Power BI**.
9. **Authorize** the connection.
10. Name the **Output alias** and select the **Group workspace** to which you want to add the **Power BI** data set. Create a new **Group workspace** at the [Power BI Portal](https://msit.powerbi.com/). 
11. Name the dataset and table. Click **Save** to create the **Output**.
12. Click **Query** in the left navigation and setup your query based on which fields of data from the events in your **Event Hub** you want in your **Power BI** dataset. This follows SQL syntax.
13. Select `FROM` the **Input** entity and `INTO` the **Output** entity you setup earlier. 
14. Click **Select time range** and load sample events that have gone through your **Event Hub**. Make sure the start time is far enough back that you can see some events loaded.
15. The following is a sample query for **Audit Events** that allows us to construct a table with the values we want:

```Javascript
SELECT
    audit.entityName,
    audit.entityType,
    audit.operationName,
    audit.userId
INTO
    [PBIAudit]
FROM
    [EHAudit]
```
 

   In this example, `PBIAudit` is the name of our **Output** and `EHAudit` is the name of our **Input** which we setup earlier in this example.
   
16. Check your Power BI workspace at [Power BI Portal](https://msit.powerbi.com/) to confirm that your dataset has been made and contains the information you intended to get.

### Creating Power BI reports

The following are useful resources for getting you up and running with producing your own Power BI reports:
- [Power BI beginner tutorial](https://www.youtube.com/watch?v=AGrl-H87pRU)
- [Official Power BI Docs](https://docs.microsoft.com/powerapps/maker/common-data-service/data-platform-powerbi-connector)
- [Building Power BI reports for the Common Data Service for Apps](https://powerapps.microsoft.com/blog/cds-for-apps-powerbi/)

### Sample Power BI reports

You can reference and build a sample of a Power BI dashboard based on Fraud Protection **Latency Event** data [here](https://github.com/microsoft/Dynamics-365-Fraud-Protection-Samples/tree/master/power%20bi%20sample).

## Related topics
- [Extensibility via Event Hubs - Overview]( extensibility-via-event-hubs-overview.md)
- [Setup extensibility via Event Hubs](extensibility-setup.md)	
- [Working with code](extensibility-with-code.md)
- [Working with Logic Apps/Power Automate]( extensibility-with-power-automate.md)
- [Working with Power Apps]( extensibility-with-power-apps.md)
- [Pricing](extensibility-pricing.md)
