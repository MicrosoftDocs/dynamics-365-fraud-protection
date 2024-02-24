---
author: zhuoche
description: This article explains how to create and use templates in Microsoft Dynamics 365 Fraud Protection.
ms.author: zhuoche
ms.date: 02/22/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Templates 
---

# Templates

## What is template?
Templates allow you to save resources (e.g. decision rules, post-decision actions, etc) and configuration (e.g. assessment configuration, Case Management configuration, etc) from your Dynamics 365 Fraud Protection portal. You can templatize multiple sub-resources together so that you can create them in a new environment or tenant without manually configurating each resource. 

Templates can be created from a resource in your Fraud Protection tenant, and downloaded to your computer as template files, or saved in template library where they will be available to be used later. 

You can create a new resource from a template file or browse from the available templates in your environment. After you upload the template file or select a template from the library, you will have the capability to preview what resources and sub-resources are contained in the template. 

> [!NOTE]
> The newly created resource and sub-resources will be in the same state when the template was created. Any changes happened after the template being created will not be applied. 


## Use cases of templates

There are many use cases and scenarios where templates can be beneficial. 

When financial institutions and payment servicer provier customers are onboarding new client, they would like to save certain resources as templates so they can easily set up similar configuration by applying the template. When merchants are making changes to existing environment, they would like to test the change in sandbox environment first, and promote the changes to production environment by exporting the template from sandbox and importing into the production environment. Users can save a rule as template so they can duplicate them in another assessment or environment. Templates can help users to share their environment or assessment configuration across environments and tenants, which greatly reduces the time to onboarding and reduce human error and manual labor during the process. 

## Types of templates
In Fraud Protection, we support the following types of templates:

### Rule template
- Published decision rules and post-decision actions in production branch
> [!NOTE]
> Rule template does not support decision rules and post-decision actions in shadowing branches. 

###	Assessment template
Sub-resources included:
- Assessment API attributes, labels and observation events
- Published decision rules and post-decision actions in production branch
- Assessment configuration and settings
- Case management queues and routing rules
- Case management configuration

> [!NOTE]
> Assessment template does not support decision rules and post-decision actions in shadowing branches. 

### Environment template
Sub-resources included:
-	Assessment API attributes, labels and observation events
-	Published decision rules and post-decision actions in production branch
-	Assessment configuration and settings
-	Case management queues and routing rules
-	Case management configuration
-	Velocities
-	List metadata without list data
-	External calls
-	External assessments
-	Functions
-	Environment metadata (e.g. name, description, geolocation, etc)

> [!NOTE]
> Environment template does not support decision rules and post-decision actions in shadowing branches.
> In template list name and columns are included, but list will be empty without any data. 

## Create template

You can create a template from the supported resources in your Fraud Protection portal. 

> [!NOTE]
> templates created in the environment will be accessible to its children environments, users in the children environments may create new resources using the template from parent environment.

### Create rule template
1. In Fraud Protectin portal, navigate to Fraud assessments, select the assessment and go to **Rules** tab.
2. click the overflow icon for a published rule that you want to templatize, select **Create template** in the menu options.
3. In **Create template** panel, type the **Name** of the template you want to use.
4. The preview section of the panel will show the list of clauses included in the rule template you are going to create.
5. You have the option to **Create template and download** or **Create template and add to library**.
   - **Create template and download** will download a tempplate file to your computer that can be imported into Fraud Protection later.
   - **Create template and add to library** will create the template and make it available to users in the Fraud Protection environment and its children environment. If you choose this option, you can give your template a **Description** for reference.
6. Click **Download** button to download template file, or click **Add template** button to add template in your Fraud Protection environment.

### Create assessment template
1. In Fraud Protectin portal, navigate to Fraud assessments, select the assessment that you want to templatize.
2. Go to **Configuration** tab, select **Create template** in the top menu bar.
3. In **Create template** panel, type the **Name** of the template you want to use.
4. The preview section of the panel will show the list of resources included in the assessment template you are going to create.
5. You have the option to **Create template and download** or **Create template and add to library**.
   - **Create template and download** will download a tempplate file to your computer that can be imported into Fraud Protection later.
   - **Create template and add to library** will create the template and make it available to users in the Fraud Protection environment and its children environment. If you choose this option, you can give your template a **Description** for reference.
6. Click **Download** button to download template file, or click **Add template** button to add template in your Fraud Protection environment.

### Create environment template
1. In Fraud Protectin portal, use the **environment switcher** on the top menu bar, go to **Manage environments**.
2. Go to the environment that you want to templatize, click the overflow icon, select **Create template** in the menu.
3. In **Create template** panel, type the **Name** of the template you want to use.
4. The preview section of the panel will show the list of resources included in the environment template you are going to create.
5. You have the option to **Create template and download** or **Create template and add to library**.
   - **Create template and download** will download a tempplate file to your computer that can be imported into Fraud Protection later.
   - **Create template and add to library** will create the template and make it available to users in the Fraud Protection environment and its children environment. If you choose this option, you can give your template a **Description** for reference.
