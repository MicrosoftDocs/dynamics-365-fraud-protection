---
author: jackwi111
description: This topic explains how to sign up for Microsoft Dynamics 365 Fraud Protection.
ms.author: v-jowigh
ms.service: crm-online
ms.date: 04/22/2019

ms.topic: conceptual
title: Sign up for Dynamics 365 Fraud Protection
---

# Sign up for Dynamics 365 Fraud Protection

You can discover the value of Microsoft Dynamics 365 Fraud Protection by using a public preview that shows how the product can help protect your business and your customers.

> [!IMPORTANT]
> Before you set up your environment for Dynamics 365 Fraud Protection, we recommend that you be familiar with [Microsoft Azure Cloud Computing Platform and Services](https://azure.microsoft.com/).

To begin, go to the [Dynamics 365 Fraud Protection preview page](https://go.microsoft.com/fwlink/?linkid=2085136), select **Request Preview**, and then complete the request form.

When you qualify for the preview, you will receive an email that includes a link and sign-up instructions. Select the link and complete the sign-up forms to create your Dynamics 365 Fraud Protection account.

## Provision your Azure tenant

An Azure tenant represents an organization within Azure Active Directory (Azure AD). It is a dedicated instance of the Azure AD service that an organization receives and owns when it signs up for a Microsoft cloud service such as Azure, Microsoft Intune, or Office 365. Essentially, an Azure tenant is a way to control user access to Azure resources to ensure you control access to your data. 

During sign-up for Dynamics 365 Fraud Protection, you can use either of the following approaches:

- Provision your existing Azure tenant.
- [Create and provision a new tenant in Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).

> [!NOTE]
> To sign up with an existing Azure tenant, you will need Azure tenant administrator permissions. If you are unsure if your company already has an Azure tenant, see [Create and provision a new tenant in Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant), and follow the steps.

> If your account has Azure tenant administrator permissions, see "Provision your existing Azure tenant" topic, and follow the steps. If no Azure tenant exists, to continue with the sign-up process, contact the individual in your organization with Azure tenant administrator permissions for support. Due to limitations migrating data between tenants, we recommend you select the tenant approach you would use if Dynamics 365 Fraud Protection were in production, which will avoid additional steps at a later stage.

### Provision your exiting Azure tenant

If your company already has an Azure tenant, add Dynamics 365 Fraud Protection to it. This enables access for the product to be managed centrally by your IT organization.

1. Click the sign-up link included in your **Welcome** email.
2. On the **Welcome** page, click **Sign in**.
3. On the **Sign in** page, enter your company email address.

After you've signed in, links for the Diagnose experience appear in Dynamics 365 Fraud Protection. Before you access the Diagnose experience, you must configure user access to Dynamics 365 Fraud Protection. For instructions, see the "Configure users in Dynamics 365 Fraud Protection" topic in [Configure user access](configure-user-access.md).

After configuing access to users, integrate your existing systems with the Dynamics 365 Fraud Protection real-time application programming interfaces (APIs). See [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md), and follow the steps.

### Create and provision a new tenant in Microsoft Azure Active Directory

To create and provision a new Azure tenant, see [Create and provision a new tenant in Microsoft Azure Active Directory (Azure AD)](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant), and follow the steps.

> [!NOTE]
> When creating your user ID, enter both your username and company name. You cannot change the company name after it has been created. If a message appears stating that your company name is not available, this means your company already has an Azure tenant. Use that Azure tenant by following the steps under "Provision your existing Azure tenant" topic. 

After you've signed up, links for the Diagnose experience appear in Dynamics 365 Fraud Protection. Before you access the Diagnose experience, you must configure user access to Dynamics 365 Fraud Protection. For instructions, see the "Configure users in Dynamics 365 Fraud Protection" topic in [Configure user access](configure-user-access.md).

After configuing access to users, integrate your existing systems with the Dynamics 365 Fraud Protection real-time application programming interfaces (APIs). See [Integrate Dynamics 365 Fraud Protection real-time APIs](integrate-real-time-api.md), and follow the steps.

## Review legal agreements

Microsoft is committed to preserving the privacy of your business, customer, and data. We recommend that you review the [Microsoft Privacy Statement](https://privacy.microsoft.com/privacystatement), [data subject request information](https://www.microsoft.com/trustcenter/privacy/gdpr/gdpr-overview), and [Terms of Use](https://www.microsoft.com/en-us/legal/intellectualproperty/copyright/default.aspx).
