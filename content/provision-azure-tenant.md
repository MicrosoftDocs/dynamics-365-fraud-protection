---
author: yvonnedeq
description: This topic explains how to provision an Azure tenant for use with Microsoft Dynamics 365 Fraud Protection.
ms.author: v-madeq
ms.date: 04/02/2021
ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Create and provision your Azure tenant
---

# Create and provision your Azure tenant

An Azure tenant represents an organization within Microsoft Azure Active Directory (Azure AD). It is a dedicated instance of the Azure AD service that an organization receives and owns when it signs up for a Microsoft cloud service such as Azure, Microsoft Intune, or Microsoft 365. Essentially, an Azure tenant is a way to manage user access to Azure resources to ensure you control access to your data.

You can use either of the following approaches to provision your Azure tenant for use with Microsoft Dynamics 365 Fraud Protection:

- [Provision your existing Azure tenant](provision-azure-tenant.md#provision-your-existing-azure-tenant).
- [Create and provision a new tenant in Azure AD](provision-azure-tenant.md#create-and-provision-a-new-tenant-in-azure-ad).

If you are unsure if your company already has an Azure tenant, see the note in the [Create and provision a new tenant in Azure AD](provision-azure-tenant.md#create-and-provision-a-new-tenant-in-azure-ad) section for help.

You will need Azure tenant administrator permissions to complete provisioning. If you don't have an admin account, contact the tenant admin in your organization for support.

> [!NOTE]
>  Due to limitations migrating data between tenants, we recommend you select the tenant approach you would use if Fraud Protection were being used in production, which will avoid additional steps at a later stage.

## Provision your existing Azure tenant

If your company already has an Azure tenant and you are an administrator, sign in to Fraud Protection using your company email address. On successful validation, the Fraud Protection service will be provisioned for your Azure tenant, and you can [configure access for other users](configure-user-access.md) and begin [integrating your systems with the Dynamics 365 Fraud Protection APIs](integrate-real-time-api.md).

You will be prompted for a tenant if there is no Azure tenant for your organization or if you are not an administrator for your existing tenant. If you need to configure a new tenant, see the instructions in the [Create and provision a new tenant in Azure AD](provision-azure-tenant.md#create-and-provision-a-new-tenant-in-azure-ad) section. If you have a tenant but do not have sufficient administrative privileges, contact your existing administrator for access.

## Create and provision a new tenant in Azure AD

To create and provision a new Azure tenant, follow the steps in [Quickstart: Create a new tenant in Azure Active Directory](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).

> [!NOTE]
> When you create your user ID, enter both your user name and company name. You cannot change the company name after it has been created. If a message appears stating that your company name is not available, this means your company already has an Azure tenant. Use that Azure tenant by following the steps under the "Provision your existing Azure tenant" topic. 

After you've signed up, you can proceed to configuring user access to Fraud Protection. For more information, see [Configure user access to Dynamics 365 Fraud Protection](configure-user-access.md).

After configuring access to users, integrate your existing systems with the Fraud Protection real-time application programming interfaces (APIs). For more information, see [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md).


[!INCLUDE[footer-include](includes/footer-banner.md)]
