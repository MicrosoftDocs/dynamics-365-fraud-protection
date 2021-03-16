---
author: yvonnedeq
description: This topic explains how to use velocities to examine user and entity patterns to flag potential fraud in Microsoft Dynamics 365 Fraud Protection.

ms.author: v-madeq
ms.service: fraud-protection
ms.date: 03/16/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Perform velocity checks

---

# Perform velocity checks

## Overview

Velocity checks allow you to examine the historical patterns of a user or entity (for example, a credit card or an IP address) and then use these historical patterns to flag potential fraud. Fraudsters generally do not place a single order and stop – usually they experiment with one transaction first, and if it is successful, they follow up with additional transactions over a period of time until a flag is raised. 

Velocity checks help you understand how several separate and different events that occur over time may be related. They also help you understand how frequently certain data points recur. This factors enable you to quickly identify deviations from normal user behavior and take action accordingly. 

## Define a velocity

To define velocities in Fraud Protection, use the **FROM**, **SELECT**, **GROUPBY**, and **WHEN** keywords, within the following structure:

 ```json
FROM <*event type**aggregation method*> AS <*alias*>  
GROUPBY <*attribute name*>   
WHEN <*condition*>
```

- After **FROM**, select an assessment on which to observe your velocity: Purchase, AccountLogin, or AccountCreation. 
- After **SELECT**, select an aggregation method (Count, DistinctCount, or Sum), and then name your velocity using the **AS** keyword. This name can be used to reference your velocity in rules. 

| Aggregation Method | Description                 | Example  |
|--------------------|-----------------------------|----------|
| Count              | Returns the number of times an event has occurred.| SELECT Count() AS numPurchases  | 
| DistinctCount      | Returns the number of distinct values for the specified property.| SELECT DistinctCount(@”device.ipAddress”) AS distinctIPaddresses  | 
| Sum                | Returns the total sum of values for a specified numeric property, across all events which meet the condition. | SELECT Sum(@”totalAmount”) AS totalSpending  | 

- After **GROUPBY**, select a property or an expression. This property/expression is evaluated for every event processed. Events evaluated to the same value in GROUPBY are aggregated into a single value.
- **The **WHEN** statement is optional.** After **WHEN**, you may type a Boolean expression. Only events matching this condition are considered in the aggregation; other events are ignored.  

> [!NOTE]
> The time window over which you’d like to observe the velocity is specified when you reference the velocity from a rule, not in the velocity definition itself. 

### Examples of velocity checks

Use the following examples to create your own velocity checks.

#### How much money a specific user has spent

```json
FROM Purchase AS totalSpending_perUser  
SELECT Sum(@”totalAmount”)
GROUPBY @”user.userId”
```

#### How many times a specific IP address has been used to create a new account

```json
FROM AccountCreation AS newAccounts_perIP
SELECT Count()
GROUPBY @”device.ipAddress”
```

#### How many unique users have logged in using a specific device

```json
FROM AccountLogin AS uniqueUserLogins_perDevice
SELECT DistinctCount(@”user.userId”)
GROUPBY @”deviceId” 
```

#### How many login attempts has a specific user made which were rejected by Fraud Protection

```json
FROM AccountLogin AS loginRejections_perUser
SELECT Count()
GROUPBY @”user.userId”
WHEN @”ruleEvaluation.decision” == “Reject”
```

#### How many purchases has a specific user made from outside of the US, and which also received a high-risk score

```json
FROM Purchase AS intlHighRiskTxns_perUser
SELECT Count()
GROUPBY @”user.userId”
WHEN @”user.country” != “US” and @riskScore > 900
```

## Create a velocity set

