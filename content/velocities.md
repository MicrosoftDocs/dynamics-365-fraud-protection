---
author: josaw1
description: This article explains how to use velocities to examine user and entity patterns to flag potential fraud in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/27/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Perform velocity checks

---

# Perform velocity checks

The frequency of events from a user or entity (such as a credit card) might indicate suspicious activity and potential fraud. For example, after fraudsters try a few individual orders, they often use a single credit card to quickly place many orders from a single IP address or device. They might also use many different credit cards to quickly place many orders. Velocity checks help you identify these types of event patterns. By defining velocities, you can watch incoming events for these types of patterns and use rules to define thresholds beyond which you want to treat the patterns as suspicious.

If your instance of Microsoft Dynamics 365 Fraud Protection has multiple environments, you can define a velocity set in a specific environment by using the environment switcher. You can reference velocity only in the rules that are defined in the corresponding environment. If velocity is created in a parent environment, and the rule is defined in the same environment, the transactions in the child environments will be included in the velocity when the parent-level rule runs. 

## Define a velocity

Velocity sets are made up of individual velocities. You define velocities in Dynamics 365 Fraud Protection by using the **SELECT**, **FROM**, **WHEN**, and **GROUPBY** keywords in the following structure.

```FraudProtectionLanguage
SELECT <aggregation method> AS <velocity name>
FROM <event type>
WHEN <condition>
GROUPBY <attribute name>
```

> [!NOTE]
> Arrays can't be used to GROUPBY in a velocity definition.

- After **SELECT**, specify an aggregation method: *Count*, *DistinctCount*, or *Sum*. Then use the **AS** keyword to name the velocity. This name can then be used to reference the velocity in rules.

    Here is an explanation of the aggregation methods.

    | Aggregation method | Description | Example |
    |--------------------|-------------|---------|
    | Count              | This method returns the number of times that an event has occurred. | SELECT Count() AS numPurchases |
    | DistinctCount      | This method returns the number of distinct values for the specified property. If the specified property is null or empty for an incoming event, the event won't contribute to the aggregation. | SELECT DistinctCount(@"device.ipAddress") AS distinctIPaddresses |
    | Sum                | This method returns the sum of values for a specified numeric property. | SELECT Sum(@"totalAmount") AS totalSpending |

- After **FROM**, specify an assessment or observation event to observe the velocity on. Th field you want to observe velocity for, or group by, must be part of the API call. To observe a cross-event velocity, specify multiple events across assessments or observation events.
- *The **WHEN** statement is optional.* After **WHEN**, you can type a Boolean expression. Only events that match the condition are considered in the aggregation. Other events are ignored. The expression is used to filter the events that are considered in the velocity.
- After **GROUPBY**, specify a property or an expression. The property or expression is then evaluated for every event that is processed. All events that are evaluated to the same value in the **GROUPBY** statement are combined to calculate the aggregation that is specified in the **SELECT** statement. If the **GROUPBY** expression is null or empty for an incoming event, the event won't contribute to the aggregation.

> [!TIP]
> Any expression that can be used in a rule can also be used in a velocity. These expressions include lists and external calls. For a full list of available functions, see the [language reference guide](fpl-lang-ref.md).

> [!NOTE]
> The time window that you want to observe the velocity over isn't specified in the velocity definition itself. Instead, you specify it when you reference the velocity from a rule.

### Examples of velocities

Use the following examples to create your own velocities.

#### The amount of money that each user has spent

```FraudProtectionLanguage
SELECT Sum(@"totalAmount") AS totalSpending_perUser
FROM Purchase
GROUPBY @"user.userId"
```

#### The number of times that each IP address has been used to create a new account

```FraudProtectionLanguage
SELECT Count() AS NewAccounts_perIP
FROM AccountCreation
GROUPBY @"device.ipAddress"
```

#### For each device, the number of unique users who have signed in

```FraudProtectionLanguage
SELECT DistinctCount(@"user.userId") AS uniqueUserLogins_perDevice
FROM AccountLogin
GROUPBY @"deviceAttributes.deviceId"
```

#### For each user, the number of sign-in attempts that were rejected by Fraud Protection or received a high risk score

