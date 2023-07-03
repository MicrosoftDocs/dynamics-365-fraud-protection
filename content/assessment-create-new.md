# Assessment wizard overview

If you have a fraud scenario that cannot be addressed using our existing [Account creation](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/ap-overview), [Account login](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/ap-overview), or [Purchase](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/purchase-protection) APIs, the Assessment wizard provides you with the tools to create your own customized real-time Fraud Protection APIs.

Once you have identified the specific fraud scenario you would like to protect your business against, and the data you will use to evaluate this scenario for likelihood of fraud, you can access this wizard by clicking the "_+ New assessment_" link under Fraud assessments in left-hand navigation bar.

Clicking this link will open the Assessment wizard, which consists of five steps:

1. [Select template](assessment-create-new.md#assessment-wizard-select-template)
2. [Define schema details](assessment-create-new.md#assessment-wizard-define-schema-details)
3. [Select observation events](assessment-create-new.md#assessment-wizard-select-observation-events)
4. [Define settings](assessment-create-new.md#assessment-wizard-define-settings)
5. [Finalize name and endpoint](assessment-create-new.md#assessment-wizard-finalize-name-and-endpoint)

This “_+ New assessment_” link is only visible in the root environment and to users with “Read/Write” permissions to Assessments as defined in [User roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/configure-user-access).  If both pre-requisites are true and the “_+ New assessment_” link still is not visible in left-hand navigation bar, you have reached maximum limit of assessments (16) that can be created at any given time and will need to delete one of your existing assessments before a new one can be created.  The Account creation, Account login, Purchase, and Loss prevention assessments in the left-hand navigation bar do not contribute to this limit.

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

The **Card payment** template allows you to assess the fraud risk of online and offline card payments for financial institutions. This template is geared towards issuing banks and other financial institutions.  For merchant-based purchase scenarios, please use Fraud Protection’s [Purchase protection](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/purchase-protection) solution.

### Device fingerprinting template

The **Device fingerprinting template** allows you to gather intelligence from remote computing devices to help assess fraud risk.  This template is useful in scenarios where you want to enable _device fingerprinting only_ and allows you to access the full suite of device attributes that Fraud Protection collects, along with other enrichments like IP intelligence.  If you would like to use device fingerprinting as part of any other scenario, you can integrate it into any of our other assessment templates by adding the “Device Fingerprinting” section to your API schema in the [Define schema details](assessment-create-new.md#assessment-wizard-define-schema-details) step of the Assessment wizard.

The device fingerprinting template has some special settings designed to keep the API lightweight.  Search and case management are both disabled by default and cannot be enabled for this template. Additionally, this template does not support risk scoring.  The _Model.Risk_ FQL function cannot be invoked when an API based on this template is used.

To use the full suite of device attributes in rules and velocities, you will need to call the _Device.GetFullAttributes_ FQL function.  Upon creating a new API based on the device fingerprinting template, a default sample rule is created that references this _Device.GetFullAttributes_ function.  For more details on this _Device.GetFullAttributes_ function, see [Language reference](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/fpl-lang-ref) guide.  For more details on default sample rules, see **INSERT 'Default rules' URL**.

See [Set up device fingerprinting](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/device-fingerprinting) for more details on setting up and enabling device fingerprinting for web and mobile.

See the following pages for more details on the device fingerprinting attribute fields Fraud Protection attempts to collect:
-	**INSERT 'Device fingerprinting attribute list for web' URL**
-	**INSERT 'Device fingerprinting attribute list for iOS' URL**
-	**INSERT 'Device fingerprinting attribute list for Android' URL**

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

The standard data fields available to any API are organized and only made available in the form of pre-defined sections.  Every fraud assessment template comes with a default set of these standard sections.  Of these default sections, the only one that is required for any template is “_Metadata_”.  While all other default standard sections can be removed from the API schema prior to creating the assessment, we highly recommend keeping all default standard sections in your API schema since removing any of these standard sections and their associated data fields will likely result in Fraud Protection returning lower quality risk scores from the FPN.

You can also add additional standard sections to your new API by clicking the “_Add Section_” drop-down and selecting those applicable to your fraud scenario.  To view the data fields that make up each standard section, see Fraud Protection’s [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) or use the _JSON Preview Pane_ accessible from within the Assessment wizard. 

### Custom data fields

**Custom data fields** are additional fields that are not used to generate scores via the Fraud Protection Network. However, they can still be used in search, reports, rules and other tenant-specific scenarios.

These fields are fully defined by you and will not impact Fraud Protection’s AI models or scores.

We support two ways for you to add custom data fields to your API’s schema:

- Individual fields can be added by clicking the “_+ New field_” link located under the Custom header; and
- Multiple fields can be added simultaneously by uploading a custom JSON (.json) file or by manually entering well-formed JSON directly into the **Import JSON** window accessible via the “_From JSON…_” option in the “_Add section_” drop-down.

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
-	[Custom](assessment-create-new.md#custom-event)
-	[Label](assessment-create-new.md#label-event)

In this step of the Assessment wizard, you will be shown those observation and label events related to the fraud assessment template selected in the [Select template](assessment-create-new.md#assessment-wizard-select-template) step along with any of the recommended ones selected by default.  Here is a summary of the related and recommended observation and label events available in this step of the wizard, broken down by assessment template:
