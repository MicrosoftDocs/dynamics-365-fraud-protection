---
author: yvonnedeq
description: This topic explains how to monitor API calls in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.date: 10/23/2020
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Overview of API call monitoring tools
ms.custom: "intro-internal"
---


# Overview of API call monitoring tools

The monitoring tools in Microsoft Dynamics 365 Fraud Protection provide data about the API calls you have made to the service. You can also consult the error logs to aid in identifying any issues. 

## View the monitoring page

- In the left navigation, select **Data**, select **API management**, and then select the **API requests** or **Errors** tab. 

    Information on this page is updated in real time.

## API requests

The **API requests** tab shows an interactive chart of service metrics so you can evaluate performance over time.

- Use the drop-down menus and select date ranges to review API requests by time period, API name and type, and Fraud Protection experience. 
- Change your selections to refresh your charts and display only specified data.

The **Average requests/min** tiles provide a summary of API activity by type over time. The **Requests per minute** chart plots all activity in this timeframe for the API types you have chosen to view.

- Hover over points on the chart to see specific request totals by timestamp. 

## Errors

The Errors chart shows errors plotted out by date. 

- Select the **Errors** tab to review errors that may have occurred and to distinguish their types. 
- Choose a time period and API name to filter your view.
- Hover over points on the chart to see how many errors occurred at that time, their type, and their specific timestamp.

The full list of errors shows HTTP status descriptions and codes, the APIs to which they apply, the time and date when the errors occurred, and how many errors of that type occurred. 

- Filter results by selecting any of the column headers. 
- Select a line to find that error in the chart, and click it again to deselect. Results may take a few seconds to render. 


[!INCLUDE[footer-include](includes/footer-banner.md)]