```FraudProtectionLanguage
SELECT Count() AS loginRejections_perUser
FROM AccountLogin
WHEN @"ruleEvaluation.decision" == "Reject" or @"riskScore" > 900
GROUPBY @"user.userId"
```

#### For each user, the number of purchases that were made outside of the US, and that also contained a product on a high risk list

```FraudProtectionLanguage
SELECT Count() AS intlHighRiskTxns_perUser
FROM Purchase
WHEN @"user.country" != "US" and ContainsKey("Risky Products", "Product ID", @"ProductList.productId")
GROUPBY @"user.userId
```

#### For each user, the number of unique custom emails that were used across an assessment and observation event

```FraudProtectionLanguage
SELECT DistinctCount(@"custom.email") AS uniqueEmails_perUser
FROM Assessment_A1, Assessment_A1:status
GROUPBY @"custom.userId"
```

## Create a velocity set

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **Velocities**, and then select **New velocity set**.

    Fraud Protection creates a draft velocity set that is visible only to you (the creator). Note that all changes that you make to the draft are automatically saved.

2. Optional: In the **Condition** field, enter a Boolean condition. Alternatively, leave the field blank.

    Only events that match this condition are considered in the aggregation. Other events are ignored. For example, if you want the velocities in the velocity set to aggregate only events that occur in the United States, define the following condition:

    WHEN @"user.countryRegion" == "US"

