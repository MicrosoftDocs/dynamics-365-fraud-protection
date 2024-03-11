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
- Case management configuration.

> [!NOTE]
> The following resources aren't included in the assessment template:
> - Decision rules and post-decision actions in nonproduction branches.
> - Case management queues and routing rules.
> - Draft (unpublished) rules.
> - Dependent resources for rules (for example, velocities or external calls).


### Environment template

Environment template subresources include:

-	Assessment application programming interface (API) attributes, labels, and observation events.
-	Published decision rules and post-decision actions in the production branch.
-	Assessment configurations and settings.
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
> - Case management queues and routing rules.
> - List data (list name and columns are included).
> - User permission data.
> - Child environments and hierarchy structure.
> - Application ID, device fingerprint certificate, and event tracing.
> - Tab settings.
> - Custom assessment (legacy)*
> - Client-side integration
>
> - *If the environment contains custom assessment (legacy), you will not be able to create a template from the environment. Please remove the custom assessment (legacy) and try again.

## Create a template

You can create a template from the supported resources in your Fraud Protection portal. 

> [!NOTE]
> In a multi-hierarchy tenant, templates created in an environment are accessible to its children environments. For more information, see [Multi-hierarchy for templates](templates.md#view-and-manage-templates-in-parent-environments) for details.

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
>
> - If the environment contains custom assessment (legacy), you will not be able to create a template from the environment. Please remove the custom assessment (legacy) and try again.

## Create new resources using templates

### Create a new decision rule or post-decision action from a template

To create a new decision rule or post-decision action from a template, follow these steps.

1. In the Fraud Protection portal, go to **Fraud assessments**, select the assessment, and then select the **Rules** tab.
1. On the top menu bar, select **+ New rule**, and then select **From template** from the drop-down menu.
1. On **New rule** pane, select one of the following from the **Template** drop-down menu:
   - Select **Load template file** to use a template file on your computer to create the new rule. Select **Browse** to select the template file, and then upload it to the Fraud Protection portal.
   - Select a template if you want to use a template already created in Fraud Protection portal.
1. Enter a **Name** and **Description** for the new rule.
1. Preview the template to view the list of resources included in the template.
1. Select **Create** to create a new draft rule that matches the contents of the template.
1. Select **Publish** to publish the rule.

> [!NOTE]
> If the rule has a reference to another resource that isn't found in the environment (for example, a velocity, external call or function), you must resolve the missing reference before you can publish the draft rule. 

### Create a new assessment from a template

To create a new assessment from a template, follow these steps.

1. In the Fraud Protection portal, on the left navigation pane, select **Fraud assessments**, and then select **+ New assessment**.
1. In the **Assessment setup** wizard, select **Customer created template** from the available schema templates.
1. On the **Customer created templates** pane, select one of the following from the **Template** drop-down menu:
   - Select **Load template file** to use a template file on your computer to create the new rule. Select **Browse** to select the template file and upload it to the Fraud Protection portal.
   - Select a template if you want to use a template already created in Fraud Protection portal.
1. Preview the template to view the sample code and resources included in the assessment template. Select **Select** to proceed.
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
6. Enter or edit the **Data storage geography**, **Name**, **Description**, **Tags**, **Azure Entra ID**, and **Customer API ID** settings you want to use for the new environment.
7. Select **Create** to create the new environment that matches the resources of your template.

> [!NOTE]
> The **Data storage geography** setting can only be edited if a root environment is being created using the template. When creating child environments, the data storage geography is always the same as the root environment under which the child environment is being created, which may be different from the data storage geography of the source environment from which the template was created.
> 
> If the environment template contains a sub-resource that has missing dependencies (for example, a velocity, external call or function) or duplicated name with existing resources (for example, an exernal call that has duplicated name with a parent external call), the environment creation will fail. If you run into this issue, please remove the decision rule or post-decision action that reference to the missing dependency, and/or remove the external call with duplicated name and try again.

### Partial success when creating assessment using template

> [!NOTE]
> If the assessment template contains a sub-resource that has missing dependencies (for example, a velocity external call or function), the assessment creation will be partially successful. This means some of the assessment definition, and some sub-resources are successfully created but some settings and sub-resources are not created successfully. If you run into this issue, please remove the decision rule or post-decision action that reference to the missing dependency and try again.

## Template library

Templates created or imported in the current environment are visible in the template library page, which you can access in the left navigation under pane under **Data**.

You can perform the following actions on templates. For more information, see [User permission for templates](templates.md#user-permissions-for-templates).

### Import template

To import a template, follow these steps.

1. On the top menu bar, select **Import template**.
2. On the **Create template** pane, select **Browse** to select the template file and upload it to Fraud Protection portal.
3. Enter the **Name** and **Description** of the imported template.
4. Select **Create** to import the template and make it available in template library.

### Edit template

To edit a template, follow these steps.

1. On the overflow menu of the template, select **Edit**.
1. Enter the **Name** and **Description** of the template.
1. Select **Update** to save your changes.

### Export template

To export a template, do the following.

1. On the overflow menu of the template, select **Export** to download the template file to your computer. This template can be imported back into Fraud Protection at a later time.

### Delete template

To delete a template, follow these steps.

1. In the overflow menu of the template, select **Delete** in the menu.
1. Select **Delete** in the confirmation dialog to delete the template permanently. This operation can't be undone.

## Template limits

Fraud Protection has a limit on the numbers of templates that can be created per environment, as shown in the following table.

  | Template type | Limit | 
  |----------|---------------|  
  | Maximum number of rule templates within an environment | 50 |  
  | Maximum number of assessment templates within an environment | 20 |  
  | Maximum number of environment templates within an environment | 10 |  

## View and manage templates in parent environments

In the template library for your current environment, you can only view and manage the templates created in that environment. However, if there are templates created in a parent environment to the current environment, you can view and select those templates from the **Template** drop-down menu in the **Create** resource flow. In other words, users in child environments can create new resources using templates from parent environments.

## User permissions for templates

For information on user permissions, see [User role and access](user-roles-access.md) and [Payment service provider user roles and access](psp-user-roles.md)
