---
author: josaw1
description: This topic provides an overview of what support and custom lists are, and how to manage information on lists in Dynamics 365 Fraud Protection.  
ms.author: josaw
ms.date: 09/24/2021
ms.topic: how-to
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Lists overview

---

# Lists overview

Lists help you manage information that you use to fight fraud and enforce business policies. For example, you can create a list to track payment instruments that you consider risky or user email addresses that you consider safe. You can then upload the list as a comma-separated values (CSV) file and then reference it in a [rule](rules.md) to help automate decisions. 

In Microsoft Dynamics 365 Fraud Protection, there are two types of list that you can create, custom lists and support lists. 

## Custom lists

Custom lists are created and defined by you. You can upload any number of custom lists and fill them with data that is specific to your business needs or your fraud protection strategy. For example, you can create a custom list that contains email addresses, IP addresses, or product IDs, and additional values that are associated with each entry. 

## Support lists

Support lists are predefined lists included in Dynamic 365 Fraud protection that help you get started. There are support lists for each of the following entities. TYou can assign entities the status of safe, block, or watch.  

- Email address (@"user.email") – This entity is for the email address derived from a user.

- Payment instrument (@"paymentInstrumentList.merchantPaymentInstrumentId") – This entity is the payment method that is associated with a transaction.

- IP address (@"deviceContext.ipAddress") – This entity is the IP address from which the payment originates.

- User ID (@"user.userId") – This entity is the unique ID that is assigned to the user from a transaction.

- Device ID (@"deviceContext.externalDeviceId") – Device ID that is associated with the transaction 

### Manage a support list

Support lists can be modified on the **Support** page or the **Lists** page. 

To add, remove, or edit entries from support lists from Lists page, you can take the following actions in the Support Lists page. 

#### Add a new entry to a support list 

1. Select a support lists, and then select **Edit**. 

1. Enter the information for the list entry in the text box. 

1. Select a **Status**.

1. You have the option to place **Reason**, **Expiration date**, and **Comments**.

1. When you’re finished editing, select **Update**.

#### Edit an existing support list entry

1. Select one of the support lists, and then select **Edit**.  

1. Enter the information for existing entry in the text box. 

1. Existing status for the entry will be displayed below the textbox. 

1. You have the option to update **Status**, **Reason**, **Expiration date**, and **Comments**.  

1. When you’re finished editing, select **Update**. 

#### Remove a support list entry

1. Select a support list, and then select **Edit**.  

1. Enter the information for existing entry in the text box. 

1. Existing status for the entry will be displayed below the textbox. 

1. Select **Remove**. 

1. You have the option to enter **Comments**.  

1. When you’re finished editing, select **Update**.

#### Add or remove multiple support list entries

1. Select a support list, and then select **Edit**.  

1. Copy and paste the list of entries you would like to add or remove.  

1. Select a status for the entries, or select **Remove** to remove the entries from the list. 

1. You have the option to update **Reason**, **Expiration date**, and **Comments**. 

1. When you’re finished editing, select **Update**.

#### Preview a support list

To preview a support list, select the list, and then select **Preview**. 

To view the full support list, select **Download** to download the list, and then open the file in any text editor. 

> [!NOTE]
> The preview pane displays a maximum of 20 rows. 

#### Download a support list

To download a support list, do the following.
1. Select the list you want to download, and select **Download**.
1. Select the download button in the lower-left corner of the browser window to view the list. 

To download multiple support lists, select the lists, and then select **Download**. The files are downloaded as a zip file. 






