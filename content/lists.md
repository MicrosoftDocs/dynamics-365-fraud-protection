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

Lists allow you to upload and access organized data in Dynamics 365 Fraud Protection. You can reference any list in a [rule](rules.md) to help execute your business logic and fraud strategy.

The **Lists** page has two tabs separating the two types of lists you can create: **Custom lists** and **Support lists**. 

> [!NOTE]
> You cannot view or create lists in the INT environment. You must use the PROD environment.

### Custom lists

Custom lists are created and defined by you. You can upload any number of custom lists and fill these lists with data specific to your business needs or fraud protection strategy. For example, you can create a list containing email addresses, IP addresses, or product IDs, as well as additional values associated with each entry. 

### Support lists

Support lists are system-defined lists of emails and payment instruments with a *safe*, *block*, or *watch* status, as well as an associated expiration date for each entry. While these lists can be viewed and downloaded from the Lists page, they can only be modified through the [Support page](risk-support.md).

### Required list formats

To upload a custom list in Fraud Protection, you must first create and save the list as a CSV file on your local machine. The file must meet the following requirements:

- It must be in CSV UTF-8 (comma delimited) format (*.csv).
-	It must contain unique headers for every column.
-	It must be under the maximum file size of 20 megabytes (MB).

## Use lists 

[Rules](rules.md) define custom logic that automate business decisions. To help you define this logic, you can leverage any list in a rule. For example, you can create a list of email addresses which are considered to be risky, and a separate list for those which are considered to be safe. You can then configure a rule so that login attempts using an email on the *Risky Emails* list are rejected, while those using an email on the *Safe Emails* list are approved. 

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

However, you can use additional columns to  hold values relevant to that key. For example, instead of the two separate lists above, you can combine this information into a single multiple-column list, as shown below.

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

You can then configure your rule so that all login attempts using an email on this list with the status *Risky* are rejected, while those using an email with the status *Safe* are approved.

In addition to using multi-column lists to combine safe and block lists, you can also use multi-column lists to specify the unique levels of risk associated with a set of products, emails, or countries. For example, if certain product types present different levels of risk to your business, you can make decisions for these products differently. Specifically, you can evaluate each product against its own score threshold. To do this, you must first create a list to represent this information, as shown in the example below. 

|Product Type    |Score threshold|
|--------------|--------------|
|Digital    |500|
|Consumable    |600|
|Physical    |750|

You can then configure a rule that enforces that transactions are rejected when they have a [risk score](ap-scorecard.md#risk-model-score) above the specified threshold for that product type. For information on about how to create effective rules to customize your business logic, see [Rules](rules.md). 

## Upload a list
You can upload organized data in a list file to Fraud Protection and then reference the list in a [rule](rules.md).

> [!IMPORTANT]
> When working with sensitive personal data or highly regulated data types, take care to upload this data only from a secure network location. This type of data may include:<br><br>- Biometric data, genetic data, or any data related to health. <br>- Personal data revealing racial or ethnic origin or religious views; or <br>- Personal data, which by their nature, are sensitive or privacy, such as data concerning a person’s sexual orientation or philosophical beliefs.<br><br>We recommend that you do not include this type of data in the files that you upload. <br><br>For information on how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](data-upload.md#security-compliance).
 

**To upload a list to Fraud Protection:**

1. Click **New list**. 
1. Click **Browse** to locate the file. Select the file, then click **Open**. 

    Fraud Protection opens a preview of the file for you to review. The preview displays a maximum of 20 rows. 
    
1. To upload the file, click **Continue**. To upload a different file, click **Cancel** and repeat step 2. 
1. Add a name and description that will make it easy for your team to identify and use the list. 

    A list name cannot be changed after this step. 
    
1. Click **Create**.

    Because of caching, it may take up to two minutes for the list to become active. 

## Update a list

You can update a custom list from the **Lists** page at any time to add new information or change existing information. You can change the description of a custom list, but you cannot change its name. 

To modify support lists, use the [Support page](risk-support.md).

**To update the contents of a custom list in Fraud Protection:**

1. If you have the most up to date version of the list saved on your computer, open this file. Otherwise, select the list you want to update and click **Download** to get the most up to date version.
1. Make all your edits to the file directly. When you have finished editing, save the file to your machine. 
1. In the **Lists** management page, select  the list you want to update, and then click **Edit**.
1. Click **Browse** to locate the file. Select the file you just updated, and then click **Open**.
    
    Fraud Protection opens a preview of the file for you to review. The preview displays a maximum of 20 rows. 

1. To upload the file, click **Continue**, and then click **Update**. 
  
  Because of caching, it may take up to two minutes for the list to become active. 

**To update the description of a custom list in Fraud Protection:**
1.	Select the list you want to update, and then click **Edit**. 
1.	Update the text in the **Description** field, and then click **Update**.

## Delete a list

When you delete a list, any rules which use this list will no longer work.

- To delete a list, select the list, and then click **Delete**.  
-	To delete multiple lists, select the lists you want to remove, and then click **Delete**.
   
## Download a list

You can download a list in Fraud Protection and then view it in any text editor. 

- To download a list, select the list you want and click **Download**. Then click the icon in the left corner of the Fraud Protection window to view the list. 

- To download multiple lists, select the lists you want to download, and then click **Download**.

    When you download multiple files, they are downloaded as a zip file.

## Search for a list

When you search for a list, all list names and descriptions are searched, and the results are filtered accordingly. 

- To search for a list, type a keyword into the **Search** box on the upper right side of the **Lists** page. 
- To remove the filter, delete the keyword from the **Search** box, or click the **x** to the right.

## Preview a list
You can preview a list in Fraud Protection. The preview panel displays a maximum of 20 rows. 

- To preview a list, select the list you want, and then click **Preview**. 
- To view the full list, click **Download** to download the list, and then open the file in any text editor.

