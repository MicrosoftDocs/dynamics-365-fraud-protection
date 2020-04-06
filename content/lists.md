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
title: Managing lists

---
# Managing lists

Custom lists provide you with a flexible way to upload and access organized data within Dynamics 365 Fraud Protection. You can create any number of custom lists containing data specific to your business needs. For example, you can create a list containing a set of email addresses, IP addresses, or product IDs. These lists can then be referenced within a rule (link) in order to help you execute your business logic and fraud strategy at scale.

> [!NOTE]
> Lists do not display in an INT environment.

## Use lists to execute business logic

Rules (link) are used to define custom logic in order to automate decisions in your business. You may reference any custom list within a rule. For example, you may create a list of email addresses which are considered to be risky based on past transactions, as well as a list for those which are considered to be safe

|Risky email addresses |
|--------------|
|Kayla@contoso.com |
|Jamie@bellowscollege.com |
|Marie@atatum.com |

|Safe email addresses |
|--------------|
|Camille@fabrikam.com |
|sarah@gmail.com |
|Miguel@proseware.com |
|Tyler@contoso.com |

You can then configure a rule such that login attempts using an email on the "Risky email addresses" list is rejected, while those using an email on the "Safe email addresses" list are approved. 

### Single and multiple-column lists

As in the example above, you can create lists with a single column of values, representing some key (for example, email address). However, you can also also use additional columns to represent a set of values relevant to that key. For example, instead of having one single-column list containing "Safe email addresses" and another single column-list containing "Risky email addresses", you can combine this information into a single multi-column list, as shown below.

|Email address|Status|
|--------------|--------------|
|Kayla@contoso.com |Risky|
|Jamie@bellowscollege.com|Risky|
|Marie@atatum.com|Risky|
|Camille@fabrikam.com|Safe|
|Miguel@proseware.com |Safe |
|Tyler@contoso.com |Safe |

You can then configure your rule such that all login attempts using an email on this list with the status "Risky" are rejected, while those using an email with the status "Safe" are approved.

In addition to utilizing multi-column lists to combine safe and block lists, you can also use multi-column lists to specify the unique levels of risk associated with a set of products, emails, or countries. For example, if certain product types present different levels of risk to your business, you may want to make decisions for these products differently. Specifically, you may want to evaluate each product against its own score threshold (link to scoring). To do this, you first need to create a list to represent this information, such as in the example below. 

|Product ID    |Score threshold|
|--------------|--------------|
|Digital    |500|
|Consumable    |600|
|Physical    |750|

You can then configure a rule that enforces that transactions involving products of each type are rejected when they are assigned a risk score (link) greater than the specified threshold. Learn more (link) about how to create effective rules to customize your business logic. 

## Create a custom list

To create a list in Fraud Protection, you must first create and save the list as a CSV file on your local machine. The file must meet the follwing requirements.
- Be in CSV format.
-	Contain unique headers for every column.
-	Be less than 20mb.

When you are ready to upload the list to Fraud Protection, go to the **Lists** page and follow the steps below.
1. Click **New list**. 
1. Click **Browse** to locate the file. Select the file, then click **Open**. 

    Fraud Protection opens a preview of the file for you to review. The preview contains a maximum of 20 rows. 
    
1. To upload the file, click **Continue**. To upload a different file, click **Cancel** and repeat Step 2. 
1. Add a name and description that will make it easy for your team to know how to use the list. The name can't be changed after this step. 

1. Click **Create**. Because of caching, it may take up to two minutes for the list to become active. 

## Update a list

> [!NOTE]
>  Support lists can't be updated from the **Lists** page. Support lists can only be modified through the **Support** page. 

#### To update the contents of a Custom List in DFP:
1. Select the list you want to update, and click **Edit**. 
1. If you have the most up to date version of the list saved on your computer, open this file. Otherwise, press **Download** and open the downloaded file. 
1. Make all edits to the file directly. When you are finished editing, save the file to your machine. 
1. In the DFP **Edit List** panel, click **Browse** to locate the file. Select the updated file from Step 3 and click **Open**. 
    
    DFP opens a preview of the file for you to review. Note that this preview contains a maximum of 20 rows. 

1. To upload this file, click **Continue**. (To upload a different file, click Cancel and repeat Step 4). 
1.	Click **Update**. Note that due to caching, the list may take up to two minutes to update. 


## Manage lists

#### To delete a list:

1. Select the list you want to delete and click **Delete** in the command bar at the top. 

   Note that any rules which use this list will no longer work. 
   
1. To confirm you still want to delete the list from DFP, click **Delete** in the confirmation dialog.

#### To download a list:

- Select the list you want to download and click **Download** in the command bar at the top.

    When the list has been downloaded, an Excel icon displays in the lower left corner of the window.

1. Click the Excel icon on the lower left of the window to open the file.

#### To search for a list:

- Locate the **Search** box on the upper right, and type in a keyword. 

    This will search all List names and descriptions, and filter the results accordingly. 

- To remove the filter, delete the keyword from the **Search** box, or press the **x** to the right.
