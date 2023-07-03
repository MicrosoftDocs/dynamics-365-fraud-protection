# Assessment wizard overview

If you have a fraud scenario that cannot be addressed using our existing [Account creation](ap-overview.md), [Account login](ap-overview.md), or [Purchase](purchase-protection.md) APIs, the Assessment wizard provides you with the tools to create your own customized real-time Fraud Protection APIs.

Once you have identified the specific fraud scenario you would like to protect your business against, and the data you will use to evaluate this scenario for likelihood of fraud, you can access this wizard by clicking the "_+ New assessment_" link under Fraud assessments in left-hand navigation bar.

Clicking this link will open the Assessment wizard, which consists of five steps:

1. [Select template](assessment-create-new.md#assessment-wizard-select-template)
2. [Define schema details](assessment-create-new.md#assessment-wizard-define-schema-details)
3. [Select observation events](assessment-create-new.md#assessment-wizard-select-observation-events)
4. [Define settings](assessment-create-new.md#assessment-wizard-define-settings)
5. [Finalize name and endpoint](assessment-create-new.md#assessment-wizard-finalize-name-and-endpoint)

This "_+ New assessment_" link is only visible in the root environment and to users with "_Read/Write_" permissions to Assessments as defined in [User roles and access](configure-user-access.md).  If both pre-requisites are true and the "_+ New assessment_" link still is not visible in left-hand navigation bar, you have reached maximum limit of assessments (16) that can be created at any given time and will need to delete one of your existing assessments before a new one can be created.  The Account creation, Account login, Purchase, and Loss prevention assessments in the left-hand navigation bar do not contribute to this limit.

## Assessment wizard: Select template

To help get you started, we have provided you with a handful of pre-defined templates that can be used to create new Fraud Protection API’s that are tailored to some of the most common fraud scenarios.  Each of these templates comes bundled with customized logic and a set of data fields that will serve as the foundation for your new Fraud Protection API.

The Assessment wizard currently supports the following templates:

- [Card payment](assessment-create-new.md#card-payment-template)
- [Device fingerprinting](assessment-create-new.md#device-fingerprinting-template)
- [Money transfer](assessment-create-new.md#money-transfer-template)
- [Software piracy](assessment-create-new.md#software-piracy-template)
- [Custom](assessment-create-new.md#custom-template)

Fraud Protection will continue to evolve this template catalogue over time to cover other scenarios where fraud is prevalent.

To view the API schema (request payload) and sample values for a given template, select the desired template and enable the _JSON Preview_ pane.  The full sample payload will be displayed in the JSON Preview by default; however, you have the option to filter the payload to only those fields that are Required or Searchable.  See [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) to learn more about Fraud Protection’s APIs.

- **Required fields** – These data fields must be sent as part of the request payload whenever the API is invoked.  Failing to send these fields will result in a 400 error code being returned.
- **Searchable fields** – These data fields can be used as search keys within a transaction search.

In the next step of the wizard, you will have the ability to further customize the schema of your new Fraud Protection API to meet your specific business needs.

### Card payment template

The **Card payment** template allows you to assess the fraud risk of online and offline card payments for financial institutions. This template is geared towards issuing banks and other financial institutions.  For merchant-based purchase scenarios, please use Fraud Protection’s [Purchase protection](purchase-protection.md) solution.

### Device fingerprinting template

The **Device fingerprinting template** allows you to gather intelligence from remote computing devices to help assess fraud risk.  This template is useful in scenarios where you want to enable _device fingerprinting only_ and allows you to access the full suite of device attributes that Fraud Protection collects, along with other enrichments like IP intelligence.  If you would like to use device fingerprinting as part of any other scenario, you can integrate it into any of our other assessment templates by adding the "_Device Fingerprinting_" section to your API schema in the [Define schema details](assessment-create-new.md#assessment-wizard-define-schema-details) step of the Assessment wizard.

The device fingerprinting template has some special settings designed to keep the API lightweight.  Search and case management are both disabled by default and cannot be enabled for this template. Additionally, this template does not support risk scoring.  The _Model.Risk_ FQL function cannot be invoked when an API based on this template is used.

To use the full suite of device attributes in rules and velocities, you will need to call the _Device.GetFullAttributes_ FQL function.  Upon creating a new API based on the device fingerprinting template, a default sample rule is created that references this _Device.GetFullAttributes_ function.  For more details on this _Device.GetFullAttributes_ function, see [Language reference](fpl-lang-ref.md) guide.  For more details on default sample rules, see [Assessment (default) rules](rules.md#assessment-default-rules).

See [Set up device fingerprinting](device-fingerprinting.md) for more details on setting up and enabling device fingerprinting for web and mobile.  The following sections detail the device fingerprinting attribute fields Fraud Protection attempts to collect:
- [Web](device-fingerprinting.md#device-fingerprinting-attribute-list-for-web)
- [iOS](device-fingerprinting.md#device-fingerprinting-attribute-list-for-ios)
- [Android](device-fingerprinting.md#device-fingerprinting-attribute-list-for-android)

### Money transfer template

The **Money transfer template** allows you to assess the fraud risk of money transfers within a financial system or network.  This template is recommended for scenarios involving peer-to-peer payment networks like Zelle.

### Software piracy template

The **Software piracy template** allows you to assess the fraud risk of software use. This template is recommended for scenarios involving software that is licensed via a subscription.

### Custom template

The **Custom template** allows you to assess the fraud risk of a custom event.  This template is designed to be used in more obscure cases where none of the other templates fit the needs of the scenario in question.

The Custom template does not support risk scoring.  The Model.Risk FQL function cannot be invoked when an API based on this template is used.

## Assessment wizard: Define schema details

Once you have identified and selected your fraud assessment template, any data fields associated with that template are automatically included in the API’s schema (request payload).  To view the API schema (request payload) and sample values for your new fraud API, enable the _JSON Preview_ pane.

In this step of the Assessment wizard, we provide you with the ability to further customize your new API’s schema by adding any additional fields needed to help evaluate your fraud scenario and remove any fields that you may not be able to provide or are otherwise irrelevant to your fraud scenario.

Each data field is classified into one of two categories: [Standard](assessment-create-new.md#standard-data-fields) or [Custom](assessment-create-new.md#custom-data-fields).

### Standard data fields

**Standard data fields** are processed and stored within the Fraud Protection Network (FPN) to generate a risk score and can be used in search, reports, rules, and other tenant-specific scenarios.

The accuracy of the risk score returned by Fraud Protection depends on multiple factors, including whether the set of data fields provided presents a complete and accurate description of the event being evaluated.

The standard data fields available to any API are organized and only made available in the form of pre-defined sections.  Every fraud assessment template comes with a default set of these standard sections.  Of these default sections, the only one that is required for any template is "_Metadata_".  While all other default standard sections can be removed from the API schema prior to creating the assessment, we highly recommend keeping all default standard sections in your API schema since removing any of these standard sections and their associated data fields will likely result in Fraud Protection returning lower quality risk scores from the FPN.

You can also add additional standard sections to your new API by clicking the "_Add section_" drop-down and selecting those applicable to your fraud scenario.  To view the data fields that make up each standard section, see Fraud Protection’s [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) or use the _JSON Preview Pane_ accessible from within the Assessment wizard. 

### Custom data fields

**Custom data fields** are additional fields that are not used to generate scores via the Fraud Protection Network. However, they can still be used in search, reports, rules and other tenant-specific scenarios.

These fields are fully defined by you and will not impact Fraud Protection’s AI models or scores.

We support two ways for you to add custom data fields to your API’s schema:

- Individual fields can be added by clicking the "_+ New field_" link located under the Custom header; and
- Multiple fields can be added simultaneously by uploading a custom JSON (.json) file or by manually entering well-formed JSON directly into the **Import JSON** window accessible via the "_From JSON…_" option in the "_Add section_" drop-down.

Each custom data field includes the following fields:

-	**Name** (_required_) – This is the name of the custom data field included in your API’s schema.
-	**Friendly name** – This is the human-readable name assigned to the custom data field that is displayed when the field is referenced in other operational pages of Fraud Protection (e.g., Search, Case Management).
-	**Type** (_required_) – This is the data type of the custom data field.
    -	Fraud Protection supports both primitive (e.g., integer, boolean) and non-primitive (e.g., array, object) data types, as well as some context-specific data types (e.g., email, IP address).
-	**Sample value** – This value is displayed in the JSON Preview Pane to help visualize what your new API is expecting as input for this field when the API is invoked.
-	**Required** (_checkbox_) – This value dictates if the custom data field must be provided whenever the API is invoked.
    -	If enabled, failing to send this field as part of the API’s request payload will result in a 400 error code being returned.
-	**Searchable** (_checkbox_) – This value dictates if the custom data field can be used as a search key within transaction search.

Prior to your new assessment being created, you will have the ability to edit or delete any previously added custom data field.  Once the assessment has been created, you will not be able to change the **Name** or **Type** of a custom data field.

## Assessment wizard: Select observation events

Observation and label events allow customers to share information and other context with Fraud Protection for a given transaction.  These are data ingestion only events (i.e., no information is returned in the response other than success/fail).  Data sent through observation events can be used in velocities, rules, and search.

Fraud Protection supports the following observation and label events:

-	[Assessment status](assessment-create-new.md#assessment-status-event)
-	[Bank](assessment-create-new.md#bank-event)
-	[Chargeback](assessment-create-new.md#chargeback-event)
-	[Label](assessment-create-new.md#label-event)
-	[Custom](assessment-create-new.md#custom-event)

In this step of the Assessment wizard, you will be shown those observation and label events related to the fraud assessment template selected in the [Select template](assessment-create-new.md#assessment-wizard-select-template) step along with any of the recommended ones selected by default.  Here is a summary of the related and recommended observation and label events available in this step of the wizard, broken down by assessment template:

<table>
<thead>
<tr>
<th>Assessment template</th>
<th>Related events</th>
<th>Recommended events</th>
</tr>
</thead>
<tbody>
<tr>
<td>Card payment</td>
<td>Assessment status,<br>Label</td>
<td>Assessment status,<br>Label</td>
</tr>
<tr>
<td>Device fingerprinting</td>
<td>Assessment status,<br>Label</td>
<td>N/A</td>
</tr>
<tr>
<td>Money transfer</td>
<td>Assessment status,<br>Label</td>
<td>Assessment status,<br>Label</td>
</tr>
<tr>
<td>Software piracy</td>
<td>Assessment status,<br>Label</td>
<td>Assessment status,<br>Label</td>
</tr>
<tr>
<td>Custom</td>
<td>Assessment status,<br>Bank,<br>Chargeback,<br>Label</td>
<td>N/A</td>
</tr>  
</tbody>
</table>

Additional observation events can also be added to an assessment after the assessment has been created.  The list of available observation events exposed through the [Assessment configuration](assessment-configure-existing.md#assessment-configuration-overview) flow is a superset of those listed in the table above.

### Assessment status event

The **Assessment status event** allows you to provide Fraud Protection with information pertaining to the status of an assessment event. This is a data ingestion only event. Assessment Status event is applicable to all assessment templates.

### Bank event

The **Bank event** allows you to provide Fraud Protection with information pertaining to a bank event, such as transactions being approved or rejected for bank authorization. This is a data ingestion only event.

### Chargeback event

The **Chargeback event** allows you to provide Fraud Protection with information pertaining to a dispute a customer has with their bank regarding a particular transaction. This event is a data ingestion only event.

### Label event

The **Label event** allows you to provide Fraud Protection with fraud and non-fraud signals related to a transaction. This event is a data ingestion only event.

See [Labels API](labels-api.md) for more details on Fraud Protection’s label event.

### Custom event

The **Custom event** allows you to provide Fraud Protection with any custom information pertaining to a transaction.

## Assessment wizard: Define settings

In this step of the Assessment wizard, you can select the following settings based on the fraud assessment template selected in the [Select template](assessment-create-new.md#assessment-wizard-select-template) step.

### Rule evaluation behavior

This setting determines the order in which the rules will be evaluated for your assessment.  All fraud assessment templates default to "_Run all matching rules until a decision is made_", which allows multiple rules to be evaluated for a single transaction until a decision (Approve, Reject, Review) is made.  See [Rule evaluation behavior](rules.md#rule-evaluation-behavior) for more details.

### Additional features

Fraud Protection supports three settings for three different assessment features:

- **Case management** – Allows you to manage and take action on transactions that require review by human subject matter experts.  See [Case management overview](case-management-overview.md) for more details.
- **Search** – Allows you to find and view details associated with specific transactions.  See [Search](search.md) for more details.

The features available and their default settings will vary based on the fraud assessment template you selected in the Select template step.  Here is a summary of the assessment feature default settings broken down by assessment template:

| Template | Case management | Search |
|----------|-----------------|--------|
| Card payment | Enabled | Enabled |
| Device fingerprinting | N/A | N/A |
| Money transfer | Enabled | Enabled |
| Software piracy | Disabled | Disabled |
| Custom | Disabled | Custom |

For Search to work at an assessment level, please make sure you also have it enabled at the tenant level.

If you decide to disable Search and Case Management for your assessment after these features were enabled, any transactions that were indexed for Search and any support cases that were active within Case Management will continue to exist for the time periods that these features were enabled.

### Data subject IDs

A **data subject ID** is an indexable field that Fraud Protection uses to allow you to export or delete data to comply with data subject requests from your customers. _metadata.eventId_ will always be a data subject ID, and Fraud Protection gives you the option to select a maximum of two additional fields as data subject IDs.

If you have a field in your API schema that relates to user data, we highly recommend you select that field as a data subject ID as it will make it easier for you to comply with data subject requests from your customers. Some common examples of data subject IDs are:

- _user.id_
- _user.username_
- _user.email_
- _user.phone_
- _shipping.email_

If the standard section _User_ is included in your API’s schema, Fraud Protection will default select _user.id_ as a data subject ID (this counts as one of the two additional fields).

Once you have selected data subject ID(s) and created the assessment by completing the Assessment wizard, you cannot remove any of these existing data subject IDs. If you have less than three data subject IDs selected, you will be able to add additional data subject IDs via the [Assessment configuration](assessment-configure-existing.md#assessment-configuration-overview) page until this limit is reached.

Transactions that were sent before a data subject ID was selected will not be accessible for export or deletion by that data subject ID. _metadata.eventId_ is always set as a data subject ID, so events associated with a given assessment can always be exported and deleted using that field.

See [Compliance overview](security-compliance.md) for more information about exporting and deleting data.

## Assessment wizard: Finalize name and endpoint

Once you have finished configuring the settings for your fraud assessment, the last step is to name the new Fraud Protection API.

- **Friendly name** (_required_) – This is the human-readable name of your assessment that will be displayed in the left-hand navigation bar, search, case management, rules, reporting, and more.
- **API name** (_required_) – This is the unique name that will be included in each call to the API for the fraud assessment.
    - The API name cannot be changed if the assessment is in use (e.g., used in rules or velocities).  It may also be visible to the Fraud Protection engineering team as it is considered system metadata.

Upon completing this step, your newly created assessment will be accessible in the left-hand navigation bar under "_Fraud assessments_" of the Fraud Protection portal.  This new assessment can take advantage of all the core capabilities that exist in the product – invoking risk scores using our AI models, writing rules to make decisions, etc.
