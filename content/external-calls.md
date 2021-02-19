---
author: yvonnedeq
description: This topic explains how to use external calls to ingest data from APIs in Microsoft Dynamics 365 Fraud Protection.

ms.author: v-madeq
ms.service: fraud-protection
ms.date: 02/19/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: External calls

---

# External calls

## Overview

External calls enable you to ingest data from APIs outside of Microsoft Dynamics 365 Fraud Protection (Fraud Protection) and then use that data to make informed decisions in real-time. For example, third-party address and phone verification services, or your own custom scoring models, may provide critical input in determining the risk-level of an event. With external calls, you can connect to any API endpoint, make a request to that endpoint from within your rule, and use the response from that endpoint to make a decision. 

## Types of APIs you can use in an external call

Before you create an external call, there are a few restrictions you should know about:

-	Fraud Protection currently only supports the following authentication methods: *Anonymous* and *Azure Active Directory*. 
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
      
         For more information about authentication, authorization, and AAD tokens, see [Understanding authentication and authorization](external-calls.md#understanding-authentication-and-authorization).
      
      **Application ID**: If you select AAD authentication, you must provide the application ID of an existing Azure Active Directory application within your Fraud Protection subscription tenant. For more information about creating and managing Azure AD applications, see [Create Azure Active Directory Applications](https://docs.microsoft.com/dynamics365/fraud-protection/integrate-real-time-api#create-azure-active-directory-applications).

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

3. (Optional) To send a sample request to your API endpoint and view the response, select **Test**. For more information, see [Test an external call](external-calls.md#test-an-external-call).

4. When you’ve completed the required fields, select **Create**.

## Test an external call

To ensure that Fraud Protection can connect to your endpoint, test the connection at any point. 

1. To test a connection while creating a new external call or editing an existing one, once all required fields have been entered, select **Test**. 
Fraud Protection sends a request to your external call using the endpoint and parameters that you provided. 

   - If Fraud Protection successfully reaches the target endpoint, a green message bar displays at the top of the panel to inform you that the connection was successful. 

2. To view the full response, select **See response details**.

   - If Fraud Protection is unable to reach the target endpoint, or if it does not receive a response before the specified timeout, a red message bar displays at the top of the panel showing the error that was encountered. 
   
     To view more information about the error, select **See error details**.

## Monitor external calls

### Monitor external calls in the Fraud Protection portal

Fraud Protection displays a tile containing three metrics for each external call you define: 

-	**Requests per second**: The total number of requests divided by the total number of minutes in the selected time frame.
-	**Average latency**: The total number of requests divided by the total number of minutes in the selected time frame.
-	**Success rate**: The total number of successful requests divided by the total number of requests made.

The numbers and charts shown on this tile includes only data for the timeframe you select in the timeframe dropdown in the upper right corner of the page. 

> [!NOTE]
> Metrics display only when your external call is used in an active rule. 

1. To dive deeper into the data about your external call, select **Performance** in the right corner of the tile. 

   Fraud Protection displays a new page with a more in-depth view of these metrics. 

2. To view metrics for any timeframe in the last three months, adjust  the **Date range** at the top of the page. 

In addition to the three metrics described above, a fourth chart displays:

-	**Errors**: The number of errors by error type and code. 

You can view these error counts over time, or to view the distribution of errors, select **Pie chart**. 

In addition to HTTP Client Errors (400, 401, 403), you may also see the following errors:

-	**Invalid application id**: The application ID provided does not exist in your tenant or is invalid. 
-	**AAD failure**: Failed to retrieve Azure Active Directory token.
-	**Definition not found**: The external call has been deleted but is still referenced in a rule.
-	**Timeout**: Request to target took longer than the specified timeout. 
-	**Communication failure**: Unable to connect to target due to network issue or target is unavailable. 
-	**Circuit breaker**: If the external call has failed continuously, exceeding a certain threshold, all further calls will be suspended for a short interval. 
-	**Unknown Failure**: Dynamics 365 internal failure 

### Use event tracing to monitor external calls 

You can use Fraud Protection’s event tracing capability to forward events related to your external calls to your own Azure Event Hubs or Blob Storage. 

You can subscribe to the following two events related to external calls:

1.	FraudProtection.Monitoring.ExternalCalls
2.	FraudProtection.Errors.ExternalCalls

Whenever a request is made to an external call, an event is sent to the FraudProtection.Monitoring.ExternalCalls namespace. The event payload includes information on the latency of the call, the request status, and the rule and clause from which it was triggered. 

When an external call fails, an event is sent to the FraudProtection.Errors.ExternalCalls namespace. The event payload includes the URI request and body that were sent to the external call as well as the response that was received. 

For more information about event tracing, how to subscribe to events, and what you can do with events, see [Event tracing](event-tracing.md). 

For information on how to integrate this data with your own organization’s workflows, and set up custom monitoring, alerting and reporting, see [Extensibility via Event Hubs](https://docs.microsoft.com/dynamics365/fraud-protection/extensibility-via-event-hubs-overview).

## Manage external calls

1.	To edit an existing external call, select **Edit** on the card header. 

   > [!NOTE]
   > You can’t change the name and parameters of an external call after you use it in a rule.

2.	To delete an existing external call, select the ellipses, and then select **Delete**. 

   > [!NOTE]
   > You can’t delete an external call after it is referenced in a rule. 

3.	To view detailed performance metrics for an external call, select **Performance**. 

4.	To test that Fraud Protection is still able to connect to your external call, select the ellipses, and then select **Test Connection**. 

## Use an external call with rules

1.	To use your external calls to make decisions, reference them from your rules.
2.	To reference an external call named, **myCall**, in your rule, use the following syntax:

     External.myCall()

3.	Use the following syntax if **myCall** requires a parameter, for example *IPaddress*:

     External.myCall(@”device.ipAddress”)

For information about the rules language and how you can use external calls in rules, see the [Language guide for Fraud Protection rules](fpl-lang-ref.md). 

> [!NOTE]
> Using external calls in your rule may increase the latency of the rule. 

## Understanding authentication and authorization 

To ensure that data is accessed securely, APIs often  authenticate the sender of a request to verify that they have permission to access the data.External calls in Fraud Protection support two methods of authentication: *Anonymous* and *AAD*.

If you select **Anonymous**, the **Authorization** header in the HTTP request to the target endpoint will be left blank. Use this option when the target endpoint does not require an **Authorization** header. For example, if your endpoint uses an API key, configure the key-value pair as part of the request URL you enter in the **Web Request** field. The target endpoint can then validate if the API key from the request URL is allowed, and then decide if permission should be granted.

If you select AAD, the **Authorization** header in the the HTTP request to the target endpoint will include a Bearer token. A Bearer token is a JSON Web Token (JWT) issued by Azure Active Directory. For information about JWTs, see Microsoft identity platform access tokens. Fraud Protection appends the token value to the text Bearer in the required format to the request Authorization header as follows:

    Bearer <token>

### Token claims
The following table lists the claims that you can expect in Bearer tokens issued by Fraud Protection. 

| Name                            | Claim              | Description |
|---------------------------------|--------------------|-------------|
| Tenant ID                       | tid                | Identifies the Azure tenant ID of the subscription associated with your Fraud Protection account. To find your tenant ID in the Fraud Protection Portal, select the **Configuration** tab on the **API Management** page and view **Directory ID**. To find your tenant ID in the Azure Portal, see [How to find your Azure Active Directory tenant ID](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).         |
| Audience                        | aud                | Identifies the intended recipient of the token. This value will reflect exactly the application ID provided when you configure your external call on the Fraud Protection portal.                                                   |
| Application ID                  | appid              | This is Fraud Protection’s application id: bf04bdab-e06f-44f3-9821-d3af64fc93a9. This ID is owned solely by Fraud Protection, and only we can request a token on behalf of it.                                                        |
      
When your API receives a token, it should open the token, and validate the each of the above claims match their description. 
Here is an example of how you can authenticate an incoming request using the [JwtSecurityTokenHandler](https://docs.microsoft.com/dotnet/api/system.identitymodel.tokens.jwt.jwtsecuritytokenhandler?view=azure-dotnet).


```json

string authHeader = "Bearer <token>"; // the Authorization header value
var jwt = new JwtSecurityTokenHandler().ReadJwtToken(token);
string tid = jwt.Claims.Where(c => c.Type == "tid").FirstOrDefault()?.Value;
string aud = jwt.Claims.Where(c => c.Type == "aud").FirstOrDefault()?.Value;
string appid = jwt.Claims.Where(c => c.Type == "appid").FirstOrDefault()?.Value;
if(tid != "<my tenant id>" || aud != "<my application id>" || appid != "bf04bdab-e06f-44f3-9821-d3af64fc93a9")
{
throw new Exception("the token is not authorized.");
}

```