6. Click **Download** button to download template file, or click **Add template** button to add template in your Fraud Protection environment.

> [!NOTE]
> Template is created within the environment that user is currently navigated to. If user creates a template from another environment, the template will be available to the current environment and its children environments.
> 
> If the system runs into error when creating the sub-resources, the creation process will abort and some sub-resources or configuration will be missing from the newly created resource.
> 
> Modify the content of the downloaded template file may cause the template to be invalid or system error when importing the file to Fraud Protection portal.
> 
> Template file has a maximum size limit of 20MB.

## Use template to create new resources

### New rule from template
1. In Fraud Protectin portal, navigate to Fraud assessments, select the assessment and go to **Rules** tab.
2. In the top menu bar, select **+ New rule** and then choose **From template** in the drop down menu.
3. In **New rule** panel, you will see a drop down menu for **Template**.
   - If you want to use template file in your computer to create the new rule, choose the option to **Load template file**. Click the **Browse** button to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** drop down menu.
4. You can give the **Name** and **Description** you want to use for the new rule.
5. The preview section of the panel will show the list of clauses included in the rule template you are using.
6. Click **Create** button to create the new rule.
7. The new rule will be created as a draft rule, you can now publish the rule.

### New assessment from template
1. In Fraud Protectin portal, navigate to Fraud assessments on the left navigation, click **+ New assessment** from the navigation menu.
2. In **Assessment setup wizard**, select **Customer created template** from the available schema templates.
3. In **Customer created templates** pop-up modal, you will see a list for **Template**.
   - If you want to use template file in your computer to create the new rule, choose the option to **Load template file**. Click the **Browse** button to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** list.
4. The preview section of the modal will show the sample code and resources included in the assessment template you are using. Click **Select** to proceed.
5. Specify the **Friendly name** and **API name** you want to use for the new assessment.
6. Click **Create assessment** button to create the new assessment.
7. The new assessment will be created with the resources from your template.

### New environment from template
1. In Fraud Protectin portal, use the **environment switcher** on the top menu bar, go to **Manage environments**.
2. If you want to create a root environment from template, click **+ New environment** from the top menu bar. If you want to create a child environment from template, in the overflow menu of the environment, click **New child environment** in the menu.
3. In **New environment** panel, click the toggle to turn on **Use template**, you will see a drop dwn menu for **Template**.
   - If you want to use template file in your computer to create the new rule, choose the option to **Load template file**. Click the **Browse** button to select the template file, upload it to Fraud Protection portal.
   - If you want to use template created in Fraud Protection portal, select the template you want to use from the **Template** list.
4. The preview section of the panel will show the resources included in the environment template you are using. 
5. You can edit the **Data storage geography**, **Name**, **Description**, **Tags**, **Azure AD application ID** and **Customer API ID** you want to use for the new environment.
6. Click **Create** button to create the new environment.
7. The new environment will be created with the resources from your template.

> [!NOTE]
> **Data storage geography** is only editable for creating root environment, child environment will always follow its parent environment's storage geography.

## Template library
Template created by users will be available in template library. You can navigate to the template library under **Data** menu on the left navigation. You can perform the following actions on templates.

You can view the following information for templates:
- Name
- Description
- Updated by
- Updated on


### Import template
1. On the top menu bar, click **Import template** menu.
2. In **Create template** panel, click the **Browse** button to select the template file, upload it to Fraud Protection portal.
3. You can give the **Name** and **Description** you want to use for the imported template.
4. Click **Create** button, the template will be imported and will be available in template library.

### Edit template
1. In the overflow menu of the template, click **Edit** in the menu.
2. You can edit the **Name** and **Description** for the template.
3. Click **Update** button to save your changes.

### Export template
1. In the overflow menu of the template, click **Export** in the menu.
2. The exported template file will be downloaded to your computer that can be imported into Fraud Protection later.

### Delete template
1. In the overflow menu of the template, click **Delete** in the menu.
2. Click **Delete** in the confirmation dialog. The template and its associated data will be deleted permanently.

## Template limits
Fraud Protection has a limit on the numbers of templates that can be created per environment. The below are the limits

  | Template type | Limit | 
  |----------|---------------|  
  | Maximum number of rule templates within an environment | 50 |  
  | Maximum number of assessment templates within an environment | 20 |  
  | Maximum number of environment templates within an environment | 10 |  


## User permission for template
For user permission, reference [User role and access](user-roles-access.md) and [Payment service provider user roles and access](psp-user-roles.md)
