---
author: zhuoche
description: This topic explains the rule and list capabilities of the account protection feature in Microsoft Dynamics 365 Fraud Protection.
ms.author: v-davido
ms.service: fraud-protection
ms.date: 02/11/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Manage account protection rules and lists
---

# Manage account protection rules and lists

[!include [banner](includes/preview-banner.md)]

## Rules

You can use lists and rules to help automate the decision-making process for account protection. Rules shape real-time decisions from events, based on conditions and risk score thresholds that you select. Types of events include acceptance, rejection, challenges, and other user-defined settings. The rules use lists that you create and that consist of data that is relevant to your business.

These capabilities help you define the parameters that apply to your unique business, so that you can screen for risky account protection events. They also help you enforce various policies, such as geofencing policies. They are designed to help you manage the trade-offs that are inherent when you must prevent fraud.

The following operations are typically associated with rules:

- **New rule** – Create a new rule.
- **Rename** – Change the descriptive name of a rule.
- **Activate/deactivate** – Determine whether the rule affects the assessment application programming interface (API). (link)
- **Delete** – Remove a rule.
- **Move up/move down** – Change the execution order of rule.

Here are some typical components of rules:

- **Condition** – Conditions can be used to group together related rules. The rules will be run only if the condition is evaluated as true.
- **Clause** – Clauses return a decision, based on specific conditions. Clauses are run in sequential order. Some clauses are run before the machine learning (ML) model (that is, before any ML model score has been generated). Other clauses are run after a score has been generated.
- **Payload** – Payloads show a sample of what the payload for the account protection API looks like for a given event.

### Examples of rules (code example is still in progress)

Every condition should start with **WHEN**. It can accept any valid expression if its result is a Boolean value.

Here is an example of a condition.

```
WHEN Geo.CountryCode(@ip) == "BR"

WHEN @id == 100 

WHEN @count < 10 
```

The following example shows a clause that throws a challenge if the bot score is between 400 and 900.

```
Return Challenge(type = "sms", reason = "bot score") 
WHEN @botScore < 900 AND @botScore > 400 
```

The following example shows a clause that approves all users whose IP address is in a list.

```
Return Approve() 
WHEN ContainsKey(“iplist”, ”IPAddress”, @ip)
```

## Lists 

You can upload any number of lists to meet your specific business needs. After lists are uploaded, you can use them in your rules to achieve the business results that you require. To upload a list, select the **Lists** menu under **Account protection**.

Each list that you upload includes a collection of entities (that is, a collection of data of one or more columns) that you created offline and want to screen for. For example, you might upload a list of high-risk countries or regions. After you upload a list, you can give it a meaningful name and reference it in any rule.

As an example of how lists can be used, consider a scenario where a decision is made based on whether payload data is in a list.

The following operations are typically associated with lists:

- **New list** – Upload a new file that was created offline. (The file is a .csv file that includes headers.)
- **Download** – Save a list to the local computer as a file.
- **Edit** – Update an existing list by updating the list offline.
- **Delete** – Remove a list.

## Reference

> [!NOTE]
> Rule syntax is case-insensitive.

- Return statements:

    - `Approve (reason = "")`
    - `Reject (reason = "")`
    - `Challenge (type = "", reason = "")`
    - `Review (reason = "")`

- Logical operators:

    - `AND` (`&&`)
    - `OR` (`||`)
    - `-`
    - `==`
    - `@`
    - `IN`

- String operators:

    - `StartsWith`
    - `EndsWith`
    - `Contains`

- Math operators:

    - `Math.Min`
    - `Math.Max`
    - `Math.Average`

- Geo operators:

    - `Geo.RegionCode`
    - `Geo.Region`
    - `Geo.CountryCode`
    - `Geo.Country`
    - `Geo.City`
    - `Geo.PostalCode`
    - `Geo.Isp`
    - `Geo.MarketCode`

- How to use lists:

    - `ContainsKey(“dataset name”, ”index name”, @index_key)`
    - `Lookup(“dataset name”, “index name”, @index_key, “value name”)`

## Related topics

- [Account protection overview](account-protection.md)
- [View Account protection schemas](view-loss-prevent-schemas.md)
- [Account protection scorecard](ap-scorecard.md)
