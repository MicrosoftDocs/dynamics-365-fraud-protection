---
author: yvonnedeq
description: This topic explains how to use velocities to examine user and entity patterns to flag potential fraud in Microsoft Dynamics 365 Fraud Protection.

ms.author: v-madeq
ms.service: fraud-protection
ms.date: 03/23/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Perform velocity checks

---

# Perform velocity checks

## Overview

Velocity checks allow you to identify patterns of events from a user or entity (such as a credit card)    whose frequency might indicate suspicious activity and potential fraud.  For example, after trying a few individual orders, fraudsters often place many orders quickly with a single credit card, from a single IP address, or device. They may also place many orders quickly with many different credit cards.  By defining velocities, you can watch incoming events for these types of patterns and use rules to define thresholds beyond which you want to treat these patterns as suspicious. 

## Define a velocity

Velocity sets are made up of individual velocities. You define velocities in Fraud Protection with the **SELECT**, **FROM**, **WHEN**, and **GROUPBY** keywords, using the following structure:

 ```FraudProtectionLanguage
SELECT <aggregation method> AS <velocity name>
FROM <event type>
WHEN <condition>
GROUPBY <attribute name>

```

- After **SELECT**, select an aggregation method (Count, DistinctCount, or Sum), and then name your velocity using the **AS** keyword. This name can be used to reference your velocity in rules. 

| Aggregation Method | Description                 | Example  |
|--------------------|-----------------------------|----------|
| Count              | Returns the number of times an event has occurred.  | SELECT Count() AS numPurchases  | 
| DistinctCount      | Returns the number of distinct values for the specified property. If the specified property is null or empty for an incoming event, the event will not contribute to the aggregation.  | SELECT DistinctCount(@”device.ipAddress”) AS distinctIPaddresses  | 
| Sum                | Returns the sum of values for a specified numeric property. | SELECT Sum(@”totalAmount”) AS totalSpending  | 

- After **FROM**, select an assessment on which to observe your velocity: Purchase, AccountLogin, or AccountCreation. 
- *The **WHEN** statement is optional.* After **WHEN**, you may type a Boolean expression. Only events matching this condition are considered in the aggregation. Other events are ignored. This expression is used to filter the events which are considered in the velocity.
- After **GROUPBY**, select a property or an expression. This property/expression is evaluated for every event processed. Events whose GROUPBY expression evaluates to the same value are combined to calculate the requested Count, DistinctCount, or Sum. If the GROUPBY expression is null or empty for an incoming event, the event will not contribute to the aggregation.

> [!TIP]
> Any expression which can be used in a rule can also be used in a velocity. This includes lists and external calls. For a full list of available functions, see the [Language Reference Guide](fpl-lang-ref.md).

> [!NOTE]
> The time window over which you’d like to observe the velocity is specified when you reference the velocity from a rule, not in the velocity definition itself. 

### Examples of velocities 

Use the following examples to create your own velocities.

**How much money each user has spent:**

```FraudProtectionLanguage
SELECT Sum(@”totalAmount”) AS totalSpending_perUser
FROM Purchase   
GROUPBY @”user.userId” 

```

**How many times each IP address has been used to create a new account:**

```FraudProtectionLanguage
SELECT Count() AS NewAccounts_perIP
FROM AccountCreation
GROUPBY @”device.ipAddress”

```

**For each device, how  many unique users have logged in:**

```FraudProtectionLanguage
SELECT DistinctCount(@”user.userId”) AS uniqueUserLogins_perDevice
FROM AccountLogin
GROUPBY @”deviceAttributes.deviceId” 

```

**For each user, how many login attempts were made which were rejected by Fraud Protection or received a high-risk score:**

```FraudProtectionLanguage
SELECT Count() AS loginRejections_perUser
FROM AccountLogin
WHEN @”ruleEvaluation.decision” == “Reject”or @riskScore > 900
GROUPBY @”user.userId”

```

**For each user, how many purchases were made outside of the US which also contained a product on a high risk list:**

```FraudProtectionLanguage
SELECT Count() AS intlHighRiskTxns_perUser
FROM Purchase
WHEN @”user.country” != “US” and ContainsKey(“Risky Products”, “Product ID”, @”ProductList.productId”)
GROUPBY @”user.userId”

```

## Create a velocity set

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **Velocities**, and then select **New velocity set**. 

    Fraud Protection creates a velocity set draft which is only visible to you (the creator). Note that all changes made to the draft are saved automatically.

2. (Optional) In the **Condition** box, you can either write a Boolean condition or leave it blank. 

    Only events matching this condition are considered in the aggregation. Others events are ignored.
    For example, if you want the velocities in your velocity set to only aggregate events which take place in the United States, define the following condition:

    WHEN @”user.countryRegion” == “US”

