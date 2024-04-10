---
author: josaw1
description: This article explains how to work with case management as an administrator in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - developer
title: Case management for administrators
ms.custom:
---

# Case management for administrators

This article explains how to work with case management as an administrator in Microsoft Dynamics 365 Fraud Protection.

To complete administrator-specific tasks in case management for Fraud Protection, you must be assigned one of the following roles:

- **Product admin**
- **All areas administrator**
- **All areas editor**
- **Manual review fraud manager**
- **PSP administrator** (available only in payment service provider \[PSP\] environments)
- **Fraud manager** (available only in PSP environments)
- **Fraud supervisor** (available only in PSP environments)

If you're assigned one of these roles, you can complete the following tasks:

- [Define cases for manual review agents](#define-cases-for-manual-review-agents)
- [Create queues to store cases](#create-queues-to-store-cases)
- [Define the criteria to route cases to the appropriate queue](#define-the-criteria-to-route-cases-to-the-appropriate-queue)
- [View the case management report dashboard](#view-the-case-management-report-dashboard)

## Define cases for manual review agents

You can define the criteria that specific purchase transactions must meet to qualify for manual review. You can create assessment rules that generate a **Review()** decision as output. For more information about how to create these rules, see [Manage rules](rules.md). You can use any criteria that meet your business requirements.

The following example shows all transactions that must be selected for review. The risk score of the transactions is more than 600, and the user's country or region is **US**.

```
RETURN Review()
WHEN @"riskScore" > 600 and @"user.country" == "US"
```

## Create queues to store cases

You can use queues to organize purchase transactions that the assessment rules mark for review. Transactions that appear in the case management queues are referred to as *cases*. You can create up to 29 queues for each environment.

Follow these steps to create a queue.

1. In the left navigation pane, select **Case management \> Queues**, and then select **New queue**.
1. Select the assessment type.
1. Enter a name that will help you identify the purpose of the queue.
1. Enter a description that explains the types of cases that are stored in this queue.
1. Select your preference for the review sequence. If you select **Unrestricted queue**, you can review any case in the queue in any order. If you select **Restricted queue**, you must review cases in a predefined order.
1. Select the default sorting and order to define the order in which cases appear and are presented to review agents. In a restricted queue, your selections define the order in which agents can review the cases.
1. Select the time-out duration and default action to define the maximum amount of time that a case can be in the queue without being reviewed and the default action that is taken when that time is reached.
1. You can also assign this queue to a specific set of Microsoft Entra users and groups by adding them to the queue. When users go to their **Case management \> Queues** page from the left nav, they will see all the queues assigned to them. The “Queues assigned to me” filter will be selected by default. The filter can help users to focus and work on the queues that are assigned to them. 
The users can always view all the available queues by applying the “All queues” filter in the Queues page.  

You can edit or delete any queue that you've created. You can also add/remove the assigned users and groups from the queue.To edit the name of a queue or delete a queue, remove the routing rules that have a dependency on the queue. For more information about routing rules, see the next section.

All your environments have a system-created queue that is named **General**. Cases that don't qualify to be routed to a specific queue are routed to the **General** queue. The **General** queue has the following settings:

- **Timeout:** 24 hours 
- **Default action:** Approve
- **Default sorting:** Time in queue
- **Sort order:** Descending 

These settings can't be edited.

## Define the criteria to route cases to the appropriate queue

After the queues are created, define the criteria that will be used to route cases to them. These criteria make up the routing rules. Routing rules resemble assessment rules, but they don't result in a decision. Instead, they result in a routing action. Although each queue can have multiple cases, each case can be routed to only one queue. You can write multiple routing rules for the same queue.

After cases pass through the routing rules, there's a five-minute hold before they appear in the appropriate queue. During this time, the cases are updated with supplementary events. If a supplementary event that has any **statusType** value is received through the **purchaseStatus** application programming interface (API), the case won't be routed to a queue. In this case, the **statusType** value that is received in the **purchaseStatus** API event will be recorded as the transaction's latest status.

Routing rules can be created in either a visual editor or a code editor. In the code editor, you can create routing rules by using the Fraud Protection language. For more information, see [Language reference guide](fpl-lang-ref.md).

Follow these steps to create a routing rule.

1. In the left navigation pane, select **Case management \> Routing rules**, and then select **New rule**.
1. Select the relevant assessment type.
1. To add a top-level condition that can be applied to the rule set, add it under the condition segment. For example, you might want the rule set to be run for a specific product category.
1. Select **New clause** to define a new clause for the routing rule.
1. In the drop-down list, select the queue to route the cases to.
1. Define the routing criteria by using the drop-down lists for attributes and operators and providing the desired values.
1. To switch to the code editor, select **Code view** in the upper right of the clause.
1. Use the command **RouteTo Queue("\<Queue name\>") WHEN \<Condition\>**. The following example shows the code view for the command to route transactions where the total amount is more than 1,000 to a **High Value Orders** queue.

    ```
    ROUTETO Queue("High Value Orders")
    WHEN @"purchase.request.totalAmount" > 1000 
    ```

> [!NOTE]
> The routing rules that you create by using the visual editor are translated to the code view when you switch to the code editor. However, after you edit the rules by using the code editor, you can't switch back to the visual view.

To customize the order of execution for routing rules, drag the routing rules to define which rules must be executed first. When you've finished, select **Save** on the **Routing rules** page.

## View the case management report dashboard

Case management administrators have access to view the case management report dashboard. This dashboard lets managers analyze the queue and agent performance. The case management report is updated every 24 hours. You can select the assessment name, queue name, and agent name on the drop-down menu, and set the date range. The report shows the performance of several key metrics over daily, weekly, and monthly periods. To review specific cases, you can use the search feature to search by case management-specific attributes such as **Queue name**, **Agent name**, **Review decision**, and **Reason and Review notes**.
