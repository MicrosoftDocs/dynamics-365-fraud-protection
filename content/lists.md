---
author: josaw1
description: This article explains how to add, manage, and use custom lists to manage information, fight fraud, and enforce business policies in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/27/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Manage custom CSV lists

---

# Manage custom CSV lists

Custom lists are created and defined by you. You have the ability to create custom lists, utilizing comma-separated value (CSV) files, and populate them with data tailored to your specific business needs or fraud protection strategy. For instance, you can create a custom list that includes email addresses, IP addresses, or product IDs, along with additional values associated with each entry. This approach is recommended when dealing with relatively smaller datasets that do not necessitate real-time updates.

## Format requirements

To upload a custom list in Microsoft Dynamics 365 Fraud Protection, you must first create and save the list as a CSV file on your local computer. The file must meet the following requirements:

- It must be in CSV UTF-8 (comma-delimited) format (\*.csv).
- It must contain a unique header for every column.
- The file size must be less than 20 megabytes (MB).

## Use custom lists

[Rules](rules.md) define custom logic that automates business decisions. To help define this logic, you can take advantage of any list in a rule. For example, you can create one list of email addresses that you consider risky and another list of email addresses that you consider safe. You can then configure a rule so that all sign-in attempts that use an email address in the **Risky Emails** list are rejected, whereas sign-in attempts that use an email address in the **Safe Emails** list are approved.

## Single-column and multicolumn lists

The following example shows two separate lists, **Risky Emails** and **Safe Emails**. In both lists, a single column of values represents a key (in this case, the email address).

| Risky Emails |
|--------------|
| `Kayla@contoso.com` |
| `Jamie@bellowscollege.com` |
| `Marie@atatum.com` |

| Safe Emails |
|-------------|
| `Camille@fabrikam.com` |
| `Miguel@proseware.com` |
| `Tyler@contoso.com` |

However, you can use additional columns to hold values that are relevant to the key. For example, instead of using two separate lists, you can combine the same information into one multicolumn list, as shown here.

| Email address | Status |
|---------------|--------|
| `Kayla@contoso.com` | Risky |
| `Jamie@bellowscollege.com` | Risky |
| `Marie@atatum.com` | Risky |
| `Camille@fabrikam.com` | Safe |
| `Miguel@proseware.com` | Safe |
| `Tyler@contoso.com` | Safe |

You can then configure your rule so that all sign-in attempts that use an email address that appears in this list and has a status of *Risky* are rejected, whereas attempts that use an email address that has a status of *Safe* are approved.

In addition to using multicolumn lists to combine safe and block lists, you can use them to specify the unique levels of risk that are associated with a set of products, email addresses, or countries/regions. For example, if specific product types present different levels of risk to your business, you can make decisions for those products differently. Specifically, you can evaluate each product against its own score threshold. To use this approach, you must first create a list that represents this information, as shown in the following example.

| Product type | Score threshold |
|--------------|-----------------|
| Digital | 500 |
| Consumable | 600 |
| Physical | 750 |

You can then configure a rule that enforces the rejection of transactions where the [risk score](ap-scorecard.md#risk-model-score) exceeds the specified threshold for the product type. For information about how to create effective rules to customize your business logic, see [Rules](rules.md).

> [!NOTE]
>
> Lists can also be referenced within Functions. For more information, see [Functions](functions.md).

## Upload a custom list

You can upload organized data in a list file to Fraud Protection and then reference the list in a [rule](rules.md). The file must adhere to the specifications that are described in the [Format requirements](lists.md#format-requirements) section earlier in this article.

To upload a list to Fraud Protection, follow these steps.

1. Select **New list**.
1. Select **Browse** to find the file. Select the file, and then select **Open**.

    Fraud Protection opens a preview of the file for you to review. The preview pane shows a maximum of 20 rows.

1. To upload the file, select **Continue**. To upload a different file, select **Cancel**, and then repeat step 2.
1. Add a name and description that will make it easy for your team to identify and use the list.

    > [!NOTE]
    > The list name can't be changed after you complete this step.

1. Select **Create**.

    Because of caching, it might take up to two minutes for the list to become active.

> [!IMPORTANT]
> Don't include the following sensitive personal data or highly regulated data types in the files that you upload:
>
> - Biometric data, genetic data, or any data that is related to health
> - Personal data that reveals racial or ethnic origin, or religious views
> - Personal data that, by its nature, is sensitive or private, such as data about a person's sexual orientation or philosophical beliefs
>
> For information about how data is used and protected in Fraud Protection, see [Security, compliance, and data subject requests](security-compliance.md).

## Update a custom list

You can update a custom list from the **Lists** page at any time, to add new information or change existing information. You can change the description of a custom list, but you can't change its name.

To modify support lists, use the [Support page](risk-support.md).

To update the contents of a custom list in Fraud Protection, follow these steps.

1. If the most up-to-date version of the list is already saved on your computer, open that file. Otherwise, you must first select the list that you want to update, and then select **Download** to get the most up-to-date version.
1. Make all your edits directly in the file. When you've finished, save the file to your computer.
1. On the **Lists** management page, select the list to update, and then select **Edit**.
1. Select **Browse** to find the file. Select the file that you just edited, and then select **Open**.

    Fraud Protection opens a preview of the file for you to review. The preview pane shows a maximum of 20 rows.

1. To upload the file, select **Continue**, and then select **Update**. 

    Because of caching, it might take up to two minutes for the list to become active.

To update the description of a custom list in Fraud Protection, follow these steps.

1. Select the list to update, and then select **Edit**.
1. Update the text in the **Description** field, and then select **Update**.

## Delete a custom list

- To delete a list, select the list, and then select **Delete**.
- To delete multiple lists, select the lists you want to remove, and then select **Delete**.

> [!NOTE]
> Lists which are referenced in rules cannot be deleted.

## Download a custom list

You can download a list in Fraud Protection and then view it in any text editor.

- To download a list, select it, and select **Download**. Then select the download button in the lower-left corner of the browser window to view the list.
- To download multiple lists, select them, and then select **Download**. The files are downloaded as a zip file.

## Search for a custom list

When you search for a list, all list names and descriptions are searched, and the results are filtered accordingly.

- To search for a list, enter a keyword in the **Search** field in the upper right of the **Lists** page.
- To remove the filter, either clear the keyword from the **Search** field or select the **X** to the right.

## Preview a custom list

You can preview a list in Fraud Protection. The preview pane shows a maximum of 20 rows.

- To preview a list, select it, and then select **Preview**.
- To view the full list, select **Download** to download the list, and then open the file in any text editor.

## Additional resources

[Lists overview](lists-overview.md)

[Manage support lists](manage-support-lists.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