1. In the [Fraud Protection portal](https://dfp.microsoft.com/), in the left navigation, select **Velocities**, and then select **New velocity set**. 

    Fraud Protection creates a velocity set draft which is only visible to you (the creator). Note that all changes made to the draft are saved automatically.

2. (Optional) In the **Condition** box, you can either write a Boolean condition or leave it blank. 

    -  To write a Boolean condition, begin with the keyword **WHEN**.  
    -  The **WHEN** keyword determines when your velocities are updated. For example, if you want the velocities in your velocity set to only update on events which take place in the United States, define the following condition:

```
WHEN @”user.countryRegion” == “US”
```

3.	Select **New velocity** to add a velocity. 

    For information about defining velocities, see [Defining a velocity](velocities.md#define-a-velocity). 
    You can add up to 10 velocities in a set. 

4.	To publish your velocity, select **Publish**. 

    In the confirmation dialog, you can change the name, description, or status of the velocity. 
    
5. When you are ready, select **Publish** to republish the velocity.

    Once published, the velocities in the set are visible to all. 
    As events flow through Fraud Protection, they begin aggregating data. 
    
For information about using your velocities to make decisions, see [Use a velocity in rules](velocities.md#use-a-velocity-in-rules). 

### Understand the Sample panel

When you create or edit a velocity set, the **Sample** panel appears on the right side of the page. 

The **Sample** panel displays all the properties of an event that can be referenced in your velocities. These properties differ depending on which event type your velocity observes. 

To select an event type from the **Sample** panel, select an event from the **Assessments** dropdown located at the top of the panel.

The **Payload sample** section contains an example of the properties that can be sent in the request API for the assessment. 

The **enrichment sample** contains an example of properties that are added to your event by Fraud Protection, after the initial request has been sent. For examples, information from Fraud Protection’s [device fingerprinting](device-fingerprinting.md) solution, as well as risk and bot scores from our machine learning models. The enrichment sample also includes information from rule evaluation, such as the decision, the rule name, and the clause name that was triggered. Any of these properties can be used in your velocity and can be referenced using @. For example: @”user.firstName”.

## Manage your velocity sets

- To edit an existing published velocity set, select the velocity, and then select **Edit**. 

    This creates a draft of your published velocity and is set to be only visible to you. 

    > [!NOTE]
    > All changes you make to the draft are saved automatically. 

- When you are ready to push your changes into production, select **Publish**. 

    This action overwrites the previously published velocity set with your new changes. 

- To delete an existing velocity set, select the ellipsis, and then select **Delete**. 

    > [!NOTE]
    > You can’t delete a velocity set if any of its velocities are referenced in a published rule. 

- To update the name or description of a velocity set, select the ellipsis, and then select **Rename**.

- To change the status of your velocity set, select **Activate** or **Deactivate**. 

    The velocities in a velocity set marked as *Active* are constantly updated as new events flow into Fraud Protection. 
    The velocities in a set which is marked as *Inactive* are never updated. 
    
## Use a velocity in rules

To use your velocities to make decisions on incoming assessment events, you must reference them in your rules. For example, if the following velocity is defined as part of a set:

```json
FROM Purchase AS myVelocity
SELECT Sum(@”totalAmount”)
GROUPBY @”user.userId”
```

Use the following syntax to reference this velocity in a rule:

```
Velocity.myVelocity(**String** key, **Timespan** timeWindow)
```

The first parameter, **key**, represents the key that will be used to lookup the velocity. In the velocity definition above for **myVelocity**, the **GROUPBY** @”user.userId” statement indicates that values will be aggregated for each user ID encountered. When referencing the velocity from a rule, the **key** parameter specifies the user id for which to retrieve the velocity. Therefore, either of the following statements is valid:

```
Velocity.myVelocity(@”user.userId”, 7d)
Velocity.myVelocity(“12345”, 7d)
```

The **timeWindow** parameter represents the time window on which you observe the velocity. You can select a time window anywhere between 1 minute and 7 days. The following are all valid time windows:

- [1-59]m
- [1-23]h
- [1-7]d

> [!NOTE]
> The time window begins at the start of the previous unit of measurement. For example: if the current date and time is Nov 27, 2020 11:04 am, and you check a velocity over the last 2 hours, you will see the data since 9:00 am, not 9:04 am. 

> [!NOTE]
> If the velocity fails to return a value due to an error, a default value of 0 is returned and your rule continues to execute.


