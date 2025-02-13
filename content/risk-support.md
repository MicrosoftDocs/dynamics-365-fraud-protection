---
author: josaw1
description: This article explains how you can use Microsoft Dynamics 365 Fraud Protection to support your customers.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual 
search.audienceType:
  - admin
title: Support your customers with Dynamics 365 Fraud Protection
---

# Support your customers with Dynamics 365 Fraud Protection

[!include[deprecation](includes/deprecation.md)]

Risk support in Microsoft Dynamics 365 Fraud Protection lets your agents evaluate customer escalations, unblock customers whose purchase attempts are being incorrectly declined, and block future purchases from suspicious users, as appropriate. Your fraud investigators can search and investigate the history of your customers' past transactions with your business. Therefore, they can provide faster turnaround for decisions.

If your Fraud Protection instance has multiple environments, you can access **Risk support** in a specific environment by using the environment switcher. You can only search for transactions in the same environment. 

## Search and investigate

To show a customer's transactions, follow these steps.

1. In the left navigation, select **Purchase**.
2. On the **Support** tab, in the **Search** field, enter criteria to find detailed information about the customer's transactions.

Four search methods are available:

- **User ID** – Search by the unique ID that is assigned to the user.
- **User email address** – Search by the user's email address.
- **Purchase ID** – Search by the unique ID of a purchase that is sent to Fraud Protection for risk evaluation.
- **Payment instrument ID** – Search by the unique hash of a payment method that is associated with a transaction that is sent to Fraud Protection.

### Search transactions

A search on the customer's email address or the payment instrument ID might return multiple transactions. Select one of the transactions in the search results to view expanded information in the following areas:

- **Financial snapshot** – This area summarizes the history of the customer's spending, transactions, chargebacks, and refunds, if there is any history. This summary can highlight activities that fall outside typical patterns, such as a recent spike in spending, or an unusual number of transactions or chargebacks.
- **Transaction history** – This area identifies individual transactions and highlights their key properties.
- **Transaction details** – This area shows details about individual transactions, such as the payment method, the device that was used, and the originating IP address.
- **Risk information** – This area provides additional details, such as the risk score.
- **Line items** – This area itemizes everything that was purchased during the selected transaction. It shows the prices, and applicable taxes and fees.
- **Transaction map** – This area lets you see the shipping address and billing address in relation to each other. Select one of the addresses to center it on the map. If the addresses match, the pins for the two addresses will overlap.

By evaluating the results in these areas, fraud investigators can gain insights into the legitimacy of a transaction and determine the appropriate type of resolution.

## View account information

Select one of the transactions in the search results to view expanded information in the following areas:

- **Account Summary** – A summary of the history of the customer's spending, transactions, chargebacks, and refunds, if there is any history. This summary is aggregated over the last day and also over the last month.
- **Payment Instruments** – A customer's payment instruments by the issuer's last four digits. You can use this area to block individual payment instruments that are associated with a specific customer.
- **Transactions** – Details about individual transactions, such as the payment method, the device that was used, and the originating IP address.
- **Risk information** – Additional details, such as the risk score.
- **Activity Log** – This area captures any changes that were made to the customer when that customer was added to the safe list, watch list, or block list. You can use the grid in this area to identify who made the changes, and why and when the status of the customer was updated.

### Add a customer account

When you add a customer to a list, you must specify an expiry date and enter any comments that might be helpful to future reviewers of this case. You can view this information at any time in the activity log. The activity log also keeps a record of the agent who made each change. After the expiry date is passed, Fraud Protection will automatically remove the customer from the list.

### Delete a list entry

To delete an entry in a list, select the payment instrument or user status, and then select **Remove**.

## Unblock a customer

After you review a transaction and determine a course of action, return to the **Accounts** page to resolve the customer's support issue. On the **Accounts** page, you can add a customer or payment instrument to the safe list, the watch list, or the block list. By default, Fraud Protection accepts users who appear in the safe list and rejects users who appear in the block list.

To update a customer's status, follow these steps.

1. On the **Rules** management page, edit the default support rule.

    You can also create a rule to identify a course of action for users who have a status of **Watch**.

1. Select the **Edit** button next to the status of the user or payment instrument, and then select the reason for your change.


[!INCLUDE[footer-include](includes/footer-banner.md)]
