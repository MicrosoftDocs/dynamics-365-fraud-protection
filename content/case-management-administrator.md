---
author: josaw1
description: This article explains how to work with Case management as an administrator.
ms.author: josaw
ms.date: 03/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management for administrators
ms.custom:
---

# Case management for administrators

To complete administrator-specific tasks in Case management for Microsoft Dynamics 365 Fraud Protection, you must be assigned one of the following roles:

- All areas of Administrator
- All areas of Editor
- PSP administrator
- Fraud Manager
- Fraud Supervisor

If you're assigned one of these roles, you can complete the following tasks:

- [Define cases for manual review agents](#review)
- [Create organization methods to store cases](#store)
- [Define the criteria to route cases to the appropriate queue](#route)

## <a name="review"></a>Define cases for manual review agents

Define the criteria that specific purchase transactions must meet to qualify for manual review. You can create assessment rules that generate a **Review()** decision as output. For more information about how to create these rules, see [Manage rules](rules.md). You can use any criteria that meet your business requirements.

The following example shows all transactions that must be selected for review. The risk score of the transactions is more than 600, and the user's country or region is **US**.

```
RETURN Review()
WHEN @"riskScore" > 600 and @"user.country" == "US"
```

## <a name="store"></a>Create organization methods to store cases

You can use queues to organize purchase transactions that the assessment rules mark for review. Transactions that appear in the case management queues are referred to as *cases*. You can create up to 29 queues for each environment.

Follow these steps to create a queue.

1. In the left navigation pane, select **Case management** \> **Queues**, and select **New queue**.
2. Enter a name that will help you identify the purpose of the queue.
3. Enter a description that explains the type of cases that are stored in this queue.
4. Select your preference for the review sequence. If you select **Unrestricted queue**, you can review any case in the queue in any order. If you select **Restricted queue**, you must review cases in a predefined order.
5. Select the default sorting and order to define the order that cases appear and are presented to review agents in. In a restricted queue, your selections define the order of cases that agents can review.
6. Select the time-out duration and default action to define the maximum amount of time that a case can be in the queue without being reviewed and the default action that is taken when that time is reached.

You can edit or delete any queue that you've created. To edit the name of a queue or delete a queue, remove the routing rules that have a dependency on the queue. For more information about routing rules, see the next section.

All your environments will have a system-created queue that is named **General**. Cases that don't qualify to be routed to a specific queue are routed to the **General** queue. The **General** queue has the following settings:

- **Timeout:** 24 hours 
- **Default action:** Approve
- **Default sorting:** Time in queue
- **Sort order:** Descending 

These settings can't be edited.

## <a name="route"></a>Define the criteria to route cases to the appropriate queue

After the queues are created, define the criteria that will be used to route cases to them. These criteria make up the routing rules. Routing rules resemble assessment rules, but they don't result in a decision. Instead, they result in a routing action. Although each queue can have multiple cases, each case can be routed to only one queue.

After cases pass through the routing rules, there is a five-minute hold before they appear in the appropriate queue. During this time, the cases are updated with supplementary events. If a supplementary event that has any **statusType** value is received through the **purchaseStatus** application programming interface (API), the case won't be routed to a queue. In this case, the **statusType** value that is received in the **purchaseStatus** API event will be recorded as the transaction's latest status.

Routing rules can be created in either a visual editor or a code editor. In the code editor, you can create routing rules by using the Fraud Protection language. For more information, see [Language reference guide](fpl-lang-ref.md).

Follow these steps to create a routing rule.

1. In the left navigation pane, select **Case management** \> **Routing rules**, and select **New rule**.
2. To add an top-level condition that can be applied to the rule set, add it under the condition segment. For example, you might want the rule set to be run for a specific product category.
3. Select **Clause** to add a new clause.
5. In the drop-down list, select the queue to route the cases to.
6. Define the routing criteria by using the drop-down lists for attributes and operators and providing the desired values.
7. To switch to the code editor, select **Code view** in the upper right of the clause.
8. Use the command **RouteTo Queue("\<Queue name\>") WHEN \<Condition\>**. The following example shows the code view for routing transactions where the total amount is more than 1,000 to a **High Value Orders** queue.

    ```
    ROUTETO Queue("High Value Orders")
    WHEN @"purchase.request.totalAmount" > 1000 
    ```

> [!NOTE]
> The routing rules that you create by using the visual editor are translated to the code view when you switch to the code editor. However, after you edit the rules by using the code view, you can't switch back to the visual view.

To customize the order of execution for routing rules, drag the routing rules to define which rules must be executed first. When you've finished, select **Save** on the **Routing rules** page.
