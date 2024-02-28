---
author: josaw1
description: This article describes how to use external calls to ingest data from APIs in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/28/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: External calls

---

# External calls

This article describes how to use external calls to ingest data from APIs in Microsoft Dynamics 365 Fraud Protection.

External calls let you ingest data from APIs outside Microsoft Dynamics 365 Fraud Protection and then use that data to make informed decisions in real time. For example, third-party address and phone verification services, or your own custom scoring models, might provide critical input that helps determine the risk level for some events. By using external calls, you can connect to any API endpoint, make a request to that endpoint from within your rule as required, and use the response from that endpoint to make a decision.

> [!NOTE]
> If additional data is needed for all events, you can also send it as part of the assessment schema. For more information about how to send custom data as part of an API request, see [Custom data sample](view-purchase-protection-schemas.md#custom-data-sample).

## Types of APIs that can be used in an external call

Before you create an external call, you should know about the following limitations:
- Fraud Protection currently supports only the following authentication methods: *Anonymous*, *Basic*, *Certificate*, *OAuth (Microsoft Entra ID)*, *OAuth (Generic)*, and *OAuth (Custom token)*.
- Fraud Protection currently supports only the following HTTP methods: *GET* and *POST*.

> [!NOTE]
> To learn more about Microsoft's external data practices, see [External data practices](#external-data-practices).

## Create an external call

To create an external call, follow mthese steps.

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **External Calls**, and then select **New external call**.
1. Review and set the following fields as required:

    - **Name** – Enter the name that you will use to reference the external call from your rules. The name can contain only numbers, letters, and underscores. It can't begin with a number.

        > [!NOTE]
        > You can't change the name of an external call after you use it in a rule.

    - **Description** – Add a description to help your team quickly identify the external call.   
    - **Add parameter** – You can use parameters to pass data from Fraud Protection to your API endpoint. Depending on the HTTP method you selected, these parameters are sent to the endpoint either in the query string or as part of the request body. You can manually add parameters defined in this step to the request URL, header, and/or body using the format `{parameter.\<parameter name\>}`. All parameter values are interpreted as strings. You can add sample values for each parameter that Fraud Protection uses to make a sample call to your endpoint, either before creation, or whenever you select **Test connection**.

        > [!NOTE]
        > You can use the `Request.CorrelationId()` function in a rule to extract the correlation ID of an incoming event and pass it as a parameter value for the external call.

    - **Add configuration** – You can provide fixed configuration data on the external call setup page. For sensitive information, you can mark a configuration to be a secret and provide a secret identifier URL from your Azure Key Vault instead of the actual value. For information on how to store secrets in your Azure Key Vault and provide access to Fraud Protection, see [Store passwords in your Azure Key Vault](external-calls.md#Store-passwords-in-your-Azure-Key-Vault). 

    Like parameters, configurations defined in this step can be manually added to the request URL, header, and/or body using the format *{configuration.\<configuration name\>}*. However, unlike parameters where the actual value is passed from the rule, the configuration values provided on the external call setup page are used when making sample or actual calls.

     - **Web request** – Select the appropriate HTTP method (**GET** or **POST**), and then enter the API endpoint.

        > [!NOTE]
        > Only HTTPS endpoints are supported.

    - **Authentication** – Select the method to use to authenticate incoming requests. For more information about authentication, authentication-specific fields, authorization, and Microsoft Entra tokens, see [Understand authentication and authorization](external-calls.md#understand-authentication-and-authorization).
   - **Headers** - You can provide headers as needed. The default value of **Content-Type** is "application/json". Currently, Fraud Protection only supports "application/json" and "application/x-www-form-urlencoded" content types.
    - **Sample request** – Provides an example of the request that's sent to your external call. The request should reflect the parameter names and values that you specified, and it can't be edited. You can also add configurations to the request URL or body as well. 

        > [!NOTE]
        > For the *GET* method, no request body is included. 

       For *POST* methods, the request body is shown. You can construct a custom request body for a POST call by selecting **+ Advanced build your own request**. The sample request is used to make a sample call to your endpoint, either before creation or whenever you select **Test connection**.

     - **Sample response** – Provides an example of the data that's returned in a successful response from your API endpoint. This data must be in JavaScript Object Notation (JSON) format and can be referenced in your rules. The sample response that you provide is shown in the rule editor, and also enables autocomplete on the response fields. Select **{} Get API response** to automatically enter an actual response from your API in this field.
       
        > [!NOTE]
        > Sample response has to be poppulated in order to successfully complete the external call setup.
        
    - **Timeout** – Specify how long, in milliseconds, the request should wait before it times out. You must specify a number between 1 and 5000.
    - **Default response** – Specify the default response that should be returned if your request fails or exceeds the specified time-out. The value must be valid JSON object or JSON element.

1. Optional: To send a sample request to your API endpoint and view the response, select **Test connection**. For more information, [Test an external call](external-calls.md#test-an-external-call).
1. When finished setting the required fields, select **Create**.

## Test an external call

To ensure that Fraud Protection can connect to your endpoint, test the connection at any point.

- To test a connection while you're creating a new external call or editing an existing external call, set all the required fields, and then select **Test connection**. Fraud Protection uses the endpoint and parameters that you provided to send a request to your external call. You can also manually add configurations in the URL, header, or request body. 
- If Fraud Protection successfully reaches the target endpoint, a green message bar appears at the top of the panel to inform you that the connection was successful. To view the full response, select **See details**.
- If Fraud Protection can't reach the target endpoint, or if it doesn't receive a response before the specified time-out, a red message bar appears at the top of the panel and shows the error that was generated. To view more information about the error, select **See details**.

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
- **Microsoft Entra failure** – The Microsoft Entra token could not be retrieved.
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
- To test that Fraud Protection can still connect to your external call, select the ellipsis (**...**), and then select **Test connection**.

## Use an external call in rules

To use your external calls to make decisions, reference them from your rules.

For example, to reference an external call that's named **myCall** in your rule, use the following syntax:

External.myCall()

If **myCall** requires a parameter, such as *IPaddress*, use the following syntax:

External.myCall(@"device.ipAddress")

You can also access the Diagnostics object in rules, which can enable you to discover important diagnostic and debug information from an external call response. The Diagnostics object contains the Request payload, Endpoint, HttpStatus code, Error message, and Latency. Any of these fields can be accessed in the rules experience and can be used with the Observe Output method to create custom properties. It's important to note that the Diagnostics object has to be created by using its corresponding extension method, “.GetDiagnostics()”, before the object’s fields can be used in the rules. 

Below is a sample rule using the Diagnostic object:

```FraudProtectionLanguage
LET $extResponse = External. myCall(@"device.ipAddress")
LET $extResponseDiagnostics = $extResponse.GetDiagnostics()
OBSERVE Output(Diagnostics = $extResponseDiagnostics ) 
WHEN $extResponseDiagnostics.HttpStatusCode != 200
```
For information about the rules language and how you can use external calls in rules, see the [Language reference guide](fpl-lang-ref.md).

> [!NOTE]
> If you use external calls in a rule, the latency of the rule might increase.

## Understand authentication and authorization

To ensure that data is securely accessed, APIs often authenticate the sender of a request to verify that they have permission to access the data. External calls in Fraud Protection support the following methods of authentication:
- Anonymous
- Basic
- Certificate
- OAuth (Microsoft Entra ID) *(formerly Azure Active Directory)*
- OAuth (Generic)
- OAuth (Custom token)

> [!NOTE]
> Currently, Fraud Protection supports only the following HTTP methods:
> - GET
>- POST

### Anonymous

If you select **Anonymous**, the authorization header in the HTTP request to the target endpoint will be left blank. Use this option when the target endpoint does not require an authorization header. For example, if your endpoint uses an API key, configure the key-value pair as part of the request URL that you enter in the **Web Request** field. The target endpoint can then validate if the API key from the request URL is allowed, and then decide whether permission should be granted.

### Basic

If you select **Basic** as the authentication method, provide the following information to set up the external call:
- **Username** – Provide the username for the URL that you're trying to connect to.
- **Password URL** – Provide the password identifier URL from your Azure Key Vault for basic authentication. FOr information on how to store a password in your Azure Key Vault and provide access to Fraud Protection, see [Store passwords in your Azure Key Vault](external-calls.md#store-passwords-in-your-Azure-Key-Vault).

### Certificate

If you select **Certificate** as the authentication method, provide the following information to setup the external call:
- **Certificate URL** – Provide the certificate identifier URL from your Azure Key Vault. For information on how to generate a certificate in your Azure Key Vault and provide access to Fraud Protection, see [Create a certificate in your Azure Key Vault](external-calls.md#Create-a-certificate-in-your-Azure-Key-Vault).

### OAuth (Microsoft Entra ID)

If you select **OAuth (Microsoft Entra ID)** (formerly Azure Active Directory) as the authentication method, provide the following additional information to setup the external call:
- **Audience** - If you selected OAuth (Microsoft Entra ID) as the authentication method, you'll be asked to provide an audience. You can use an existing Azure application as the audience or create a new one through the integration experience within the Fraud Protection portal. Ensure the audience has permission to access the external call/service. For more information about how to configure Microsoft Entra authentication, see [Configure Microsoft Entra authentication](/azure/app-service/configure-authentication-provider-aad?tabs=workforce-tenant). 
- **Application ID** – You must provide the application ID of a new or existing Microsoft Entra application within your Fraud Protection subscription tenant. Generate a certificate in your Azure Key Vault. The Fraud Protection app should have read access to this Azure Key Vault. For information on how to generate a certificate in your Azure Key Vault and provide access to Fraud Protection, see [Create a certificate in your Azure Key Vault](external-calls.md#Create-a-certificate-in-your-Azure-Key-Vault). Load the certificate to this Microsoft Entra application. For more information about how to create and manage Microsoft Entra applications, see [Create Microsoft Entra Applications](integrate-real-time-api.md#create-microsoft-entra-applications).
- **Certificate URL** – Provide the certificate identifier URL from your Azure Key Vault. This is the same certificate you uploaded to the Microsoft Entra app earlier. 

When you select **Microsoft Entra ID**, the authorization header in the HTTP request to the target endpoint includes a bearer token. A bearer token is a JSON Web Token (JWT) issued by Microsoft Entra ID. For more information about JWTs, see [Microsoft identity platform access tokens](/azure/active-directory/develop/access-tokens). Fraud Protection appends the token value to the text "Bearer" in the required format in the request authorization header as shown in the following example:

Bearer \<token\>

#### Token claims

The following table lists the claims that you can expect in bearer tokens that are issued by Fraud Protection.

| Name           | Claim | Description |
|----------------|-------|-------------|
| Tenant ID      | tid   | This claim identifies the Azure tenant ID of the subscription that's associated with your Fraud Protection account. For information about how to find your tenant ID in the Fraud Protection portal, see [Required IDs and information](integrate-real-time-api.md#required-ids-and-information). For information about how to find your tenant ID in the Azure portal, see [How to find your Microsoft Entra tenant ID](/azure/active-directory/fundamentals/how-to-find-tenant). |
| Audience       | aud   | This claim identifies the Azure application that's authorized to access the external service you want to call. To learn more about how configure Microsoft Entra authentication, see [Configure Microsoft Entra authentication](/azure/app-service/configure-authentication-provider-aad?tabs=workforce-tenant) |
| Application ID | appid | This claim identifies who is requesting a token. To learn more about how configure Microsoft Entra authentication, see [Configure Microsoft Entra authentication](/azure/app-service/configure-authentication-provider-aad?tabs=workforce-tenant) |

When your API receives a token, it should open the token and validate that each of the preceding claims matches its description.

Here is an example that shows how you can authenticate an incoming request by using [JwtSecurityTokenHandler](/dotnet/api/system.identitymodel.tokens.jwt.jwtsecuritytokenhandler).

```C#
string authHeader = "Bearer <token>"; // the Authorization header value
var jwt = new JwtSecurityTokenHandler().ReadJwtToken(token);
string tid = jwt.Claims.Where(c => c.Type == "tid").FirstOrDefault()?.Value;
string aud = jwt.Claims.Where(c => c.Type == "aud").FirstOrDefault()?.Value;
string appid = jwt.Claims.Where(c => c.Type == "appid").FirstOrDefault()?.Value;
if(tid != "<my tenant id>" || aud != "<my audience>" || appid != "<my application id>")
{
    throw new Exception("the token is not authorized.");
}
```

### OAuth (Generic)

If you select **OAuth (Generic)** as the authentication method, provide the following additional information to setup the external call:
- **Token URL** – The API endpoint for the token call.
- **Token authentication** – Select either Anonymous or Basic authentication method for the token call.
- **Client ID/Username** – The client ID for anonymous authentication, or username for basic authentication. 
- **Client secret/Password URL** – The client secret identifier URL from your Azure Key Vault for anonymous authentication, or password identifier URL for basic authentication. For information on how to store a secret in your Azure Key Vault and provide access to Fraud Protection, see [Store passwords in your Azure Key Vault](external-calls.md#Store-passwords-in-your-Azure-Key-Vault).
- **Scope** – The scope value. 
- **Resource** – The Resource value (if needed).

### OAuth (Custom token)

If you select **OAuth (Custom token)** as the authentication method, you can configure a custom OAuth token call by selecting **+ Create token request** and providing the following information:
- **Configurations** – Configuration values you want to pass in the token call. For more information on configurations, see [Create an external call](#create-an-external-call).
- **Token URL** – The API endpoint for the token call.
- **Token authentication** – Select either the anonymous or basic authentication method for the token call.
- **Username** – Username for basic authentication. 
- **Password URL** – Password identifier URL from your Azure Key Vault for basic authentication. For information on how to store a password in your Azure Key Vault and provide access to Fraud Protection, see [Store passwords in your Azure Key Vault](external-calls.md#Store-passwords-in-your-Azure-Key-Vault).
- **Headers** – Header values. 
- **Sample request** – An example of the request that's sent to your token endpoint:
    - **Sample request URL** – A read-only field that shows the request URL used to make the sample call.
    - **Sample request body** – You can construct a custom request body for the token call by selecting **+ Advanced build your own request**. The sample request URL and body are used to make a sample call to your token endpoint, either before creation or whenever you select **Test connection**.
- **Timeout** – Specify the timeout duration between 1 and 5000.

## Work with Azure Key Vault

In accordance with Microsoft's commitment to your data security, Fraud Protection only allows you to provide Azure Key Vault URLs in the external call setup page for secrets, passwords, and certificates. 

### Store passwords in your Azure Key Vault 

To upload secrets or passwords to the Azure key vault and grant access permissions to Fraud Protection, follow these steps.

1. Sign in to the [Azure portal](https://portal.azure.com/#home) using your tenant credentials.
1. You can use an existing key vault, or create a new key vault by following the instructions in [Quickstart: Create a key vault using the Azure portal](/azure/key-vault/general/quick-create-portal). Ensure that **Get** and **List** are selected in the secret permissions.
1. In the left navigation pane, select **Secrets**, and then select **Generate/Import**.
1. On the **Create a secret** page, enter a name for your secret. The secret value should be the password for the web URL that you want to connect to using external calls.
1. Enter information in the required fields, and then select **Create**. Copy and save the secret identifier because you'll need it when setting up the external call in the Fraud Protection portal.
1. In the left navigation pane, under **Settings**, select **Access Policies**, and then select **Add new access policy**.
1. In the **Secret Permissions** section, select the **Get** and **List** checkboxes.
1. In the **Principal** and **Authorized application** fields, search for **Dynamics 365 Fraud Protection**, and then select **Select**.
1. Select **Add**, and then **Save**.

### Create a certificate in your Azure Key Vault 

Create a certificate in your Azure Key Vault, follow these steps. 

1. Sign in to the [Azure portal](https://portal.azure.com/#home) using your tenant credentials.
1. You can use an existing key vault, or create a new key vault by following the instructions in [Quickstart: Create a key vault using the Azure portal](/azure/key-vault/general/quick-create-portal). Make sure that **Get** and **List** are selected in the secret permissions.
1. In the left pane, select **Certificates**, and then click **Generate/Import**.
1. On the **Create a certificate** page, enter a name for your certificate. For **Subject**, enter the certificate subject.
1. Enter information in the required fields, and then select **Create**.
1. In left navigation pane, select **Access Policies**, and then select **Create**.
1. In the **Certificate Permissions** section, select the **Get** and **List** checkboxes.
1. In the **Principal** and **Authorized application** fields, search for **Dynamics 365 Fraud Protection**, and then select **Select**.
1. Select **Add**, and then **Save**.

For more information on how to generate a certificate in Azure Key Vault, see [Creating and merging a certificate signing request in Azure Key Vault](/azure/key-vault/certificates/create-certificate-signing-request?tabs=azure-portal).


## External data practices

You acknowledge that you are responsible for adhering to all applicable laws and regulations, including without limitation data protection laws, contractual restrictions and/or policies related to data sets you provide to Microsoft through the External Calls feature of Fraud Protection. Further, you acknowledge that your use of Fraud Protection is subject to use restrictions detailed in the [Microsoft Customer Agreement](https://www.microsoft.com/licensing/terms/productoffering/MicrosoftDynamics365Services/MCA), which states that you may not use Fraud Protection (i) as the sole factor in determining whether to proceed with a payment transaction; (ii) as a factor in determining any person's financial status, financial history, creditworthiness, or eligibility for insurance, housing, or employment; or (iii) to make decisions that produce legal effects or significantly affect a person. You are also prohibited from providing or otherwise using sensitive or highly regulated data types in connection with your use of the external calls feature of Fraud Protection. Please take time to review any data set or data types before you use them in connection with the external calls feature of Fraud Protection to ensure that you are compliant with this provision. Microsoft also reserves the right to verify that you are compliant with this provision.


## Additional resources

- Video: [Learn about the new external calls feature in Dynamics 365 Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DJM3KpsGYaag&data=04%7C01%7Cv-madeq%40microsoft.com%7C25acb8fe676d47dd48bb08d908cb2c10%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637550490968730638%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=7ePFKAsF4XwuaFur9WBmSRa0fDdCHDFbA%2FzQHOuoeLE%3D&reserved=0)
- Blog: [Customize your protection with new features in the Dynamics 365 Fraud Protection preview: Make informed decisions in real-time with external calls](https://cloudblogs.microsoft.com/dynamics365/bdm/2021/04/14/customize-your-protection-with-new-features-in-the-dynamics-365-fraud-protection-preview/)
