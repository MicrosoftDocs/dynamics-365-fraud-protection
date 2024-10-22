---
author: josaw1
description: This article explains how to add, manage, and use custom Cosmos DB lists to manage information, fight fraud, and enforce business policies in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 10/22/2023
ms.topic: how-to
search.audienceType:
  - admin
title: Manage custom Cosmos DB lists

---

# Manage custom Cosmos DB lists

Custom lists are created and defined by you. You have the ability to create custom lists that utilize Cosmos DB as a data source, tailored to your specific business needs or fraud protection strategy. For instance, you can create a custom list containing email addresses, IP addresses, or product IDs, along with additional values associated with each entry. This option is ideal for large and complex datasets that require real-time updates and access. Moreover, it allows you to maintain all list data in one place within your Cosmos DB database.

## Prerequisites

- To create a custom list using Cosmos DB in Microsoft Dynamics 365 Fraud Protection, you must first [create a container in Azure Cosmos DB](https://learn.microsoft.com/en-us/azure/cosmos-db/nosql/how-to-create-container) and [choose a partition key that's appropriate for your data structure](https://learn.microsoft.com/en-us/azure/cosmos-db/partitioning-overview#choose-partitionkey).
- You can store your connection string securely in Azure Key Vault, which will be used later in the list definition. For more information, see [About Azure Key Vault managed storage account keys](https://learn.microsoft.com/en-us/azure/key-vault/secrets/about-managed-storage-account-keys).
- Add a role assignment to grant "Key Vault Secrets User" access for "Dynamics 365 Fraud Protection". For more information, see [Assign Azure roles using the Azure portal](https://learn.microsoft.com/en-us/azure/role-based-access-control/role-assignments-portal).

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

## Create a custom list

You can define a list and then reference the list in a [rule](rules.md). Before creating the list definition, ensure you have met the prerequisites described in the [Prerequisites](manage-cosmos-db-lists.md#prerequisites) section earlier in this article.

To create a list definition, follow these steps.

1. Select **New list**.
1. Add a name and description that will make it easy for your team to identify and use the list.
1. Select **Cosmos DB** from data source menu.
1. Add **Azure Cosmos DB account**.
1. Add **Database name**.
1. Add **Azure key vault URL** which contains the connection string to the Azure Cosmos DB. The connection string should be stored as a secret in the key vault. An example of such a connection string is: `AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>`.
1. You can now add a timeout and select **Test connection** to check your database connection. A list of containers will appear after a successful connection.
1. Choose a container from the dropdown menu. Once you select a container, properties from the first document in the container will be auto-populated as columns.
1. To add more columns, select  **Add column**. You can either select a column from the dropdown menu, if available, or enter a custom column name which will be added to the Cosmos DB container later.
1. You can select **Preview** to preview the list data..
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

You can update a custom Cosmos DB list definition from the **Lists** page at any time to add new information or modify existing information. Please note that this does not include data updates; these should be made directly from your database and will be automatically reflected in our system. Changes can be made to the description of a custom list, however, its name and columns cannot be altered if it's being used in a published rule or velocity.

To update a custom Cosmos DB list in Fraud Protection, follow these steps.

1. Select the list you wish to update, and then select **Edit**.
1. Make the desired changes.
1. If any of the mandatory fields in the **Database** section have been changed, you can select **Test connection** before updating.
1. Optionally, you can select **Preview** to view the list data before updating.
1. Select **Update** to apply your changes.

## Delete a custom list

- To delete a list, select the list, and then select **Delete**.
- To delete multiple lists, select the lists you want to remove, and then select **Delete**.

> [!NOTE]
> Lists which are referenced in rules or velocities cannot be deleted.

## Search for a custom list

When you search for a list, all list names, descriptions, data source type are searched, and the results are filtered accordingly.

- To search for a list, enter a keyword in the **Search** field in the upper right of the **Lists** page.
- To remove the filter, either clear the keyword from the **Search** field or select the **X** to the right.

## Preview a custom list

You can preview a list in Fraud Protection. The preview pane shows a maximum of 20 rows.

- To preview a list, select it, and then select **Preview**.

## Monitor custom lists in the Fraud Protection portal

> [!NOTE]
> Metrics are shown only when you test connections by selecting "Test connection" or when your list is used in an active rule.

1. To dive into the metrics about your Cosmos DB list, select the list from the lists page. Then, select **Performance** either from the command bar at the top of the page or from the dropdown menu that appears after right-clicking.

    Fraud Protection shows a new page that has a more detailed view of the metrics.

2. To view metrics for any time frame in the last three months, adjust the **Date range** setting at the top of the page.

In addition to the three metrics that were described earlier, an **Error** chart is shown. This chart shows the number of errors by error type and code. To view error counts over time, or to view the distribution of errors, select **Pie chart**.

In addition to HTTP client errors (400, 401, and 403), you might see the following errors:

- **Definition not found** – The list has been deleted, but it's still referenced in a rule.
- **Timeout** – The request to the target took longer than the specified time-out.
- **Communication failure** – No connection could be made to the target because of a network issue or because the target is unavailable.
- **Circuit breaker** – If the list has failed continuously and has exceeded a certain threshold, all further calls will be suspended for a short interval.
- **Unknown Failure** – An internal Dynamics 365 failure occurred.

## Additional resources

[Lists overview](lists-overview.md)

[Manage custom CSV lists](lists.md)

[Manage support lists](manage-support-lists.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
