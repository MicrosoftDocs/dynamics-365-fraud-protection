---
author: jegrif
description: Support your customers
ms.author: v-jegrif
ms.service: crm-online
ms.date: 03/01/2019

ms.topic: conceptual
title: Support your customers
---


# Support your customers

Risk support within Microsoft Dynamics 365 Fraud Protection enables your agents to evaluate customer escalations, unblock customers whose purchase attempts are being improperly declined, and block future purchases from suspicious users as appropriate. Your fraud investigators can search and investigate your customers’ past transactional history with your business, providing an accelerated turnaround for decisions.

## Search and investigate

Select **Risk support** under **Risk decisioning** in the navigation, then search for transactions to get detailed information and see the reasoning behind Dynamics 365 Fraud Protection’s risk decisions.

The available search methods include:

- User email  
- Purchase ID (unique ID of a purchase sent to Dynamics 365 Fraud Protection for risk evaluation) 
- Payment instrument ID (unique hash of a payment method associated with a transaction sent to Dynamics 365 Fraud Protection) 

Searching by a customer's email address or payment instrument may reveal multiple transactions. Select any of them for expanded information in the following areas:

- **Financial snapshot** summarizes the customer's spending, transaction, chargeback, and refund history, if any. This breakdown can highlight activities that fall outside typical patterns, such as a recent spike in spending or an unusual number of transactions or chargebacks. 
- **Transaction history** identifies individual transactions and highlights their key properties, including the results of risk decisions made in Dynamics 365 Fraud Protection. 
- **Transaction details** shows specifics about individual transactions, like the payment method, the device used, the originating IP address, and more. **Risk information** provides additional details about the risk decision, including the specific score. 
- **Line items** itemizes everything purchased during the selected transaction, the price, and applicable taxes and fees. 
- The **Transaction map** enables you to see the shipping address and billing address in relation to each other. Select either address to center it on the map. If the addresses match, the pins will overlap.

When evaluated by a fraud investigator, these results can provide insights into the legitimacy of a transaction and help indicate what type of resolution is appropriate.

## Unblock customers

Once a transaction has been reviewed and a course of action has been determined, use **Actions** to resolve the customer's support issue.

From here, a customer or payment instrument can be placed on the **Safe list** or **Block list**. Choose the appropriate reason for your  choice from the provided dropdown.

Adding a customer to a list requires an expiry date and any comments that will be helpful to future reviewers of this case. View these at any time under **Activity log**. The log will also keep record of which agent made each change.

Note that after an expiry date has passed, Dynamics 365 Fraud Protection will remove the customer from the list. To delete a list entry at any time, select **Remove from lists**. 