3. To define a new velocity from scratch, select **New velocity**. For information about defining velocities, see [Define a velocity](velocities.md#define-a-velocity). 

   You can also start from an existing velocity template by selecting the arrow to the right of **New velocity**. 
   To view a full list of templates and their contents, select **See all**.
   
   You can add up to 10 velocities in a set. 
    
4. To publish your velocity, select **Publish**. 

   In the confirmation dialog, you can change the name, description, or status of the velocity. When you are ready, select **Publish**.

   Once published, the velocities in the set are visible to all. As events flow through Fraud Protection, the velocities will begin aggregating data. 

    
   For information about using your velocities to make decisions, see [Use a velocity in rules](velocities.md#use-a-velocity-in-rules). 

> [!NOTE]
> Once a velocity is published, it will start aggregating data from that point forward. Historical data will not be considered.

### Understand the Sample panel

When you create or edit a velocity set, the **Sample** panel appears on the right side of the page. 

- The **Sample** panel displays all the properties of an event that can be referenced in your velocities. These properties differ depending on which event type your velocity observes. Select the event type from the **Event** dropdown at the top of the panel.
- The **payload sample** section contains an example of the properties that can be sent in the request API for the assessment. 
- The **enrichment sample** contains an example of properties that are added to your event by Fraud Protection, after the initial request has been sent. For examples, this includes   information from Fraud Protection’s [device fingerprinting](device-fingerprinting.md) solution, as well as risk and bot scores from our machine learning models. 

    The enrichment sample also includes information from rule evaluation, such as the decision, the rule name, and the clause name that was triggered. Any of these properties can be used in your velocity, and can be referenced using @. For example: @”user.firstName”.

## Manage your velocity sets

- To edit an existing published velocity set, select the velocity, and then select **Edit**. 

    This creates a draft of your published velocity and is set to be only visible to you. All   changes you make to the draft are saved automatically. 

    When you are ready to push your changes into production, select **Publish**. This action overwrites the previously published velocity set with your new changes. 
    
    > [!NOTE]
    > Any changes you make to a velocity will only affect the values calculated from that point forward. Changes do not apply to previous event data.    

- To delete an existing velocity set, select the ellipsis, and then select **Delete**. 

    > [!NOTE]
    > You can’t delete a velocity set if any of its velocities are referenced in a published rule. 

- To update the name or description of a velocity set, select the ellipsis, and then select **Rename**.

- To change the status of your velocity set, select **Activate** or **Deactivate**. 

    The velocities in a velocity set marked as *Active* are constantly updated as new events flow into Fraud Protection. 
    The velocities in a set which is marked as *Inactive* are never updated. 
    
## Use a velocity in rules

To use your velocities to make decisions on incoming assessment events, you must reference them in your rules. For example, if the following velocity is defined as part of a set:

```FraudProtectionLanguage
FROM Purchase AS totalSpending
SELECT Sum(@”totalAmount”)
GROUPBY @”user.userId”

```

In your rule, you can perform a velocity check using  the following syntax: 

```FraudProtectionLanguage
Velocity.totalSpending(@”user.userId”, 7d)

```

The first parameter is the **key**, which will be used to lookup the velocity. In the velocity definition above for  **totalSpending**, the GROUPBY @”user.userId” statement indicates that values will be aggregated for each user ID encountered. When referencing the velocity from a rule, the **key** parameter specifies the specific user id to retrieve the velocity value for. If the key parameter is null or empty, Fraud Protection returns 0. 

The second parameter is the **timeWindow** on which you observe the velocity. You can select a time window between 1 minute and 7 days. Currently, the following are all valid time windows:

- [1-59]m
- [1-23]h
- [1-7]d

In the future, this list will be expanded.

> [!NOTE]
> The time window begins at the start of the previous unit of measurement. For example, if the current date and time is April 1, 2021 11:04 am, and you check a velocity over the timeWindow 2h, you will see the data since 9:00 am, not 9:04 am. 

> [!NOTE]
> If the velocity fails to return a value due to an error, a default value of 0 is returned, and your rule continues to execute.

> [!NOTE]
> Velocities are updated only after all rules have been evaluated. Therefore, when you reference a velocity in a rule, it will not be included in  the current event being processed.

## Use rules to view velocity values  

In addition to returning decisions, rules can also utilize observation functions such as Trace() and Other(). For more information on observation functions, see the [Language Reference Guide](fpl-lang-ref.md). 

You can use Other() to print out velocity values in each Assessment API response. For example, you can create the following rule:

```FraudProtectionLanguage
RETURN Approve(), Other(
    totalSpending_7d = Velocity.totalSpending_perUser(@"user.userId", 7d),
    loginsPerDevice_1m = Velocity.login_count_perDevice(@"deviceAttributes.deviceId", 1m)
)

```

Each Account Login or Account Creation event that triggers this rule, will then the following section in the API response:

```JSON
      "Other": {
        "clause1": {
          "totalSpending_7d": "0",
          "loginsPerDevice_1m": "0"
        }
      },

```

> [!NOTE]
> This behavior does not apply to Purchase events. 

Alternatively, instead of printing the velocity values directly to the API response, you can also send the values to your own Azure Event Hubs or Blob Storage, using [event tracing](event-tracing.md). For example, you can create the following rule: 

```FraudProtectionLanguage
RETURN Approve(), Trace(
    totalSpending_7d = Velocity.totalSpending_perUser(@"user.userId", 7d),
    loginsPerDevice_1m = Velocity.login_count_perDevice(@"deviceAttributes.deviceId", 1m)
)

```

If you subscribe to the [FraudProtection.Trace.Rule event](event-tracing.md#trace-events), the following information will be sent as part of each event:

```JSON
    "attributes": {
"totalSpending_7d": 523.99
      "loginsPerDevice_1m": 1
    }

```
