---
author: swasif
description: This article explains how to create and configure API roles for Microsoft Entra applications.
ms.author: josaw
ms.date: 08/30/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Configure Microsoft Entra app access
---

# Configure Microsoft Entra app access

[!include[deprecation](includes/deprecation.md)]

In Microsoft Dynamics 365 Fraud Protection, administrators can grant API roles to Microsoft Entra apps through the **Application access** section on the **Access control** page. For more information about the available roles, refer to the [User roles and access](user-roles-access.md) article. 

You can assign API roles to a new or existing Microsoft Entra apps. 

### Create a new Entra app

You can assign API roles to an Entra app during the app creation process.

1. From the **+ Assign application role(s)** drop-down, select **Create new application**, and then fill in the fields to create your app. The following fields are required:

    - **Application display name** – Enter a descriptive name for your app. The maximum length is 93 characters.
    - **Authentication method** – Select whether a certificate or a secret (password protected) is used for authentication.
    
      - Select **Certificate**, and then select **Choose file** to upload the public key. When you acquire tokens, you will need the matching private key.
      - Select **Secret** to automatically generate a password after the app is created.

2.	Select the API roles you want to assign to this app from the **Roles** drop-down. There are two API roles to choose from. Risk_API role is selected by default. 
  - **Risk_API**: Entra apps assigned Risk_API roles can call Fraud Protection assessment and observation events API endpoints.
  - **Provisioning_API**: Entra apsp assigned Provisioning_API roles can call Fraud Protection provisioning API endpoint, which allows the creation, update, and deletion of non-root environments.  

> [!NOTE]
> You can edit API roles at any time.

3.	When you've completed filling in the fields, select **Create application**.

The **Confirmation** page summarizes the app's name and ID, and either the certificate thumbprint or the secret, depending on the authentication method that you selected.


### Assign an API role to an existing Entra app

You can also assign API roles for an existing Entra app in your Azure tenant.

1.	From the **+ Assign application role(s)** drop-down, select **Existing application**, and enter the app name or ID to search for the existing app. 
2.	The **Roles** drop down displays the assigned API roles the are pre-selected. You can change the selection as needed, and select **Assign role(s)** to update the assigned roles.

> [!NOTE]
> **Assign role(s)** is enabled only when the API role assignment selection has been changed. If no changes are made, it remains disabled. 

### Edit or revoke access of existing Entra apps

To edit or revoke access of an existing Entra app, you can select the app from the list and select **Edit** or **Revoke access**. You can select multiple applications from the list to revoke access in bulk. 
