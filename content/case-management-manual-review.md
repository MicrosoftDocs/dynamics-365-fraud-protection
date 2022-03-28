---
author: josaw1
description: This topic provides information about completing manual reviews in Case management for Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/28/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Case management for manual reviewers
ms.custom:
---

# Case management for manual reviewers

To complete a manual review of a case in case management, you must be assigned one of the following roles:

- Manual review agent
- All areas of Administrator
- All areas of Editor
- PSP Administrator
- Fraud manager
- Fraud supervisor

## View cases in a queue

In Dynamics 365 Fraud Protection Case management, you can view all the cases you have access to in a particular queue. To view cases in queue, select **View cases** on the queue tile. All the cases that are pending review are listed in the top grid, and all the cases that are currently in review are listed in the bottom grid. 

You can also select the Purchase ID of a case and view the details of the transaction whether it's under review by another agent.

## Review the case and linked transactions

You can start a review of a case in multiple ways. 

  - Select **Start review** on the tile of the queue. 
  - If you are viewing the cases in a queue, you can select **Start review** in the top right of **Pending review** grid. 
  - Select the Purchase ID of a case in the queue to view the details of the transaction. You will have the option to start the review from the **Transaction details** page. Additionally, if the queue you are viewing allows for unrestricted processing, you can hover over the Purchase ID of any case in the **Pending review** grid and select **Start review**.  

After you select **Start review**, the **Transaction review** page opens with categorized details of the transaction. To get the raw data sent to DFP for that transaction, select **JSON view** in the top right corner of the **Transaction review** page. On the **Link analysis** tab, you can view other transactions that are linked to the case you are reviewing. In link analysis, you can choose one or more attributes to trace the linkage. Use the drop-down menu to filter for transactions that match all or any of the attributes selected. Select **Column options** to customize the fields you want to view to help with your decision. You can also export the results of linked transactions for additional analysis.

## Decisions and notes for a case

When you have reviewed the necessary details of the transaction and are ready to make a decision on the case, select **Approve** or **Reject** on the top left corner of the **Transaction review** page. Depending on what you select, the subsequent modal offers a list of reason codes that you can select from to support your decision. You can also add your notes for record keeping about the transaction. These notes are associated with the transaction, Going forward, any user who searches for and sees the transaction will be able to see the notes you add.

> [!NOTE]
> The **Transaction review** page will monitor and provide an alert if you have been reviewing a case for 30 minutes. You can choose to extend the time for another 30 minutes if you are still reviewing the case, by selecting **Continue reviewing** on the message. If no action is taken on the message, the case will be sent back to the queue and made available for another agent to review.

## Add notes without reviewing a case

If you are unable to complete a review of the case, you can leave notes for the next reviewer. 
1. To add a note to the case, select **Notes** in the top right corner of the **Transaction review** page.
2. Select **+Note** to add a note which will be associated with the transaction. This note can be viewed by anyone who views the transaction in future. 
3. Select **Send back to queue** to send the case back to the queue and make it available for another agent to review.

