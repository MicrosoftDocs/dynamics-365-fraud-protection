---
author: yvonnedeq
description: This topic explains how to use external calls to ingest data from APIs in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/01/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: External calls

---

# External calls

[!include [banner](includes/preview-banner.md)]

External calls let you ingest data from APIs outside Microsoft Dynamics 365 Fraud Protection and then use that data to make informed decisions in real time. For example, third-party address and phone verification services, or your own custom scoring models, might provide critical input that helps determine the risk level for some events. By using external calls, you can connect to any API endpoint, make a request to that endpoint from within your rule as required, and use the response from that endpoint to make a decision.

> [!NOTE]
> If this additional data will be needed for all events, you can also send it as part of the assessment schema. For more information about how to send custom data as part of an API request, see [Custom data sample](view-purchase-protection-schemas.md#custom-data-sample).

## Types of APIs that can be used in an external call

Before you create an external call, you should know about the following limitations:

- Fraud Protection currently supports only the following authentication methods: *Anonymous* and *AAD*.
- Fraud Protection currently supports only the following HTTP methods: *GET* and *POST*.

## Create an external call

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **External Calls**, and then select **New external call**.
2. Review and set the following fields as required:

    - **Name** – Enter the name that you will use to reference the external call from your rules. The name can contain only numbers, letters, and underscores. It can't begin with a number.

        > [!NOTE]
        > You can't change the name of an external call after you use it in a rule.

    - **Description** – Add a description to help your team quickly identify the external call.
    - **Web Request** – Select the appropriate HTTP method (**GET** or **POST**), and then enter the API endpoint.
    - **Authentication** – Select the method that should be used to authenticate incoming requests:

        - If you select **Anonymous**, an authorization header won't be sent.
        - If you select **AAD**, an Azure Active Directory (Azure AD) token will be generated in your tenant, and *Bearer \<token\>* will be used as the authorization header.

        For more information about authentication, authorization, and Azure AD tokens, see the [Understand authentication and authorization](external-calls.md#understand-authentication-and-authorization) section later in this topic.

    - **Application ID** – If you selected **AAD** as the authentication method, you must provide the application ID of an existing Azure AD application within your Fraud Protection subscription tenant. For more information about how to create and manage Azure AD applications, see [Create Azure Active Directory Applications](integrate-real-time-api.md#create-azure-active-directory-applications).
    - **Add parameter** – You can use parameters to pass data from Fraud Protection to your API endpoint. Depending on the HTTP method that you selected, these parameters will be sent to the endpoint either in the query string or as part of the request body.

        You can add sample values for each parameter. Fraud Protection will use these parameter values to make a sample call to your endpoint, either before creation or whenever you select **Test**.

        > [!NOTE]
        > All parameter values are interpreted as strings.

    - **Sample Request** – Provide an example of the request that is sent to your external call. The request should reflect the parameter names and values that you specified, and it can't be edited.

        For *GET* methods, the request URL is shown. For *POST* methods, the request body is shown.

        The sample request is used to make a sample call to your endpoint, either before creation or whenever you select **Test**.

    - **Sample Response** – Provide an example of the data data that is returned in a successful response from your API endpoint. This data should be in JavaScript Object Notation (JSON) format and  can be referenced in your rules. The sample that you provide here is shown as you create rules.

        Select **Test** to automatically enter a real response from your API in this field.

    - **Timeout** – Specify how long, in milliseconds, the request should wait before it times out. You must specify a number between 1 and 1000.
    - **Default Response** – Specify the default response that should be returned if your request fails or exceeds the specified time-out. The value must be valid JSON object or JSON element.

3. Optional: To send a sample request to your API endpoint and view the response, select **Test**. For more information, see the next section, [Test an external call](external-calls.md#test-an-external-call).
4. When you've finished setting the required fields, select **Create**.

## Test an external call

To ensure that Fraud Protection can connect to your endpoint, test the connection at any point.

- To test a connection while you're creating a new external call or editing an existing external call, set all the required fields, and then select **Test**.

    Fraud Protection  uses the endpoint and parameters that you provided to send a request to your external call.

    - If Fraud Protection successfully reaches the target endpoint, a green message bar appears at the top of the panel to inform you that the connection was successful. To view the full response, select **See response details**.
    - If Fraud Protection can't reach the target endpoint, or if it doesn't receive a response before the specified time-out, a red message bar appears at the top of the panel and shows the error that was encountered. To view more information about the error, select **See error details**.

## Monitor external calls

### Monitor external calls in the Fraud Protection portal

Fraud Protection shows a tile that contains three metrics for each external call that you define:

- **Requests per second** – The total number of requests divided by the total number of minutes in the selected time frame.
- **Average latency** – The total number of requests divided by the total number of minutes in the selected time frame.
- **Success rate** – The total number of successful requests divided by the total number of requests that have been made.

The numbers and charts that are shown on this tile include only data for the time frame that you select in the drop-down list in the upper-right corner of the page.

> [!NOTE]
> Metrics are shown only when your external call is used in an active rule.

1. To dive deeper into the data about your external call, select **Performance** in the right corner of the tile.

    Fraud Protection shows a new page that has a more detailed view of the metrics.

2. To view metrics for any time frame in the last three months, adjust the **Date range** setting at the top of the page.

In addition to the three metrics that were described earlier, an **Error** chart is shown. This chart shows the number of errors by error type and code. To view error counts over time, or to view the distribution of errors, select **Pie chart**.

In addition to HTTP client errors (400, 401, and 403), you might see the following errors:

- **Invalid application id** – The application ID that was provided doesn't exist in your tenant, or it isn't valid.
- **AAD failure** – The Azure AD token could not be retrieved.
- **Definition not found** – The external call has been deleted, but it's still referenced in a rule.
- **Timeout** – The request to the target took longer than the specified time-out.
- **Communication failure** – No connection could be made to the target because of a network issue or because the target is unavailable.
- **Circuit breaker** – If the external call has failed continuously and has exceeded a certain threshold, all further calls will be suspended for a short interval.
- **Unknown Failure** – An internal Dynamics 365 failure occurred.

### Use event tracing to monitor external calls

You can use Fraud Protection's event tracing capability to forward events that are related to your external calls to your own instances of Azure Event Hubs or Azure Blob Storage. In the Fraud Protection portal, on the **Event Tracing** page, you can subscribe to the following two events that are related to external calls:

- FraudProtection.Monitoring.ExternalCalls
- FraudProtection.Errors.ExternalCalls

Whenever a request is made to an external call, an event is sent to the FraudProtection.Monitoring.ExternalCalls namespace. The event payload includes information about the latency of the call, the request status, and the rule and clause from which the request was triggered.

When an external call fails, an event is sent to the FraudProtection.Errors.ExternalCalls namespace. The event payload includes the URI request and body that were sent to the external call, and the response that was received.

For more information about event tracing, how to subscribe to events, and what you can do with events, see [Event tracing](event-tracing.md).

For information about how to integrate this data with your own organization's workflows, and set up custom monitoring, alerting and reporting, see [Extensibility via Event Hubs](extensibility-via-event-hubs-overview.md).

## Manage external calls

- To edit an existing external call, select **Edit** on the card header.

    > [!NOTE]
    > You can't change the name and parameters of an external call after you use it in a rule.

- To delete an existing external call, select the ellipsis (**...**), and then select **Delete**.

    > [!NOTE]
    > You can't delete an external call after it's referenced in a rule.

- To view detailed performance metrics for an external call, select **Performance**.
- To test that Fraud Protection can still connect to your external call, select the ellipsis (**...**), and then select **Test Connection**.

## Use an external call in rules

To use your external calls to make decisions, reference them from your rules.

For example, to reference an external call that is named **myCall** in your rule, use the following syntax:

External.myCall()

If **myCall** requires a parameter, such as *IPaddress*, use the following syntax:

External.myCall(@"device.ipAddress")

For information about the rules language and how you can use external calls in rules, see the [Language reference guide](fpl-lang-ref.md).

> [!NOTE]
> If external calls are used in a rule, the latency of the rule might increase.

## Understand authentication and authorization

To ensure that data is securely accessed, APIs often authenticate the sender of a request to verify that they have permission to access the data. External calls in Fraud Protection support two methods of authentication: *Anonymous* and *AAD*.

If you select **Anonymous**, the authorization header in the HTTP request to the target endpoint will be left blank. Use this option when the target endpoint doesn't require an authorization header. For example, if your endpoint uses an API key, configure the key-value pair as part of the request URL that you enter in the **Web Request** field. The target endpoint can then validate if the API key from the request URL is allowed, and then decide whether permission should be granted.

If you select **AAD**, the authorization header in the HTTP request to the target endpoint will include a bearer token. A bearer token is a JSON Web Token (JWT) that is issued by Azure AD. For information about JWTs, see [Microsoft identity platform access tokens](https://docs.microsoft.com/azure/active-directory/develop/access-tokens). Fraud Protection appends the token value to the text "Bearer" in the required format in the request authorization header as shown here:

Bearer \<token\>

### Token claims

The following table lists the claims that you can expect in bearer tokens that are issued by Fraud Protection.

| Name           | Claim | Description |
|----------------|-------|-------------|
| Tenant ID      | tid   | This claim identifies the Azure tenant ID of the subscription that is associated with your Fraud Protection account. For information about how to find your tenant ID in the Fraud Protection portal, see [Required IDs and information](integrate-real-time-api.md#required-ids-and-information). For information about how to find your tenant ID in the Azure portal, see [How to find your Azure Active Directory tenant ID](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-how-to-find-tenant). |
| Audience       | aud   | This claim identifies the intended recipient of the token. The value will exactly reflect the application ID that you provided when you configured your external call in the Fraud Protection portal. |
| Application ID | appid | This claim is Fraud Protection's application ID: *bf04bdab-e06f-44f3-9821-d3af64fc93a9*. This ID is owned solely by Fraud Protection and only Microsoft can request a token on its behalf. |

When your API receives a token, it should open the token and validate that each of the preceding claims matches its description.

Here is an example that shows how you can authenticate an incoming request by using [JwtSecurityTokenHandler](https://docs.microsoft.com/dotnet/api/system.identitymodel.tokens.jwt.jwtsecuritytokenhandler?).

```C#
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

## External data practices

You acknowledge that you are responsible for adhering to all applicable laws and regulations, including without limitation data protection laws, contractual restrictions and/or policies related to data sets you provide to Microsoft through the External Calls feature of Fraud Protection. Further, you acknowledge that your use of Fraud Protection is subject to use restrictions detailed in the [Microsoft Customer Agreement](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftDynamics365Services/MCA), which states that you may not use Fraud Protection (i) as the sole factor in determining whether to proceed with a payment transaction; (ii) as a factor in determining any person's financial status, financial history, creditworthiness, or eligibility for insurance, housing, or employment; or (iii) to make decisions that produce legal effects or significantly affect a person. You are also prohibited from providing or otherwise using sensitive or highly regulated data types in connection with your use of the external calls feature of Fraud Protection. Please take time to review any data set or data types before you use them in connection with the external calls feature of Fraud Protection to ensure that you are compliant with this provision. Microsoft also reserves the right to verify that you are compliant with this provision.
