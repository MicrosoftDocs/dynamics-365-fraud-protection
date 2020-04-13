---
author: yvonnedeq
description: This topic explains how you can use Microsoft Dynamics 365 Fraud Protection to support your customers.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 4/02/2020

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

**To display a customer's transactions:**

1. In the left navigation, click **Purchase protection** and then click **Support**.
2. Enter criteria in the **Search** box to locate detailed information on the customer's transactions.

These are the available search methods:

- **User ID** - The unique ID assigned to the user.
- **User email address**.
- **Purchase ID** – The unique ID of a purchase that is sent to Fraud Protection for risk evaluation.
- **Payment instrument ID** – The unique hash of a payment method that is associated with a transaction that is sent to Fraud Protection.

### Search transactions

A search on the customer's email address or the payment instrument ID might return multiple transactions. Select one of the transactions in the search results to view expanded information in the following areas:

- **Financial snapshot** – This area summarizes the history of the customer's spending, transactions, chargebacks, and refunds, if there is any history. This summary can highlight activities that fall outside typical patterns, such as a recent spike in spending, or an unusual number of transactions or chargebacks.
- **Transaction history** – This area identifies individual transactions and highlights their key properties.
- **Transaction details** – This area shows details about individual transactions, such as the payment method, the device that was used, and the originating IP address. 
- **Risk information** provides additional details such as the specific risk score.
- **Line items** – This area itemizes everything that was purchased during the selected transaction. It shows the prices, and applicable taxes and fees.
- **Transaction map** – This area lets you see the shipping address and billing address in relation to each other. Select one of the addresses to center it on the map. If the addresses match, the pins for the two addresses will overlap.

By evaluating the results in these areas, fraud investigators can gain insights into the legitimacy of a transaction and determine the appropriate type of resolution.

## View account information

Select one of the transactions in the sSearch results to view expanded information in the following areas:

- **Account Summary** – A summary of the history of the customer's spending, transactions, chargebacks, and refunds, if there is any history. This summary is aggregated over the last day as well as the last month.
- **Payment Instruments** – A customer's payment instruments by issuer-last four digits. You can use this area to block individual payment instruments associated with a given customer.
- **Transactions** – Details about individual transactions, such as the payment method, the device that was used, and the originating IP address. 
- **Risk information** - This provides additional details such as the specific risk score.
- **Activity Log** – This area captures any changes made to the customer as they were added to the safe/block/watch list. You can use this table to identify who made the changes as well as why and when the status of this customer was updated.

### Add a customer account

When you add a customer to a list, you must specify an expiry date and enter any comments that will be helpful to future reviewers of this case. You can view this information at any time in the activity log. The log also keeps a record of the agent who made each change. Fraud Protection will automatically remove the customer from the list after the expiry date passes.

### Delete a list entry

To delete an entry in a list, select the payment instrument or user status and click **Remove**.

## Unblock a customer

After you review a transaction and determine a course of action, return to the **Accounts** page to resolve the customer's support issue. On the **Accounts** page, you can add a customer or payment instrument to the **Safe list**, the **Watch list**, or the **Block list**. By default, Fraud Protection accepts users on the **Safe list** and rejects users on the **Block list**.

**To update a customer's status:**

1. Open the **Rules** management page and edit the **Default Support Rule**.

    You can also create a rule to identify a course of action for users with a status of **Watch**.

1. Click the **Edit** icon next to the status of your user or payment instrument, and then select the reason for your change.

