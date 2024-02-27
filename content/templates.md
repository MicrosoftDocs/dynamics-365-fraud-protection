---
author: zhuoche
description: This article describes how to create and use templates in Microsoft Dynamics 365 Fraud Protection.
ms.author: zhuoche
ms.date: 02/27/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Templates 
---

# Templates

This article describes how to create and use templates in Microsoft Dynamics 365 Fraud Protection.

Templates allow you to save resources (for example, decision rules or post-decision actions) and configurations (for example, assessment or case management configurations) from your Fraud Protection portal. You can include multiple subresources in the same template so that you can use it in a new environment or tenant without manually configuring each resource. 

You can create templates from a resource in your Fraud Protection tenant and then download them to your computer as template files or save them in template library where they can be used later. 

You can create a new resource from a template file or browse from the available templates in your environment. After you upload the template file or select a template from the library, you'll be able to preview what resources and subresources are contained in the template. 

> [!NOTE]
> Newly created resources and subresources are in the same state as when the template was created. Any updates to a resource after it has been referenced in a template only applies to the resource, not to the corresponding template. If updates are also needed for the corresponding template, delete the old template and create a new one.

## Use cases of templates

There are many use cases and scenarios where templates can be beneficial. For example:

- When financial institutions and payment service provider customers are onboarding new client, they can set up new environments using a template.
- When merchants make changes to their Fraud Protection configuration, they can test in sandbox environment, and then promote their changes to production environment using a template.
- Users can save a rule as template so they can duplicate them in another assessment or environment.

## Types of templates

Following templates are currently supported in Fraud Protection.

### Rule template

A rule template publishes decision rules and post-decision actions in the production branch.

> [!NOTE]
> The following resources aren't included in rule template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Draft (unpublished) rules.
> - Dependent resources for rules (for example, velocities or external calls).

### Assessment template

Assessment template subresources include:

- Assessment API attributes, labels and observation events.
- Published decision rules and post-decision actions in production branch.
- Assessment configuration and settings.
- Case management queues and routing rules.
- Case management configuration.

> [!NOTE]
> The following resources aren't included in assessment template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Draft (unpublished) rules.
> - Dependent resources for rules (for example: velocities, external calls, etc).

### Environment template

Environment template subresources include:

-	Assessment application programming interface (API) attributes, labels, and observation events.
-	Published decision rules and post-decision actions in the production branch.
-	Assessment configurations and settings.
-	Case management queues and routing rules.
-	Case management configurations.
-	Velocities.
-	List metadata without list data.
-	External calls.
-	External assessments.
-	Functions.
-	Environment metadata (for example, name, description, or geolocation metadata).

> [!NOTE]
> Following resources aren't included in environment template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Draft (unpublished) rules.
> - List data (list name and columns are included).
> - User permission data.
> - Child environments and hierarchy structure.
> - Application ID, device fingerprint certificate, and event tracing.
> - Tab settings.

## Create template

You can create a template from the supported resources in your Fraud Protection portal. 