3. To define a new velocity from scratch, select **New velocity**. For information about how to define velocities, see the [Define a velocity](velocities.md#define-a-velocity) section earlier in this article.

    To start from an existing velocity template, select the arrow to the right of **New velocity**. To view a full list of existing templates and their contents, select **See all**.

    You can add up to 10 velocities in a set.

4. To publish the velocity, select **Publish**.
5. In the confirmation dialog box, you can change the name, description, or status of the velocity. When you're ready, select **Publish**.

After the velocity is published, the velocities in the velocity set are visible to all users. As events flow through Fraud Protection, the velocities will start to aggregate data.

> [!NOTE]
> After a velocity is published, it starts to aggregate data from that point forward. Historical data isn't considered.

For information about how to use your velocities to make decisions, see the [Use a velocity in rules](velocities.md#use-a-velocity-in-rules) section later in this article.

### Understand the Sample pane

When you create or edit a velocity set, the **Sample** pane appears on the right side of the page.

- The **Sample** pane shows all the event properties that can be referenced in your velocities. These properties vary, depending on the type of event that your velocity observes. Select the event type in the **Event** field at the top of the pane.
- The **payload sample** section contains an example of the properties that can be sent in the request API for the assessment.
- The **enrichment sample** section contains an example of the properties that Fraud Protection adds to your event after the initial request has been sent. For example, these properties include information from Fraud Protection's [device fingerprinting](device-fingerprinting.md) solution, and risk and bot scores from the machine learning models.

    The enrichment sample also includes information from rule evaluation, such as the decision, the rule name, and the name of the clause that was triggered. You can use any of these properties in your velocity. Use an at sign (@) to reference them (for example, *@"user.firstName"*).

## System-defined (default) velocities

Fraud Protection creates several system-defined velocities per environment. For example, the following default velocities may be added.

- **Default - Email velocities**
- **Default - Payment instrument velocities**
- **Default - IP velocities**
- **Default - Device ID velocities**

Some Fraud Protection functionality relies on the default velocities, such as the **Search results** page for purchase protection. 

You can't edit or delete system-defined velocities. However, you can clone them and then edit or delete the clones. 

## Manage your velocity sets

- To edit an existing published velocity set, select the velocity, and then select **Edit**.

    A draft of your published velocity is created and is visible only to you. All changes that you make to the draft are automatically saved.

    When you're ready to push your changes into production, select **Publish**. The previously published velocity set is overwritten with your changes.

    > [!NOTE]
    > Any changes that you make to a velocity affect only the values that are calculated from that point forward. They don't affect previous event data.

- To delete an existing velocity set, select the ellipsis (**...**), and then select **Delete**.

    > [!NOTE]
    > You can't delete a velocity set if any of its velocities are referenced in a published rule.

- To update the name or description of a velocity set, select the ellipsis (**...**), and then select **Rename**.
- To change the status of your velocity set, select **Activate** or **Deactivate**.

    - The velocities in a velocity set that is marked as *Active* are constantly updated as new events flow into Fraud Protection.
    - The velocities in a velocity set that is marked as *Inactive* are never updated.

## Use a velocity in rules

To use your velocities to make decisions about incoming assessment events, you must reference them in your rules. For example, the following velocity is defined as part of a velocity set.

```FraudProtectionLanguage
SELECT Sum(@"totalAmount") AS totalSpending_perUser
FROM Purchase 
GROUPBY @"user.userId"
WHEN Velocity.totalSpending_perUser(@"user.userid", 7d) > 1000
```

In your rule, you can do a velocity check by using the following syntax.

```FraudProtectionLanguage
WHEN Velocity.totalSpending_perUser(@"user.userid", 7d) > 1000
```

The first parameter is **key**. This parameter is used to look up the velocity. In the preceding velocity definition for **totalSpending**, the **GROUPBY\ @"user.userId"** statement indicates that values will be aggregated for each user ID that is encountered. When you reference the velocity from a rule, the **key** parameter specifies the user ID to retrieve the velocity value for. If the **key** parameter is null or empty, Fraud Protection returns *0*.

The second parameter is **timeWindow**. This parameter specifies the time window that you want to observe the velocity over. You can select a time window between one second to ninety days. Currently, the following are all valid time windows:

- \[1–59\]s
- \[1–59\]m
- \[1–23\]h
- \[1–90\]d


> [!NOTE]
> The time window begins at the start of the previous unit of measure. For example, if the current date and time are 11:04 AM on April 1, 2021, and you check a velocity over a two-hour (*2h*) time window, you will see the data since 9:00 AM, not since 9:04 AM.
>
> If a velocity fails to return a value because of an error, a default value of *0* is returned, and your rule continues to run.
>
> Velocities are updated with the current event after rule evaluation. Therefore, if you reference a velocity in a rule, it wouldn't include the current event being processed.

## Use rules to view velocity values

In addition to returning decisions, rules can use [observation functions](fpl-lang-ref.md#observation-functions) such as **Output()** to print certain values to the API response. For example, a user could write the following clause, which does not make a decision, but will simply output the values of several velocities in the API response.

```FraudProtectionLanguage
OBSERVE Output(
    totalSpending_7d = Velocity.totalSpending_perUser(@"user.userid", 7d),
    loginsPerDevice_1m = Velocity.loginCount_perDevice(@"deviceAttributes.deviceId", 1m)
)
```

Each assessment event that triggers this rule will then print the following section in the API response:

```JSON
"MerchantRuleOutput": {
    "clause1": {
        "totalSpending_7d": "523.99",
        "loginsPerDevice_1m": "1"
    }
},
```

Instead of printing the velocity values directly to the API response, you can use [event tracing](event-tracing.md) to send the values to your own instance of Azure Event Hubs or Azure Blob Storage. For example, you create the following rule.

```FraudProtectionLanguage
RETURN Approve(), Trace(
    totalSpending_7d = Velocity.totalSpending_perUser(@"user.userid", 7d),
    loginsPerDevice_1m = Velocity.loginCount_perDevice(@"deviceAttributes.deviceId", 1m)
)
```

If you subscribe to the [FraudProtection.Trace.Rule event](event-tracing.md#trace-events), the following information will then be sent as part of each event.

```JSON
"attributes": {
    "totalSpending_7d": 523.99
    "loginsPerDevice_1m": 1
}
```

## Additional resources

- Video: [Learn about the new velocity feature in Dynamics 365 Fraud Protection](https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DsCPt3o8Qg30&data=04%7C01%7Cv-madeq%40microsoft.com%7C25acb8fe676d47dd48bb08d908cb2c10%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637550490968740595%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C1000&sdata=Epc2wB1eV5G8p5hPg1WCtlFlwGMujavBzD2r%2FqtQtwo%3D&reserved=0)
- Blog: [Customize your protection with new features in the Dynamics 365 Fraud Protection preview: Identify potential fraud with velocities](https://cloudblogs.microsoft.com/dynamics365/bdm/2021/04/14/customize-your-protection-with-new-features-in-the-dynamics-365-fraud-protection-preview/)
