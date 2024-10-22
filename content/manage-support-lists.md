---
author: josaw1
description: This article explains how to edit, add, and remove entities in support lists in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Manage support lists

---

# Manage support lists

Support lists are predefined lists that are included in Microsoft Dynamic 365 Fraud Protection to help you get started. There are support lists for each of the following entities. You can assign entities a status of *Safe*, *Block*, or *Watch*.

- **Email address (@"user.email")** – This entity is the email address that is derived from a user.
- **Payment instrument (@"paymentInstrumentList.merchantPaymentInstrumentId")** – This entity is the payment method that is associated with a transaction.
- **IP address (@"deviceContext.ipAddress")** – This entity is the IP address where the payment originates.
- **User ID (@"user.userId")** – This entity is the unique ID that is assigned to the user from a transaction.
- **Device ID (@"deviceContext.externalDeviceId")** – This entity is the device ID that is associated with a transaction.

Support lists can be modified on the **Support** page or the **Lists** page.

To add, remove, or edit entries in support lists from the **Lists** page, you can complete the following procedures on the **Support Lists** page.

## Add an entry to a support list

1. Select a support list, and then select **Edit**.
1. In the text box, enter the information for the new list entry.
1. In the **Status** field, select a status.
1. Optional: Enter values in the **Reason**, **Expiration date**, and **Comments** fields.
1. When you've finished, select **Update**.

## Edit a support list entry

1. Select a support list, and then select **Edit**.
1. In the text box, update the information for an existing entry.

    The current status of the entry is shown below the text box.

1. Optional: Update the **Status**, **Reason**, **Expiration date**, and **Comments** fields.
1. When you've finished, select **Update**.

## Remove a support list entry

1. Select a support list, and then select **Edit**.
1. In the text box, enter the information for an existing entry.

    The current status of the entry is shown below the text box.

1. Select **Remove**.
1. Optional: Enter a value in the **Comments** field.
1. When you've finished, select **Update**.

## Add or remove multiple support list entries

1. Select a support list, and then select **Edit**.
1. Add your multiple entries, one per line.
1. Select a status for the entries, or select **Remove** to remove the entries from the list.
1. Optional: Update the **Reason**, **Expiration date**, and **Comments** fields.
1. When you've finished, select **Update**.

## Preview a support list

To preview a support list, select the list, and then select **Preview**.

> [!NOTE]
> The preview pane shows a maximum of 20 rows.

To view the full support list, select **Download** to download the list, and then open the file in any text editor.

## Download a support list

1. Select the list to download, and then select **Download**.
1. Select the **Download** button in the lower-left corner of the browser window to view the list.

To download multiple support lists, select the lists, and then select **Download**. The files are downloaded as a zip file.

## Additional resources

[Lists overview](lists-overview.md)

[Manage custom lists](lists.md)