> [!NOTE]
> In a multi-hierarchy tenant, templates created in an environment are accessible to its children environments. For more information, see [Multi-hierarchy for templates](templates.md#multi-hierarchy-for-template) for details.

### Create a rule template

To create a rule template, follow these steps.

1. In the Fraud Protection portal, go to **Fraud assessments**, select the assessment for which you want to create a rule template, and then go to the **Rules** tab.
1. Select the overflow symbol for a published rule for which you want to create a rule template, and then select **Create template** from the menu options.
1. In the **Create template** pane, enter the **Name** you want to use for the template.
1. Preview of the template will show the list of clauses included in the rule template you are going to create.
1. Select either **Download** or **Add template**.
   - **Download** creates the template and downloads a template file to your computer that can be imported into Fraud Protection.
   - **Add template** creates the template and adds it to the Fraud Protection template library to make it available to users in the Fraud Protection and child environments. If you select this option, you can add a description of the template for reference.

### Create an assessment template

To create an assessment template, follow these steps.

1. In Fraud Protection portal, navigate to Fraud assessments, select the assessment that you want to templatize.
2. Go to **Configuration** tab, select **Create template** in the top menu bar.
3. In **Create template** panel, type the **Name** of the template you want to use.
4. Preview of the template will show the list of resources included in the assessment template you are going to create.
5. You have the option to **Create template and download** or **Create template and add to library**.
   - **Create template and download** will download a template file to your computer that can be imported into Fraud Protection later.
   - **Create template and add to library** will create the template and make it available to users in the Fraud Protection environment and its children environment. If you select this option, you can give your template a **Description** for reference.
6. Select **Download** to download template file, or select **Add template** to add template in your Fraud Protection environment.

### Create an environment template

To create an environment template, follow these steps.

1. In Fraud Protection portal, use the **environment switcher** on the top menu bar, go to **Manage environments**.
2. Go to the environment that you want to templatize, select the overflow icon, select **Create template** in the menu.
3. In **Create template** panel, type the **Name** of the template you want to use.
4. Preview of the template will show the list of resources included in the environment template you are going to create.
5. You have the option to **Create template and download** or **Create template and add to library**.
   - **Create template and download** will download a template file to your computer that can be imported into Fraud Protection later.
   - **Create template and add to library** will create the template and make it available to users in the Fraud Protection environment and its children environment. If you select this option, you can give your template a **Description** for reference.
6. Select **Download** to download template file, or select **Add template** to add template in your Fraud Protection environment.

> [!NOTE]
> Template is created within the environment that user is currently navigated to. If user creates a template from another environment, the template is available to the current environment and its children environments.
> 
> If the system runs into error when creating the subresources, the creation process will abort and some subresources or configuration will be missing from the newly created resource.
> 
> Modifying the content of a template file manually after downloading it may lead to errors when importing the template file back in the Fraud Protection portal.
> 
> Template file has a maximum size limit of 20MB. You will not be able to upload a file that exceeds this limit. 

## Creating new resources through templates

### New Decision Rule or Post Decision Action from a template

1. In Fraud Protection portal, navigate to Fraud assessments, select the assessment and go to **Rules** tab.
2. In the top menu bar, select **+ New rule** and then select **From template** in the drop down menu.
3. In **New rule** panel, you will see a drop down menu for **Template**.
   - If you want to use template file in your computer to create the new rule, select the option to **Load template file**. Select **Browse** to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** drop down menu.
4. You can give the **Name** and **Description** you want to use for the new rule.
5. Preview of the template will show the list of clauses included in the rule template you are using.
6. Select **Create** to create the new rule.
7. A new draft rule would be created matching the contents of the template. To publish this rule, you will need to select Publish.

> [!NOTE]
> If the rule has a reference to another resource that is not found in the environment (for example, a velocity or external call), you need to resolve the missing reference before you can successfully publish the draft rule. 

### New assessment from template

1. In Fraud Protection portal, navigate to Fraud assessments on the left navigation, select **+ New assessment** from the navigation menu.
2. In **Assessment setup wizard**, select **Customer created template** from the available schema templates.
3. In **Customer created templates** pop-up modal, you will see a list for **Template**.
   - If you want to use template file in your computer to create the new rule, select the option to **Load template file**. Select **Browse** to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** list.
4. Preview of the template will show the sample code and resources included in the assessment template you are using. Select **Select** to proceed.
5. Specify the **Friendly name** and **API name** you want to use for the new assessment.
6. Select **Create assessment** to create the new assessment.
7. The new assessment is created with the resources from your template.

### New environment from template

1. In Fraud Protection portal, use the **environment switcher** on the top menu bar, go to **Manage environments**.
2. If you want to create a root environment from template, select **+ New environment** from the top menu bar. If you want to create a child environment from template, in the overflow menu of the environment, select **New child environment** in the menu.
3. In **New environment** panel, select the toggle to turn on **Use template**, you will see a drop down menu for **Template**.
   - If you want to use template file in your computer to create the new rule, select the option to **Load template file**. Select **Browse** to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** list.
4. Preview of the template will show the resources included in the environment template you are using. 
5. You can edit the **Data storage geography**, **Name**, **Description**, **Tags**, **Azure AD application ID** and **Customer API ID** you want to use for the new environment.
6. Select **Create** to create the new environment.
7. The new environment is created with the resources from your template.

> [!NOTE]
> **Data storage geography** can only be edited if a root environment is being created using template. When creating child environments, the data geography would always be the same as the root environment under which the child environment is being created, which may be different from the data geography of the source environment from which the template was created.

## Template library

Templates created or imported in the current environment would be visible in the template library page, present in the left navigation under the **Data** menu.

You can perform the following actions on templates (Refer to [User permission for templates](templates.md#user-permission-for-template)):

### Import template

1. On the top menu bar, select **Import template** menu.
2. In **Create template** panel,select **Browse** to select the template file, upload it to Fraud Protection portal.
3. You can give the **Name** and **Description** you want to use for the imported template.
4. Select **Create**, the template is imported and available in template library.

### Edit template

1. In the overflow menu of the template, select **Edit** in the menu.
2. You can edit the **Name** and **Description** for the template.
3. Select **Update** to save your changes.

### Export template

1. In the overflow menu of the template, select **Export** in the menu.
2. The exported template file is downloaded to your computer that can be imported into Fraud Protection later.

### Delete template

1. In the overflow menu of the template, select **Delete** in the menu.
2. Select **Delete** in the confirmation dialog. The template will be deleted permanently, i.e., this operation cannot be undone.

## Template limits

Fraud Protection has a limit on the numbers of templates that can be created per environment. The below are the limits

  | Template type | Limit | 
  |----------|---------------|  
  | Maximum number of rule templates within an environment | 50 |  
  | Maximum number of assessment templates within an environment | 20 |  
  | Maximum number of environment templates within an environment | 10 |  

## Multi-hierarchy for template

In template library, users can only view and manage the templates created in the current environment. However, if there are templates created in an environment that is parent to the current environment, users will be able to view and select those templates from the **Template** drop down menu in the create resource flow. In another word, users in the children environments may create new resources using the template from a parent environment.

## User permission for template

For user permission, reference [User role and access](user-roles-access.md) and [Payment service provider user roles and access](psp-user-roles.md)
