---
author: yvonnedeq
description: This topic provides details on how to use lists.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 04/03/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Manage lists

---
# Manage lists

## Overview

Lists provide you with a flexible way to upload and access organized data within Dynamics 365 Fraud Protection. You can reference any list in  a [rule](rules.md) in order to help you execute your business logic and fraud strategy at scale.

The Lists page has two tabs separating the two types of Lists you can create: **Custom lists** and **Support lists**. 

## Custom lists

Custom lists are created and defined by you. You can upload any number of custom lists and fill these lists with data specific to your business needs or fraud protection strategy. For example, you can create a list containing a set of email addresses, IP addresses, or product IDs, as well as additional values associated with each entry. 

## Support lists

Support lists are system-configured lists of emails and payment instruments with a *safe*, *block*, or *watch* status, as well as an associated expiration date for each entry. While these lists can be viewed and downloaded from the Lists page, they can only be modified through the [Support page](risk-support.md).

> [!NOTE]
> You cannot view or create lists in the INT environment. You must use the PROD environment.


## Using lists 

[Rules](rules.md) are used to define custom logic in order to automate decisions in your business. To help you define this logic, you can reference any list in a rule. For example, you can create a list of email addresses which are considered to be risky, and a separate list for those which are considered to be safe. You can then configure a rule so that login attempts using an email on the *Risky Emails* list is rejected, while those using an email on the *Safe Emails* list are approved. 

### Single and multiple-column lists

The example above results in two separate lists, *Risky Emails* and *Safe Emails*, with a single column of values representing a key (in this case, email address). 

<table>
<tr><td>

|Risky emails|
|--------------|
|Kayla@contoso.com |
|Jamie@bellowscollege.com |
|Marie@atatum.com |

</td><td>

|Safe emails |
|--------------|
|Camille@fabrikam.com |
|Miguel@proseware.com |
|Tyler@contoso.com |

</td></tr> </table>

However, you can use additional columns to  hold values relevant to that key. For example, instead of the two separate lists above, you can combine this information into a single multi-column list, as shown below.

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

You can then configure your rule so that all login attempts using an email on this list with the status *Risky* are rejected, while those using an email with the status *Safe* are approved.

In addition to using multi-column lists to combine safe and block lists, you can also use multi-column lists to specify the unique levels of risk associated with a set of products, emails, or countries. For example, if certain product types present different levels of risk to your business, you can make decisions for these products differently. Specifically, you can evaluate each product against its own [score threshold] (scorecard.md). To do this, you must first create a list to represent this information, as shown in the example below. 

|Product ID    |Score threshold|
|--------------|--------------|
|Digital    |500|
|Consumable    |600|
|Physical    |750|

You can then configure a rule that enforces that transactions are rejected when they have a [risk score](ap-scorecard.md#risk-model-score) above the specified threshold for that product type. For information on about how to create effective rules to customize your business logic, see [Rules](rules.md). 

## Upload a list

To create a custom list in Fraud Protection, you must first create and save the list as a CSV file on your local machine. The file must meet the following requirements.
- Must be in CSV UTF-8 (comma delimited) format (*.csv).
-	Must contain unique headers for every column.
-	Must be under the maximum file size of 20 megabytes (MB).

**To upload a list to Fraud Protection:**

1. Click **New list**. 
1. Click **Browse** to locate the file. Select the file, then click **Open**. 

    Fraud Protection opens a preview of the file for you to review. The preview contains a maximum of 20 rows. 
    
1. To upload the file, click **Continue**. To upload a different file, click **Cancel** and repeat step 2. 
1. Add a name and description that will make it easy for your team to identify and use the list. A list name cannot be changed after this step. 
1. Click **Create**.

    Because of caching, it may take up to two minutes for the list to become active. 

## Update a list

You can update a custom list at any time to include new information or change existing information. You can change the description of a list, but you cannot change its name.

> [!NOTE]
>  You cannot update support lists from the Fraud Protection **Lists** page. You can only modify them through the [Support page](risk-support.md). 

**To update the contents of a custom list in Fraud Protection:**

1. If you have the most up to date version of the list saved on your computer, open this file. Otherwise, select the list you want to update and click **Download** to get the most up to date version.
1. Make all your edits to the file directly. When you have finished editing, save the file to your machine. 
1. Select the list you want to update, and then click **Edit**.
1. Click **Browse** to locate the file. Select the file you just updated, and then click **Open**.
    
    Fraud Protection opens a preview of the file for you to review. The preview contains a maximum of 20 rows. 

1. To upload the file, click **Continue** and then click **Update**. 
  
  Because of caching, it may take up to two minutes for the list to become active. 

**To update the description of a custom list in Fraud Protection:**
1.	Select the list you want to update, and then click **Edit**. 
1.	Update the text in the **Description** field, and then click **Update**.

## Delete a list

When you delete a list, any rules which use this list will no longer work.

- To delete a list, select the list, and then click **Delete**.  
   
## Download a list

You can download a list in Fraud Protection and then view it in Microsoft Excel. 

- To download a list, select the list you want, and then click **Download**. 
- To open a downloaded list, click the **Excel** icon in the left corner of the Fraud Protection window.

## Search for a list

When you search for a list, all list names and descriptions are searched, and the results are filtered accordingly. 

- To search for a list, type a keyword into the **Search** box on the upper right side of the **Lists** page. 
- To remove the filter, delete the keyword from the **Search** box, or click the **x** to the right.

## Preview a list
You can preview a file in Fraud Protection. The preview contains a maximum of 20 rows. 

- To preview a list, select the list you want and click **Preview**. 
- To view the full list, click **Download** to download the list and then open the file in Excel.

