---
author: jegrif
description: Support your customers
ms.author: v-jegrif
ms.date: 03/01/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Support your customers
---


# Support your customers

Customer support within Microsoft Dynamics 365 Fraud Protection enables your agents to evaluate customer escalations, unblock customers whose purchase attempts are being improperly declined, and block suspicious purchases as appropriate. Your fraud investigators can search and investigate your customers’ past transactional history with your business, providing an accelerated turnaround for decisions. 

## Search and investigate

Select **Support dashboard** and search for transactions to get detailed information and see the reasoning behind Dynamics 365 Fraud Protection’s risk decisions.

The available search methods include:

- User.Email 
- Purchase.PurchaseID 
- PaymentInstrument.PaymentInstrumentID

Searching by a customer's email address or payment instrument may reveal multiple transactions. Select any of them for expanded information in the following areas:

- **Financial snapshot** summarizes the customer's spending, transaction, chargeback, and refund history, if any. This breakdown highlights activities that fall outside typical patterns, such as a recent spike in spending or an unusual number of transactions or chargebacks. 
- **Transaction history** identifies individual transactions and highlights their key properties, including the results of risk decisions made in Dynamics 365 Fraud Protection. 
- **Transaction details** show specifics about individual transactions, like the payment method, the device used, the originating IP address, and more. **Risk information** provides additional details about the risk decision, including the specific score. 
- **Line items** itemizes everything purchased during the selected transaction, the price, and applicable taxes and fees. 
- The **Transaction map** enables you to see the shipping address, billing address, and IP address in relation to each other, and calculates the distance between them. Select any address to center it on the map. If any of the addresses are the same, the pins will overlap.

When evaluated by a fraud investigator, these results can provide insights into the legitimacy of a transaction and help indicate what type of resolution is appropriate.

## Unblock customers

Once a transaction has been reviewed and a course of action has been determined, use **Actions** to resolve the support issue appropriately.

From here, a customer or payment instrument can be placed on the **Safe list** or **Block list**. List assignment can be changed if a decision was determined to be incorrect, an account was rehabilitated, or new suspicious activity occurs.

Adding an entry to a list requires an expiry date and any comments that will be helpful to future reviewers of this case. View these at any time under **Activity log**. After an expiry date has passed, Dynamics 365 Fraud Protection will no longer whitelist or block them based on those lists.

Use **Comment only** to add notes to an entry without changing its status, and **Remove from lists** to delete any previous list assignments. 
