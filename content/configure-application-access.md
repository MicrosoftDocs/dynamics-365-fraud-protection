---
author: swasif
description: This article explains how to create and configure API roles for Microsoft Entra applications
ms.author: josaw
ms.date: 08/28/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Configure application access
---

# Configure application access

In Microsoft Dynamics 365 Fraud Protection, administrators can also grant API roles to Microsoft Entra Applications through the **Application access** section on the **Access control** page. For more information about the available roles, see [User roles and access](user-roles-access.md) . 

You can assign API roles to a new Microsoft Entra application or an existing applications. 

### Create new Entra App

You can assign API roles to an Entra App during the application creation process as follows:

1. From the **+ Assign application role(s)** drop-down, on the top navigation, select **Create new application**, and then fill in the fields to create your app. The following fields are required:

    - **Application display name** – Enter a descriptive name for your app. The maximum length is 93 characters.
    - **Authentication method** – Select whether a certificate or a secret (password protected) is used for authentication.
    
      - Select **Certificate**, and then select **Choose file** to upload the public key. When you acquire tokens, you will need the matching private key.
      - Select **Secret** to automatically generate a password after the application has been created.

2.	Select the API roles you want to assign to this application from the **Roles** drop-down at the bottom. There are two API roles to choose from. Risk_API role is selected by default. 
  - **Risk_API**: Entra applications assigned Risk_API roles can call DFP assessment and observation events API endpoints.
  - **Provisioning_API**: Entra applications assigned Provisioning_API roles can call DFP Provisioning API endpoint allowing creation, update, and deletion of non-root environments.  

> [!Note]
> API roles can be edited at any time.

3.	When you've finished filling in the fields, select **Create application**.

The confirmation page summarizes the app's name and ID, and either the certificate thumbprint or the secret, depending on the authentication method that you selected.


### Assign API role to an existing Entra application

You can also assign API roles for an existing Entra application in your Azure tenant. To assign or edit API roles for an existing app, please follow the steps below: 

1.	From the **+ Assign application role(s)** drop-down, on the top navigation, select **Existing application**, and enter application name or ID to search for the existing application. 
2.	The Roles drop down will show the assigned API roles pre-selected. You can change the selection as needed and click on **Assign role(s)** button at the bottom of the pane to update the assigned roles.

> [!Note]
> **Assign role(s)** button will be enabled only when the API role assignment selection has been changed. If no changes are made, the button will remain disabled. 

### Edit or Revoke access of existing Entra applications

To edit or revoke access of an existing Entra application, you can select the application from the list and click on **Edit** or **Revoke access** from the top navigation. You can select multiple applications from the list to revoke access in bulk. 
