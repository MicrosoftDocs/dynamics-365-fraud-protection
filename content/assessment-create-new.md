---
author: josaw1
description: This article provides information about the Assessment wizard and how to create customized real-time APIs in Fraud Protection.
ms.author: josaw
ms.date: 02/27/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Assessment wizard overview

---

# Assessment wizard overview

If you have a fraud scenario that can't be addressed using the [Account creation](ap-overview.md), [Account login](ap-overview.md), or [Purchase](purchase-protection.md) APIs, the Assessment wizard provides you with the tools to create your own customized real-time Dynamics 365 Fraud Protection APIs.

After you identify the specific fraud scenario you want to protect your business against, and the data to evaluate the scenario, select **+ New assessment** to open the **Assessment wizard**.

The **Assessment wizard** which consists of five steps:

1. [Select template](#template)
2. [Define schema details](#schema)
3. [Select observation events](#observation)
4. [Define settings](#settings)
5. [Finalize name and endpoint](#finalize)

This link is only visible in the root environment and to users with **Read/Write** permissions to **Assessments** as defined in the article, [User roles and access](configure-user-access.md). If both prerequisites are true and the **+ New assessment_** link isn't visible, you have reached the maximum limit of 16 assessments that can be created. Delete one of your existing assessments before you create a new one. The **Account creation**, **Account login**, **Purchase**, and **Loss prevention** assessments don't contribute to this limit.

## <a name="template"></a> Select template

To get started, use the available predefined templates to create new Fraud Protection API’s that are tailored to some of the most common fraud scenarios. Each of these templates is bundled with customized logic and a set of data fields that serve as the foundation for your new Fraud Protection API.

The **Assessment wizard** currently supports the following templates:

- [Card payment](assessment-create-new.md#card-payment-template)
- [Device fingerprinting](assessment-create-new.md#device-fingerprinting-template)
- [Loyalty program](assessment-create-new.md#loyalty-program-template)
- [Money transfer](assessment-create-new.md#money-transfer-template)
- [Software piracy](assessment-create-new.md#software-piracy-template)
- [Custom](assessment-create-new.md#custom-template)

Fraud Protection continues to evolve this template catalog over time to cover other scenarios where fraud is prevalent.

To view the API schema (request payload) and sample values for a given template, select the template and enable the **JSON Preview** pane. The full sample payload is displayed in the preview pane by default. However, you can filter the payload to only those fields that are required or searchable. See [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) to learn more about Fraud Protection’s APIs.

- **Required fields** – These data fields must be sent as part of the request payload whenever the API is invoked. Failing to send these fields results in a 400 error code being returned.
- **Searchable fields** – These data fields can be used as search keys within a transaction search.

In the next step of the wizard, you can further customize the schema of your new Fraud Protection API to meet your specific business needs.

### Card payment template

The **Card payment** template allows you to assess the fraud risk of online and offline card payments for financial institutions. This template should be used for issuing banks and other financial institutions. For merchant-based purchase scenarios, use Fraud Protection’s [Purchase protection](purchase-protection.md) solution.

### Device fingerprinting template

Use the **Device fingerprinting template** to gather intelligence from remote computing devices to help assess fraud risk. This template is useful in scenarios where you want to enable **device fingerprinting only**. The template allows you to access the full suite of device attributes that Fraud Protection collects, along with other enrichments like IP intelligence. To use device fingerprinting as part of any other scenario, integrate it into other assessment templates by adding the **Device Fingerprinting** section to your API schema in the [Define schema details](#schema) step of the **Assessment wizard**.

The device fingerprinting template has some special settings designed to keep the API lightweight. **Search** and **Case management** are both disabled by default and can't be enabled for this template. Additionally, this template doesn't support risk scoring. The **Model.Risk** FQL function can't be invoked when an API based on this template is used.

To use the full suite of device attributes in rules and velocities, call the **Device.GetFullAttributes** FQL function. When you create a new API based on the device fingerprinting template, a default sample rule is created that references this function. To learn more about this function, see [Language reference](fpl-lang-ref.md) guide. For more details on default sample rules, see [Assessment (default) rules](rules.md#assessment-default-rules).

See [Overview of device fingerprinting](device-fingerprinting.md) for more information. [Attributes in device fingerprinting](df-attribute.md) details the device fingerprinting attribute fields Fraud Protection attempts to collect.

### Loyalty program template
The **Loyalty program template** allows you to assess the fraud risk of activity within loyalty programs. This template is recommended for scenarios involving rewards redemption and loyalty program enrollment.

### Money transfer template

The **Money transfer template** allows you to assess the fraud risk of money transfers within a financial system or network. This template is recommended for scenarios involving peer-to-peer payment networks like Zelle.

### Software piracy template

The **Software piracy template** allows you to assess the fraud risk of software use. This template is recommended for scenarios involving software that is licensed by using a subscription.

### Custom template

The **Custom template** allows you to assess the fraud risk of a custom event. This template is designed for more obscure cases where no other templates fit the needs of the scenario in question.

The Custom template doesn't support risk scoring. The **Model.Risk** FQL function can't be invoked when an API based on this template is used.

## <a name="schema"></a> Define schema details

After you identify and select your fraud assessment template, any data fields associated with that template are automatically included in the API’s schema (request payload). To view the API schema and sample values for your new fraud API, enable the **JSON Preview** pane.

In this step of the **Assessment wizard**, you can further customize your new API’s schema by adding any additional fields needed to help evaluate your fraud scenario and remove any fields that you may not be able to provide or are otherwise irrelevant to your fraud scenario.

Each data field is classified into one of two categories:
- [Standard](assessment-create-new.md#standard-data-fields)
- [Custom](assessment-create-new.md#custom-data-fields)

### Standard data fields

**Standard data fields** are processed and stored within the Fraud Protection Network to generate a risk score and can be used in search, reports, rules, and other tenant-specific scenarios.

The accuracy of the risk score returned by Fraud Protection depends on multiple factors, including whether the set of data fields provided presents a complete and accurate description of the event being evaluated.

The standard data fields available to any API are organized and only made available in the form of predefined sections. Every fraud assessment template comes with a default set of these standard sections. Of these default sections, only **Metadata** is required for any template. While all other default standard sections can be removed from the API schema before creating the assessment, we highly recommend keeping all default standard sections in your API schema since removing any of these standard sections and their associated data fields may result in Fraud Protection returning lower quality risk scores from the Fraud Protection Network (FPN).

You can add additional standard sections to your new API by selecting the **Add section** drop-down and selecting the sections applicable to your fraud scenario. To view the data fields that make up each standard section, see Fraud Protection’s [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) or use the **JSON Preview** pane accessible from within the **Assessment wizard**. 

### Custom data fields

**Custom data fields** are additional fields that aren't used to generate scores using the Fraud Protection Network. However, they can still be used in search, reports, rules and other tenant-specific scenarios.

These fields are fully defined by you and don't impact Fraud Protection’s AI models or scores.

Add custom data fields to your API’s schema using one of the following methods:

- Individual fields can be added by selecting **+ New field**  under the **Custom header**
- Multiple fields can be added simultaneously by uploading a custom JSON (.json) file or by manually entering well-formed JSON directly into the **Import JSON** window accessible from the **From JSON…** option in the **Add section** drop-down.

Each custom data field includes the following fields:

-	**Name** – This is the name of the custom data field included in your API’s schema.
-	**Friendly name** – This is the human-readable name assigned to the custom data field that's displayed when the field is referenced in other operational pages of Fraud Protection, such as **Search** and **Case Management**.
-	**Type** – This is the data type of the custom data field.
    - Fraud Protection supports both primitive (integer, boolean) and non-primitive (array, object) data types, as well as some context-specific data types ( email, IP address).
-	**Sample value** – This value is displayed in the **JSON Preview** pane to help visualize what your new API is expecting as input for this field when the API is invoked.
-	**Required** – This value dictates if the custom data field must be provided whenever the API is invoked.
    - If this checkbox is selected, failure to send this field as part of the API’s request payload will result in a 400 error code being returned.
-	**Searchable** – This value dictates if the custom data field can be used as a search key within transaction search.

Before your new assessment is created, you can edit or delete any previously added custom data fields. After the assessment is created, you can't change the **Name** or **Type** of a custom data field.

## <a name="observation"></a> Select observation events

You can use observation and label events to share information and other context with Fraud Protection for a specific transaction. These are data ingestion only events which means that no information is returned in the response other than success/fail. Data sent through observation events can be used in velocities, rules, and search.

Fraud Protection supports the following observation and label events:

-	[Assessment status](assessment-create-new.md#assessment-status-event)
-	[Bank](assessment-create-new.md#bank-event)
-	[Chargeback](assessment-create-new.md#chargeback-event)
-	[Label](assessment-create-new.md#label-event)
-	[Custom](assessment-create-new.md#custom-event)

In this step of the **Assessment wizard**, you're shown those observation and label events related to the fraud assessment template you previoulsy selected along with any of the recommended ones selected by default. The following table is a summary of the related and recommended observation and label events available in this step of the wizard, broken down by assessment template:

| Assessment template | Related events | Recommended events |
|----------|-----------------|--------|
| Card payment | Assessment status,<br>Label | Assessment status,<br>Label |
| Device fingerprinting | Assessment status,<br>Label | N/A |
| Loyalty program | Assessment status,<br>Label | Assessment status,<br>Label |
| Money transfer | Assessment status,<br>Label | Assessment status,<br>Label |
| Software piracy | Assessment status,<br>Label | Assessment status,<br>Label |
| Custom | Assessment status,<br>Bank,<br>Chargeback,<br>Label | N/A |

Additional observation events can also be added to an assessment after the assessment is created.  The list of available observation events exposed through the [Assessment configuration](assessment-configure-existing.md#assessment-configuration-overview) flow is a superset of those listed in the table above.

### Assessment status event

The **Assessment status event** allows you to provide Fraud Protection with information pertaining to the status of an assessment event. This is a data ingestion only event. The Assessment Status event is applicable to all assessment templates.

### Bank event

The **Bank event** allows you to provide Fraud Protection with information pertaining to a bank event, such as transactions being approved or rejected for bank authorization. This is a data ingestion only event.

### Chargeback event

The **Chargeback event** allows you to provide Fraud Protection with information pertaining to a dispute a customer has with their bank regarding a particular transaction. This event is a data ingestion only event.

### Label event

The **Label event** allows you to provide Fraud Protection with fraud and non-fraud signals related to a transaction. This event is a data ingestion only event.

For more details on Fraud Protection’s label event, see [Labels API](labels-api.md).

### Custom event

The **Custom event** allows you to provide Fraud Protection with any custom information pertaining to a transaction.

## <a name="settings"></a> Define settings

In this step of the **Assessment wizard**, select settings based on the fraud assessment template you selected earlier.

### Rule evaluation behavior

This setting determines the order in which the rules are evaluated for your assessment. All fraud assessment templates default to **Run all matching rules until a decision is made**, which allows multiple rules to be evaluated for a single transaction until a decision is made. See [Rule evaluation behavior](rules.md#rule-evaluation-behavior) for more details.

### Additional features

Fraud Protection supports the following settings for three different assessment features:

- **Case management** – Manage and take action on transactions that require a review by human subject matter experts. For more information, see [Case management overview](case-management-overview.md).
- **Search** – Find and view details associated with specific transactions. To learn more, see [Search](search.md).

The available features  and their default settings vary based on the fraud assessment template you selected in the **Select template** step. The following table is a summary of the assessment feature default settings broken down by assessment template:

| Template | Case management | Search |
|----------|-----------------|--------|
| Card payment | Disabled | Enabled |
| Device fingerprinting | N/A | N/A |
| Loyalty program | Disabled | Enabled |
| Money transfer | Disabled | Enabled |
| Software piracy | Disabled | Disabled |
| Custom | Disabled | Disabled |

For **Search** to work at an assessment level, ensure it's enabled at the tenant level.

If you decide to disable **Search** and **Case Management** for your assessment after these features were enabled, any transactions that were indexed for **Search** and any support cases that were active within **Case Management** will continue to exist for the time periods that these features were enabled.

### Data subject IDs

A **data subject ID** is an indexable field that Fraud Protection uses so you can export or delete data to comply with data subject requests from your customers. A **metadata.eventId** will always be a data subject ID. Fraud Protection gives you the option to select a maximum of two additional fields as data subject IDs.

If you have a field in your API schema that relates to user data, we highly recommend you select that field as a data subject ID as it makes it easier for you to comply with data subject requests from your customers. Some common examples of data subject IDs are:

- user.id
- user.username
- user.email
- user.phone
- shipping.email

If the standard section **User** is included in your API’s schema, Fraud Protection selects **user.id** by default as a data subject ID. This counts as one of the two additional fields.

After you select the data subject IDs and create the assessment by completing the Assessment wizard, you can't remove any of the existing data subject IDs. If you have less than three data subject IDs selected, you can add additional data subject IDs by using the [Assessment configuration](assessment-configure-existing.md#assessment-configuration-overview) page until the limit is reached.

Transactions sent before a data subject ID was selected aren't accessible for export or deletion by that data subject ID. The **metadata.eventId** is always set as a data subject ID, so events associated with a given assessment can always be exported and deleted using that field.

See [Compliance overview](security-compliance.md) for more information about exporting and deleting data.

## <a name="finalize"></a> Finalize name and endpoint

After you configure the settings for your fraud assessment, the last step is to name the new Fraud Protection API.

- **Friendly name** – This is the human-readable name of your assessment that's displayed in the navigation bar, search, case management, rules, and reporting.
- **API name** – This is the unique name thats' included in each call to the API for the fraud assessment. The API name can't be changed if the assessment is in use with rules or velocities. The API name may also be visible to the Fraud Protection engineering team as it's considered system metadata.

When you complete this step, your new assessment is accessible in the navigation bar under **Fraud assessments**. The new assessment can take advantage of all the core capabilities that exist in the product including, invoking risk scores using our AI models and writing rules to make decisions.


[!INCLUDE[footer-include](includes/footer-banner.md)]
