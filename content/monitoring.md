---
author: josaw1
description: This article explains how to monitor API calls in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Monitor API calls
ms.collection: get-started
---

# Monitor API calls

[!include[deprecation](includes/deprecation.md)]

The API monitoring tools in Microsoft Dynamics 365 Fraud Protection provide data about the API calls you have made to the service. You can also consult the error logs to aid in identifying any issues. 

If your Fraud Protection instance has multiple environments, the API call information for each environment can be found by using the environment switcher on the top right of the menu bar. If the environment has child environments, the data in the API requests and on the **Errors** tab includes API calls for all the child environments. 

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

## Health ping to online URL

Fraud Protection provides a health ping endpoint which allows customers to verify connectivity from any client to the Web Service. The health ping endpoints is a basic check for latency and availability at the network layer.  

The endpoint returns zero bytes payload along with a 200 HTTP status code.

### Curl

```
curl https://contoso-guid.api.dfp.dynamics.com/api/v1/health 2>&1 | grep HTTP
> GET /api/v1/health HTTP/1.1
< HTTP/1.1 200 OK
```

### PowerShell

```
(Invoke-WebRequest https://contoso-guid.dfp.dynamics.com/api/v1/health).StatusCode
200
```

[!INCLUDE[footer-include](includes/footer-banner.md)]
