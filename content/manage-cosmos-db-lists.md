---
author: josaw1
description: This article explains how to add, manage, and use custom Cosmos DB lists to manage information, fight fraud, and enforce business policies in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 12/11/2024
ms.topic: how-to
search.audienceType:
  - admin
title: Manage custom Cosmos DB lists
---

# Manage custom Cosmos DB lists

[!include[deprecation](includes/deprecation.md)]

Custom lists are created and defined by you. You can create custom lists that use Cosmos DB as a data source, tailored to your specific business needs or fraud protection strategy. For example, you can create a custom list containing email addresses, IP addresses, or product IDs, along with other values associated with each entry. This option is ideal for large and complex datasets that require real-time updates and access. Moreover, you can maintain all list data in one place within your Cosmos DB database.

## Prerequisites

- To create a custom list using Cosmos DB in Microsoft Dynamics 365 Fraud Protection, you must first [create a container in Azure Cosmos DB](/azure/cosmos-db/nosql/how-to-create-container) and [choose a partition key that's appropriate for your data structure](/azure/cosmos-db/partitioning-overview#choose-partitionkey).
- You can store your connection string securely in Azure Key Vault, which is used later in the list definition. For more information, refer to the [About Azure Key Vault managed storage account keys](/azure/key-vault/secrets/about-managed-storage-account-keys) article.
- Add a role assignment to grant "Key Vault Secrets User" access for "Dynamics 365 Fraud Protection". For more information, refer to the [Use an Azure RBAC for managing access](/azure/key-vault/general/rbac-guide#best-practices-for-individual-keys-secrets-and-certificates-role-assignments) article.

[!INCLUDE[custom-list-explanation](includes/custom-list-explanation.md)]

## Create a custom list

You can define a list and then reference the list in a [rule](rules.md). Before you create the list definition, make sure you met the prerequisites described in the [Prerequisites](manage-cosmos-db-lists.md#prerequisites) section earlier in this article.

To create a list definition, follow these steps.

1. Select **New list**.
1. Add a name and description that will make it easy for your team to identify and use the list.
1. Select **Cosmos DB** from the **Data source** menu.
1. Add **Azure Cosmos DB account**.
1. Add **Database name**.
1. Add the **Azure key vault URL** that contains the connection string to the Azure Cosmos DB. The connection string should be stored as a secret in the key vault. An example of a connection string is: `AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>`.
1. Add a timeout and select **Test connection** to check your database connection. A list of containers appears after a successful connection.
1. Choose a container from the dropdown menu. Once you select a container, properties from the first document in the container are auto-populated as columns.
1. To add more columns, select  **Add column**. You can either select a column from the dropdown menu, if available, or enter a custom column name to be added to the Cosmos DB container later.
1. You can select **Preview** to preview the list data.
1. Select **Create**. Because of caching, it may take up to two minutes for the list to become active.

> [!IMPORTANT]
> Don't include the following sensitive personal data or highly regulated data types in the Cosmos DB container:
>
> - Biometric data, genetic data, or any data that is related to health.
> - Personal data that reveals racial or ethnic origin, or religious views.
> - Personal data that, by its nature, is sensitive or private, such as data about a person's sexual orientation or philosophical beliefs.
>
> For information about data use and protection in Fraud Protection, refer to the [Security, compliance, and data subject requests](security-compliance.md) article.

## Update a custom list

You can update a custom Cosmos DB list definition from the **Lists** page at any time to add new information or modify existing information. This doesn't include data updates. Data updates should be made directly from your database, and are automatically reflected in the system. You can make changes to the description of a custom list, but its name and columns can't be changed if they're used in a published rule or velocity.

To update a custom Cosmos DB list in Fraud Protection, follow these steps.

1. Select the list you want to update, and then select **Edit**.
1. Make the desired changes.
1. If you change any of the mandatory fields in the **Database** section, you can select **Test connection** before updating. Optionally, you can select **Preview** to view the list data before updating.
1. Select **Update** to apply your changes.

## Delete a custom list

- To delete a list, select the list, and then select **Delete**.
- To delete multiple lists, select the lists you want to remove, and then select **Delete**.

> [!NOTE]
You can't delete lists that are referenced in rules or velocities.

## Search for a custom list

When you search for a list, all list names, descriptions, and data source type are searched, and the results are filtered accordingly.

- To search for a list, enter a keyword in the **Search** field in the upper right of the **Lists** page.
- To remove the filter, either clear the keyword from the **Search** field or select the **X**.

## Preview a custom list

You can preview a list in Fraud Protection. The preview pane shows a maximum of 20 rows.

- To preview a list, select the list, and then select **Preview**.

## Monitor custom lists in the Fraud Protection portal

Fraud Protection displays a tile that contains three metrics for each Cosmos DB list that you define.

[!INCLUDE[external-call-metrics](includes/external-call-metrics.md)]

> [!NOTE]
> Metrics are displayed only when you test connections by selecting **Test connection** or when your list is used in an active rule.

1. To display a more detailed view of the metrics for your Cosmos DB list, select the list from the **Lists** page. Then select **Performance** from the command bar. 

2. To view metrics for any time frame in the last three months, adjust the **Date range** setting at the top of the page.

Fraud Protection displays an **Error** chart in addition to the three previously described metrics. The error chart shows the number of errors by error type and code. To view error counts over time, or to view the distribution of errors, select **Pie chart**.

Fraud Protection may display the following errors in addition to HTTP client errors (400, 401, and 403).

- **Definition not found** – The list was deleted, but it's still referenced in a rule.
- **Timeout** – Specify how long, in milliseconds, the request should wait before it times out. You must specify a number between 1 and 5000.
- **Communication failure** – No connection could be made to the target because of a network issue or because the target is unavailable.
- **Circuit breaker** – If the list failed continuously and has exceeded a certain threshold, all further calls will be suspended for a short interval.
- **Unknown Failure** – An internal Fraud Protection failure occurred.

## Additional resources

[Lists overview](lists-overview.md)

[Manage support lists](manage-support-lists.md)

[Manage custom CSV lists](lists.md)

[!INCLUDE[footer-include](includes/footer-banner.md)]
