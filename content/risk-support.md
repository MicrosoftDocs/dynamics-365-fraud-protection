---
author: jegrif
description: This topic explains how you can use Microsoft Dynamics 365 Fraud Protection to support your customers.
ms.author: v-jegrif
ms.service: fraud-protection
ms.date: 04/22/2019

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin

title: Support your customers
---

# Support your customers

Risk support in Microsoft Dynamics 365 Fraud Protection lets your agents evaluate customer escalations, unblock customers whose purchase attempts are being incorrectly declined, and block future purchases from suspicious users, as appropriate. Your fraud investigators can search and investigate the history of your customers' past transactions with your business. Therefore, they can provide faster turnaround for decisions.

## Search and investigate

In the navigation, under **Risk decisioning**, select **Risk support**. Then search for transactions to get detailed information and see the reasons behind the risk decisions that Dynamics 365 Fraud Protection has made.

Here are the available search methods:

- **User email address**
- **Purchase ID** – The unique ID of a purchase that is sent to Dynamics 365 Fraud Protection for risk evaluation
- **Payment instrument ID** – The unique hash of a payment method that is associated with a transaction that is sent to Dynamics 365 Fraud Protection

A search on the customer's email address or the payment instrument ID might return multiple transactions. Select one of the transactions in the search results to view expanded information in the following areas:

- **Financial snapshot** – This area summarizes the history of the customer's spending, transactions, chargebacks, and refunds, if there is any history. This summary can highlight activities that fall outside typical patterns, such as a recent spike in spending, or an unusual number of transactions or chargebacks.
- **Transaction history** – This area identifies individual transactions and highlights their key properties, such as the results of risk decisions that have been made in Dynamics 365 Fraud Protection.
- **Transaction details** – This area shows details about individual transactions, such as the payment method, the device that was used, and the originating IP address. **Risk information** provides additional details about the risk decision, such as the specific score.
- **Line items** – This area itemizes everything that was purchased during the selected transaction. It shows the prices, and applicable taxes and fees.
- **Transaction map** – This area lets you see the shipping address and billing address in relation to each other. Select one of the addresses to center it on the map. If the addresses match, the pins for the two addresses will overlap.

By evaluating the results in these areas, fraud investigators can gain insights into the legitimacy of a transaction and determine the appropriate type of resolution.

## Unblock customers

After a transaction has been reviewed, and a course of action has been determined, use **Actions** to resolve the customer's support issue.

From here, you can add a customer or payment instrument to either the Safe list or the Block list. Then, on the drop-down menu, select the reason for your choice.

If you add a customer to a list, you must specify an expiry date and enter any comments that will be helpful to future reviewers of this case. You can view this information at any time under **Activity log**. The log also keeps a record the agent who made each change.

Note that after an expiry date has passed, Dynamics 365 Fraud Protection will remove the customer from the list. To delete a list entry at any time, select **Remove from lists**.
