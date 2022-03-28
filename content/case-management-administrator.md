---
author: josaw1
description: This topic provides information about working with Case management as an Administrator.
ms.author: josaw
ms.date: 03/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management for Administrators
ms.custom:
---

# Case management for Administrators

To complete administrator-specific tasks in Case management, you must be assigned one of the following roles:

- All areas of Administrator
- All areas of Editor
- PSP administrator
- Fraud Manager
- Fraud Supervisor

If you are assigned one of the roles, you can complete the following tasks:

- [Define cases for manual review agents](#review)
- [Create organization methods for storing cases](#store)
- [Define the criteria to route cases to the appropriate queue](#route)

## <a name="review"></a> Define cases for manual review agents
To enable purchase transactions for manual review, define the criteria which qualifies certain transactions for manual review. You can create assessment rules which then out put a **Review()** decision. For more information about creating the rules, see [Manage rules](rules.md). You can use any criteria that meets your business needs.

The following example shows all transactions to be selected for review. The transactions have a score greater than **600** and the user country is **US**. 

  ```
   RETURN Review()
   WHEN @"riskScore" > 600 and @"user.country" == "US"

  ```

## <a name="store"></a> Create organization methods for storing cases

You can use queues to organize purchase transactions that are marked for review by the assessment rules. Transactions that appear in the case management queues are referred to as **cases**. You can create up to 29 queues for each environment. 

Complete the following steps to create a queue.

1. In the left navigation pane, select **Case management** > **Queues** and select **+ New Queue**.
2. Give the queue name that helps you identify the purpose of the queue.
3. Enter a description that explains the type of cases stored in this queue.
4. Choose the review sequence preference. An **Unrestricted queue** lets you review any case in the queue in any order. For a **Restricted queue**, you must review cases in a predefined order.
5. Select the default sorting and order to define the order in which cases are displayed and presented to review agents. In a restricted queue, this selection defines the order of cases that agents can review. 
6. Select the time out duration and default action to define the maximum amount of time a case can be in the queue without being reviewed and the default action that is taken when that maximum time duration is met.

You can edit or delete any queue you have created. To edit the name of a queue or delete a queue, remove the routing rules that have a dependency on the queue. See the next section for more information about routing rules. 

All your environments will have a system created queue named **General**. Cases that don't qualify to be routed to a specific queue are routed to the **General** queue. Settings for the **General queue** are:

  - Timeout = 24 hours 
  - Default action = Approve
  - Default sorting = Time in queue
  - Sort order = Descending 
 
 These settings can't be edited.   

## <a name ="route"></a> Define the criteria to route cases to the appropriate queue

After the queues are created, define the criteria based on which cases will be routed to these queues. These criteria make up the routing rules, which are similar to assessment rules except that routing rules don't result in a decision. Instead, routing rules result in a routing action. While one queue can have multiple cases, one case can only be routed to one queue.

All cases have a hold of five minutes after passing through the routing rules, to update with supplementary events, before they appear in the respective queue. If a supplementary event is received through the **purchaseStatus** API with any **statusType**, the case will not be routed to aqueue and the **statusType** received in the **purchaseStatus** API event will be recorded as the transaction's latest status. 

Routing rules can be authored through a visual editor or through a code editor. You can author routing rules in code editor using the FraudProtection Language. For more information, see [Language reference guide](fpl-lang-ref.md).

Complete the following steps to create routing rules.

1. On the left navigation page, select **Case management** > **Routing rules** and select **+ New Rule**.
2. To add an uber level condition that can be applied to the rule set, add it under the condition segment. For example, ff you want the rule set to be executed for a particular product category.
3. Select **+ Clause** to add a new clause.
5. From the drop-down list, select the queue to route the cases to.
6. Set the criteria for routing using the drop-down lists for attributes, operators, and supplying the desired value.
7. To switch to code editor, select **Code view** on the top right of the clause. 
8. Use the command **RouteTo Queue(“<Queue name>”) WHEN <Condition>**. The following example shows the code view for routing transactions greater than 1,000 to a **High value orders** queue.

  ```
    ROUTETO Queue("High Value Orders")
    WHEN @"purchase.request.totalAmount" > 1000 
  ```
  
> [!NOTE]
> The routing rules you create using the visual editor are translated to code view when you switch. However, after you edit using the code view, you can't switch back to visual view.  

Routing rules can be customized to set the order of execution by dragging and dropping the routing rules to define which rules must be executed first. After the ordering is complete, on the **Routing rules** page, select **Save**.



