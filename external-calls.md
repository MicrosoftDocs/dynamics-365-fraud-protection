---
author: yvonnedeq
description: This topic explains how to use external calls to ingest data from APIs in Microsoft Dynamics 365 Fraud Protection.

ms.author: v-madeq
ms.service: fraud-protection
ms.date: 02/18/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: External calls

---

# External calls

## Overview

External calls enable you to ingest data from APIs outside of Microsoft Dynamics 365 Fraud Protection (Fraud Protection) and then use that data to make informed decisions in real-time. For example, using third-party addresses, phone verification services, or your own custom scoring models may provide important inputs to make a fully informed decision on an event. 

With external calls, you can connect to any API endpoint, make a request to that endpoint from within your rule, and use the response from that endpoint to make a decision. 

## Types of APIs you can use in an external call

Before you create an external call, there are a few restrictions you should know about:

-	Fraud Protection currently only supports the following authentication methods: Anonymous and Azure Active Directory 
-	Fraud Protection currently only supports the following HTTP methods: *GET* and *POST*. 

## Create an external call

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **External Calls**, and then select **New external call**. 

2. Review and complete the following fields:

   - **General** 
   
      **Name**: This is the name you use to reference your external call from your rules. The name can only contain numbers, letters, and underscores, and cannot begin with a number.

      > [!NOTE]
      > You cannot change the name of an external call after you use it in a rule. 

      **Description**: Add a description that makes it easy for your team to quickly identify the external call.

   - **Request**

      **Web Request**: Select the appropriate HTTP method (**GET** or **POST**), and then enter the API endpoint.
      **Authentication**: Choose how you want to authenticate incoming requests. 
   
      - If you select **Anonymous**, no authorization header will be sent. 
      - If you select **AAD**, an AAD token will be generated in your tenant, and *Bearer <token>* is used as the authorization header. 
      
         For more information about authentication, authorization, and AAD tokens, see [Understanding authentication and authorization]().
      
      **Application ID**: If you select AAD authentication, you must provide the application ID of an existing Azure Active Directory application within your Fraud Protection subscription tenant. For more information about creating and managing Azure AD applications, see [Create Azure Active Directory Applications]().

   - **Parameters**: 
   
     You can use parameters to pass data from Fraud Protection to your API endpoint. Depending on the the HTTP method you select, these parameters are sent to the endpoint either in the query string or as part of the request body. 
     
      - To add a new parameter, select **Add parameter**. 
      
     You can add sample values for each parameter. Fraud Protection will use these parameter values to make a sample call to your endpoint, either prior to creation or whenever you select **Test**.

      > [!NOTE]
      > All parameter values are interpreted as strings

   - **Sample Request**:
   
      This is an example of the request that will be sent to your external call. 
      For GET methods, the request URL is shown, and for POST methods, the request body is shown. This field reflects the parameter names and values you specified in the **Parameters field** and can’t be edited. 
      The sample request is used to make a sample call to your endpoint, prior to creation, or any time you select **Test**. 

   - **Response**:
   
      The **Sample response** is an example of the JSON data returned in a successful response from your API endpoint. Any data returned in the response can be referenced in your rules. The sample you provide here is shown as you create rules. 

   - **Timeout**:
   
      Specify how long in milliseconds the request should wait before timing out. You must specify a number between 1 and 1000. 

   - **Default Response**:

      Specify the default response that should be returned when your request fails or exceeds the specified timeout. This must be valid JSON object or JSON element. 

3. (Optional) To send a sample request to your API endpoint and view the response, select **Test**. For more information, see [Test your external call]().

4. When you’ve completed the required fields, select **Create**.

## Test an external call

To ensure that Fraud Protection can connect to your endpoint, test the connection at any point. 

1. To test a connection while creating a new external call or editing an existing one, once all required fields have been entered, select **Test**. 
Fraud Protection sends a request to your external call using the endpoint and parameters that you provided. 

   - If Fraud Protection successfully reaches the target endpoint, a green message bar displays at the top of the panel to inform you that the connection was successful. 

2.	To view the full response, select **See response details**.

   - If Fraud Protection is unable to reach the target endpoint, or if it does not receive a response before the specified timeout, a red message bar displays at the top of the panel showing the error that was encountered. 
   
   To view more information about the error, select **See error details**.

## Monitor external calls

### Monitor external calls in the Fraud Protection portal

Fraud Protection displays a tile containing three metrics for each external call you define: 

-	Requests per second: The total number of requests divided by the total number of minutes in the selected time frame.
-	Average latency: The total number of requests divided by the total number of minutes in the selected time frame.
-	Success rate: The total number of successful requests divided by the total number of requests made.

The numbers and charts shown on this tile includes only data for the timeframe you select in the timeframe dropdown in the upper right corner of the page. 

> [!NOTE]
> Metrics display only when your external call is used in an active rule. 

1. To dive deeper into the data about your external call, select Performance in the right corner of the tile. 

   Fraud Protection displays a new page with a more in-depth view of these metrics. 

2.	To view metrics for any timeframe in the last three months, adjust  the **Date range** at the top of the page. 

