# Assessment wizard overview

If you have a fraud scenario that cannot be addressed using our existing [Account creation](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/ap-overview), [Account login](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/ap-overview), or [Purchase](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/purchase-protection) APIs, the Assessment wizard provides you with the tools to create your own customized real-time Fraud Protection APIs.

Once you have identified the specific fraud scenario you would like to protect your business against, and the data you will use to evaluate this scenario for likelihood of fraud, you can access this wizard by clicking the "_+ New assessment_" link under Fraud assessments in left-hand navigation bar.

Clicking this link will open the Assessment wizard, which consists of five steps:

1. **INSERT 'Select template' URL**
2. **INSERT 'Define schema details' URL**
3. **INSERT 'Select observation events' URL**
4. **INSERT 'Define settings' URL**
5. **INSERT 'Finalize name and endpoint' URL**

This “_+ New assessment_” link is only visible in the root environment and to users with “Read/Write” permissions to Assessments as defined in [User roles and access](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/configure-user-access).  If both pre-requisites are true and the “_+ New assessment_” link still is not visible in left-hand navigation bar, you have reached maximum limit of assessments (16) that can be created at any given time and will need to delete one of your existing assessments before a new one can be created.  The Account creation, Account login, Purchase, and Loss prevention assessments in the left-hand navigation bar do not contribute to this limit.

## Assessment wizard: Select template

To help get you started, we have provided you with a handful of pre-defined templates that can be used to create new Fraud Protection API’s that are tailored to some of the most common fraud scenarios.  Each of these templates comes bundled with customized logic and a set of data fields that will serve as the foundation for your new Fraud Protection API.

The Assessment wizard currently supports the following templates:

- **INSERT 'Card payment' URL**
- **INSERT 'Device fingerprinting' URL**
- **INSERT 'Money transfer' URL**
- **INSERT 'Software piracy' URL**
- **INSERT 'Custom' URL**

Fraud Protection will continue to evolve this template catalogue over time to cover other scenarios where fraud is prevalent.

To view the API schema (request payload) and sample values for a given template, select the desired template and enable the _JSON Preview_ pane.  The full sample payload will be displayed in the JSON Preview by default; however, you have the option to filter the payload to only those fields that are Required or Searchable.  See [Swagger UI documentation](https://dfpswagger.azurewebsites.net/index.html) to learn more about Fraud Protection’s APIs.

- **Required fields** – These data fields must be sent as part of the request payload whenever the API is invoked.  Failing to send these fields will result in a 400 error code being returned.
- **Searchable fields** – These data fields can be used as search keys within a transaction search.

In the next step of the wizard, you will have the ability to further customize the schema of your new Fraud Protection API to meet your specific business needs.

### Card payment template

The **Card payment** template allows you to assess the fraud risk of online and offline card payments for financial institutions. This template is geared towards issuing banks and other financial institutions.  For merchant-based purchase scenarios, please use Fraud Protection’s [Purchase protection](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/purchase-protection) solution.

### Device fingerprinting template

The **Device fingerprinting template** allows you to gather intelligence from remote computing devices to help assess fraud risk.  This template is useful in scenarios where you want to enable _device fingerprinting only_ and allows you to access the full suite of device attributes that Fraud Protection collects, along with other enrichments like IP intelligence.  If you would like to use device fingerprinting as part of any other scenario, you can integrate it into any of our other assessment templates by adding the “Device Fingerprinting” section to your API schema in the **INSERT 'Define schema details' URL** step of the Assessment wizard.

The device fingerprinting template has some special settings designed to keep the API lightweight.  Search and case management are both disabled by default and cannot be enabled for this template. Additionally, this template does not support risk scoring.  The _Model.Risk_ FQL function cannot be invoked when an API based on this template is used.

To use the full suite of device attributes in rules and velocities, you will need to call the _Device.GetFullAttributes_ FQL function.  Upon creating a new API based on the device fingerprinting template, a default sample rule is created that references this _Device.GetFullAttributes_ function.  For more details on this _Device.GetFullAttributes_ function, see [Language reference](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/fpl-lang-ref) guide.  For more details on default sample rules, see **INSERT 'Default rules' URL**.

See [Set up device fingerprinting](https://learn.microsoft.com/en-us/dynamics365/fraud-protection/device-fingerprinting) for more details on setting up and enabling device fingerprinting for web and mobile.

See the following pages for more details on the device fingerprinting attribute fields Fraud Protection attempts to collect:
-	**INSERT 'Device fingerprinting attribute list for web' URL**
-	**INSERT 'Device fingerprinting attribute list for iOS' URL**
-	**INSERT 'Device fingerprinting attribute list for Android' URL**
