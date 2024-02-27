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

- Assessment API attributes, labels, and observation events.
- Published decision rules and post-decision actions in production branch.
- Assessment configuration and settings.
- Case management queues and routing rules.
- Case management configuration.

> [!NOTE]
> The following resources aren't included in the assessment template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Draft (unpublished) rules.
> - Dependent resources for rules (for example, velocities or external calls).

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
> The following resources aren't included in environment template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Draft (unpublished) rules.
> - List data (list name and columns are included).
> - User permission data.
> - Child environments and hierarchy structure.
> - Application ID, device fingerprint certificate, and event tracing.
> - Tab settings.

## Create a template

You can create a template from the supported resources in your Fraud Protection portal. 

> [!NOTE]
> In a multi-hierarchy tenant, templates created in an environment are accessible to its children environments. For more information, see [Multi-hierarchy for templates](templates.md#multi-hierarchy-for-template) for details.

### Create a rule template

To create a rule template, follow these steps.

1. In the Fraud Protection portal, go to **Fraud assessments**, select the assessment for which you want to create a rule template, and then go to the **Rules** tab.
1. Select the overflow symbol for a published rule for which you want to create a rule template, and then select **Create template** from the menu options.
1. On the **Create template** pane, enter the **Name** you want to use for the template.
1. Preview the rule template to view the list of clauses included in the template.
1. Select either **Download** or **Add template**.
   - **Download** creates the template and downloads a template file to your computer that can be imported into Fraud Protection.
   - **Add template** creates the template and adds it to the Fraud Protection template library to make it available to users in the Fraud Protection and child environments. If you select this option, you can add a description of the template for reference.

### Create an assessment template

To create an assessment template, follow these steps.

1. In the Fraud Protection portal, navigate to **Fraud assessments**, and then select the assessment for which you want to create a template.
1. Go to the **Configuration** tab, and then select **Create template** on the top menu bar.
1. On the **Create template** pane, enter the **Name** you want to use for the template.
1. Preview the assessment template to view the list of resources included in the template.
1. Select either **Download** or **Add template**.
   - **Download** creates the template and downloads a template file to your computer that can be imported into Fraud Protection.
   - **Add template** creates the template and adds it to the Fraud Protection template library to make it available to users in the Fraud Protection and child environments. If you select this option, you can add a description of the template for reference.

### Create an environment template

To create an environment template, follow these steps.

1. In the Fraud Protection portal, go to **Manage environments** using the environment switcher on the top menu bar.
1. Go to the environment for which you want to create a template, select the overflow icon, and then select **Create template** on the top menu bar.
1. On the **Create template** pane, enter the **Name** you want to use for the template.
1. Preview the environment template to view the list of resources included in the template.
1. Select either **Download** or **Add template**.
   - **Download** creates the template and downloads a template file to your computer that can be imported into Fraud Protection.
   - **Add template** creates the template and adds it to the Fraud Protection template library to make it available to users in the Fraud Protection and child environments. If you select this option, you can add a description of the template for reference.

> [!NOTE]
> - The template is created within the environment the user is currently in. If the user creates a template from another environment, the template is available to the current environment and its children environments.
> - If the system generates errors when creating the subresources, the creation process aborts and some subresources or configurations will be missing from the newly created resource.
> - Modifying the content of a template file manually after downloading it may lead to errors when importing the template file back into the Fraud Protection portal.
> - A template file has a maximum size limit of 20 MB. You won't be able to upload a file that exceeds this limit. 

## Create new resources using templates

### Create a new decision rule or post-decision action from a template

To create a new decision rule or post-decision action from a template, follow these steps.

1. In the Fraud Protection portal, go to **Fraud assessments**, select the assessment, and then select the **Rules** tab.
1. On the top menu bar, select **+ New rule**, and then select **From template** from the drop-down menu.
1. On **New rule** pane, select one of the following from the **Template** drop-down menu:
   - Select **Load template file** to use a template file on your computer to create the new rule. Select **Browse** to select the template file and upload it to the Fraud Protection portal.
   - Select a template if you want to use a template already created in Fraud Protection portal.
1. Enter a **Name** and **Description** for the new rule.
1. Preview the template to view the list of resources included in the template.
1. Select **Create** to create a new draft rule that matches the contents of the template.
1. Select **Publish** to publish the rule.

> [!NOTE]
> If the rule has a reference to another resource that isn't found in the environment (for example, a velocity or external call), you must resolve the missing reference before you can publish the draft rule. 

### Create a new assessment from a template

To create a new assessment from a template, follow these steps.

1. In the Fraud Protection portal, on the left navigation pane, select **Fraud assessments**, and then select **+ New assessment**.
1. In the **Assessment setup** wizard, select **Customer created template** from the available schema templates.
1. On the **Customer created templates** pane, select one of the following from the **Template** drop-down menu:
   - Select **Load template file** to use a template file on your computer to create the new rule. Select **Browse** to select the template file and upload it to the Fraud Protection portal.
   - Select a template if you want to use a template already created in Fraud Protection portal.
1. Preview the template to view the the sample code and resources included in the assessment template. Select **Select** to proceed.
1. Enter the **Friendly name** and **API name** for the new assessment.
1. Select **Create assessment** to create the new assessment that matches the resources of your template.

### Create a new environment from a template

To create a new environment from a template, follow these steps.

1. In the Fraud Protection portal, go to **Manage environments** using the environment switcher on the top menu bar.
2. Do one of the following:
    - Select **+ New environment** from the top menu bar if you want to create a root environment from a template.
    - Select **New child environment** from the overflow menu of the environment if you want to create a child environment from a template.
4. On the **New environment** pane, select the toggle to turn on the **Use template** option, and then select one of the following from the **Template** drop-down menu:
   - Select **Load template file** to use a template file on your computer to create the new rule. Select **Browse** to select the template file and upload it to the Fraud Protection portal.
   - Select a template if you want to use a template already created in Fraud Protection portal.
5. Preview the template to view the list of resources included in the environment template. 
6. Enter or edit the **Data storage geography**, **Name**, **Description**, **Tags**, **Azure AD application ID**, and **Customer API ID** settings you want to use for the new environment.
7. Select **Create** to create the new environment that matches the resources of your template.

> [!NOTE]
> The **Data storage geography** setting can only be edited if a root environment is being created using the template. When creating child environments, the data storage geography is always the same as the root environment under which the child environment is being created, which may be different from the data storage geography of the source environment from which the template was created.

## Template library

Templates created or imported in the current environment would be visible in the template library page, present in the left navigation under the **Data** menu.

You can perform the following actions on templates (Refer to [User permission for templates](templates.md#user-permission-for-template)):

### Import template

1. On the top menu bar, select **Import template** menu.
2. In **Create template** pane,select **Browse** to select the template file, upload it to Fraud Protection portal.
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
