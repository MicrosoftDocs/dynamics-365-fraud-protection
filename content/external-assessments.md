---
author: swasif23
description: This article provides an overview of the external assessments capability in Microsoft Dynamics 365 Fraud Protection.
ms.author: swasif
ms.date: 07/22/2023
ms.topic: conceptual
search.audienceType:
  - admin
title: External assessments

---

# External assessments

External assessment is a mechanism to call an assessment from any other assessment. An external assessment isn't an assessment itself. Instead, it acts like a data source which allows you to send data and receive a response from a target assessment. 
An assessment can have one of two possible sharing settings:
- Private: Accessible only in assessment’s root environment
- Shared: Accessible in all environments in the tenant

External assessment can be set up to point to any **Private** assessment, available in the same root environment, or any **Shared** assessment, available in any root environment of the tenant. 
> [!Note]
> To learn more about how to change sharing setting of an assessment from Private to Shared or vice versa, please visit [Assessment configuration overview](assessment-configure-existing.md)

After an external assessment has been set up, it can be called through a rule from any assessment in that environment. 

![External assessment flow](media/external-assessments.png)
>*For Private Assessment: Environment Y = Environment X*
>
>*For Shared Assessment: Environment Y = Any root environment within the same tenant*

Calling assessment refers to any assessment that calls a Private or Shared assessment, through an External assessment. Calling assessment has to have an active Use an external assessment rule set up. When the rule condition is met, the rule will call the External Assessment and perform the configured actions. Similar to External calls, External assessments are not inherited by children. Hence, to use an External assessment in a rule, External assessment must be set up in the environment you want to call it from.  

## Create an External Assessment

To create an External Assessment, first ensure you have the right permission to perform this operation. To learn more user roles and permissions, see [User roles and access](user-roles-access.md)

1.	In the Fraud Protection portal, in the left navigation, select **External Assessments**, and then select **+ New external assessment**.
2.	On the **New external assessment** page, set the following fields:
  - **Target assessment to call** – In the drop-down you can see all the Private assessments, set up in the same root environment, as well as any available Shared assessments, set up in any root environment of the same tenant. Select the assessment you want to target.

  > [!NOTE]
  > If the Shared assessment you want to point your external assessment to is not showing in the drop-down, then check the Sharing setting of the assessment and ensure it is set to Shared. To learn more on how to configure Sharing setting please visit [Assessment configuration overview](assessment-configure-existing.md).

  - **Name** – Enter the name that you will use to reference the external assessment from your rules. The name can contain only numbers, letters, and underscores. It can't begin with a number.

  > [!NOTE]
  > You can't change the name of an external assessment after you use it in a rule.

  - **Description** – Add a description to help your team quickly identify the external assessment.
  - **API to preview** – Select the API you want to preview the sample code for. The sample code is the FQL you can use in a rule to call this shared assessment

  > [!NOTE]
  > You can use the external assessment to call Evaluate, Observation or Label API of the shared/private assessment it is pointing to. 

  - **Sample response** – This shows the sample response expected from the target assessment. The information shown here is manually provided by the target assessment admin, and is used to enable the IntelliSense, in Rule compiler, on the sample response fields
3.	When you've finished setting the required fields, select **Create**.

## Call an External Assessment

To use your external assessments, reference them from your rules. 
For example, to reference an external assessment, named **myAssessment**, in your rule use the following syntax:

```FraudProtectionLanguage
Assessments.myAssessment.Evaluate($baseInput = @@)
```

In the above example, ```$baseInput = @@```will map all fields needed by the shared/external assessment from the calling assessment’s payload. You can map specific fields only as well. You can also define what actions you want the rule to take based on the information it will receive back from the External assessment call.

For example,

```FraudProtectionLanguage
LET $card = {
  number: 12345,
  expy: "2023-03-10".ToDateTime()
}
LET $response = Assessments.MicroTx.evaluate(card = $card, user = @@"user")
OBSERVE Output(decision = $response.decisionDetails.merchantRuleDecision)

```
You can set up a rule to call the external assessment by either using the *Use an external assessment* rule template or copy/paste the sample FQL from the external assessment page. Please be sure to use the sample code for the API (Evaluate, Observe, Label) you want to call. The sample code will show all the fields that can be sent to the shared assessment. The required fields are marked as such in the code. 

Here is another sample FQL for calling the evaluate API of external assessment named **ExtAssessment1**:

```FraudProtectionLanguage
LET $customUser = {
    id: "userId123456",
    username: "johnsmith2",
    firstName: "John",
    lastName: "Smith",
    email: "johnsmith2@gmail.com",
    address: {
        street1: "0123 Bechtelar Loop",
        city: "Kubtown",
        state: "SC",
        zipCode: "44329",
        countryRegion: "US"
    }
}

LET $result = Assessments.ExtAssessment1.Evaluate(
    user = $customUser,
    specialConsideration = true)
OBSERVE Output(Result = $result)

```

External Calls and External Assessments may require complex structured objects as part of their request schema. For more information on how to use JSON Arrays and Objects, please check the [Language reference guide](fpl-lang-ref.md). 

## Monitor external calls in the Fraud Protection portal

Fraud Protection shows a tile that contains three metrics for each external assessment that you define:
- **Requests per second** – The total number of requests divided by the total number of minutes in the selected time frame.
- **Average latency** – The total number of requests divided by the total number of minutes in the selected time frame.
- **Success rate** – The total number of successful requests divided by the total number of requests that have been made.

The numbers and charts that are shown on this tile include only data for the time frame that you select in the drop-down list in the upper-right corner of the page.

> [!NOTE]
> Metrics are shown only when your external assessment is used in an active rule.

- To dive deeper into the data about your external assessment, select Performance in the right corner of the tile.
Fraud Protection shows a new page that has a more detailed view of the metrics.
- To view metrics for any time frame in the last three months, adjust the Date range setting at the top of the page.

In addition to the three metrics that were described earlier, an **Error** chart is also shown. This chart shows the number of errors by error type and code. To view error count over time, or to view the distribution of errors, select **Pie chart**.

In addition to HTTP client errors (400, 401, and 403), you might see the following errors:

- **Invalid application ID** – The application ID that was provided doesn't exist in your tenant, or it isn't valid.
- **Microsoft Entra failure** – The Microsoft Entra token could not be retrieved.
- **Definition not found** – The external call has been deleted, but it's still referenced in a rule.
- **Timeout** – The request to the target took longer than the specified time-out.
- **Communication failure** – No connection could be made to the target because of a network issue or because the target is unavailable.
- **Circuit breaker** – If the external call has failed continuously and has exceeded a certain threshold, all further calls will be suspended for a short interval.
- **Unknown Failure** – An internal Dynamics 365 failure occurred.


[!INCLUDE[footer-include](includes/footer-banner.md)]
