---
author: cschlegel2
description: This article explains how to set up Microsoft Dynamics 365 Purchase Protection.
ms.author: cschlegel
ms.date: 12/13/2024
ms.topic: reference
search.audienceType:
  - Developer, IT PRO, Fraud Manager
title: Set up Purchase Protection
ms.custom:
---


# Set up Purchase Protection

This article provides an overview of the process for setting up Purchase Protection functionality in Microsoft Dynamics 365 Fraud Protection. To help you get started, we've provided a list of steps together with links to related onboarding and integration documents for quick reference. Use the following links to go through the provisioning, integration, and key features:

1. [Understand how Purchase Protection works](#understand)
2. [Onboarding planning and implementation milestones](#onboard)
3. [Provision Fraud Protection in INT (sandbox) and production environments](#provision)
4. [Configure user access and assign roles](#configure)
5. [Review the APIs and data mapping](#review)
6. [Integrate Purchase Protection APIs](#purchase)
7. [Integrate device fingerprinting](#device)
8. [Test and validate](#test)
9. [Set up continuous operations and features](#continuous)

## Prerequisites

Before you set up Purchase Protection, you must set up Dynamics 365 Fraud Protection. To set up Fraud Protection and control user access to your data, you must have a Microsoft Entra tenant. If you don't already have an Microsoft Entra tenant, contact your authorized Microsoft seller or partner to sign up for one. Before you can install Fraud Protection, an authorized Microsoft seller or partner must provide a promotion code to you. If you don't have a promotion code, contact your authorized Microsoft seller or partner. To learn more about Fraud Protection, and about the capabilities of Purchase Protection, Account Protection, and Loss Prevention, see the [Dynamics 365 Fraud Protection home page](index.md).

## <a name="understand"></a>1. Understand how Purchase Protection works

To learn how Purchase Protection interacts with different entities, such as customers and banks, see [How purchase protection works](how-pp-works.md). This article also highlights Purchase Protection capabilities and APIs to help you better understand risk assessment interactions.

## <a name="onboard"></a>2. Onboarding planning and implementation milestones for Purchase Protection

Onboarding planning helps you understand and plan for the project implementation milestones of Purchase Protection integration and onboarding. To learn more, see [Onboarding planning](pp-onboarding-planning-guide.md).

## <a name="provision"></a>3. Provision Fraud Protection in INT (sandbox) and production environments

Fraud Protection is provisioned in an Microsoft Entra tenant. You can provision it in your existing Microsoft Entra tenant or a new Microsoft Entra tenant. To learn more, refer to [Set up a purchased instance of Fraud Protection](promocode-set-up-dfp-purchased-version.md).

Fraud Protection gives you the option to create multiple environments and lets you customize the setup in a way that meets your specific needs. This feature gives you the flexibility to establish a hierarchy that's suitable for your requirements. To learn more, see [Manage environments](manage-psp-environments.md).

## <a name="configure"></a>4. Configure user access and assign roles

You can grant users different levels of access to the service, based on logical or functional roles. To learn more about user roles and access, and how to configure them, see the following articles:

- [Configure user roles and access](configure-user-access.md)
- [User roles and access](user-roles-access.md)
- [Payment service provider user roles and access](psp-user-roles.md)

## <a name="review"></a>5. Review the APIs and data mapping for Purchase Protection 

Work with your authorized Microsoft partner to confirm that your available data is aligned with our APIs, and that it provides enough information to effectively run machine learning models and generate scores. To learn more, see [Integrate purchase protection APIs](integrate-real-time-api.md) and [Labels API](labels-api.md).

## <a name="purchase"></a>6. Integrate Purchase Protection APIs

Work with your authorized Microsoft partner to confirm that your questions are addressed and the APIs are correctly integrated. To learn more, see [Swagger UI](swagger.md).

## <a name="device"></a>7. Integrate device fingerprinting

Fraud Protection provides sophisticated device fingerprinting functionality that significantly enhances your model scoring. Device fingerprinting can be integrated into either a partner's hosted page or a merchant's webpage. To view our Swagger user interface (UI), where you can visualize and interact with the API's resource, see [Set up device fingerprinting](device-fingerprinting.md).

## <a name="test"></a>8. Test and validate Purchase Protection

As test traffic begins to flow into the sandbox environment, contact your authorized Microsoft partner to confirm that your data is being received. When the validations have been successfully completed, the integration process can proceed to its full implementation in production environments. Inform your authorized Microsoft partner that you've started sending traffic to confirm that the data was received.

## <a name="continuous"></a>9. Set up continuous operations and features

As you begin to set up your Purchase Protection operations and features, you can determine your own unique set of rules and velocities while you use other features as required to best serve the needs of your business.

### Transaction Acceptance Booster

The Transaction Acceptance Booster (TAB) helps you benefit from higher acceptance rates by sharing Transaction Trust Knowledge with banks. To learn more, see [Transaction acceptance booster (TAB)](transaction-acceptance-booster.md).

### Rules

You can create rules that include features such as velocities, lists, external calls, and Fraud Protection model scores to make decisions. To learn more about rules, see [Manage rules](rules.md).

### Velocities

Velocity checks help you identify several types of event patterns. To learn more, see [Velocity checks](velocities.md).

### Lists

You can use lists to manage the information that you use to fight fraud and enforce business policies. To learn more, see the following articles:

- [Lists Overview](lists-overview.md)
- [Manage support lists](manage-support-lists.md)
- [Manage custom lists](lists.md)

### Search

You can use the search functionality to find and view details about events in Fraud Protection, based on specific filter values. To learn more, see [Search](search.md) and [Risk support](risk-support.md).

### Case management

Use case management to organize and access transactions, specify the level of ambiguity that requires review by human subject matter experts, and provide a feedback loop for the AI-based assessments. To learn more about how to work with case management, see the following articles:

- [Case management overview](case-management-overview.md)
- [Case management for administrators](case-management-administrator.md)
- [Case management for manual reviewers](case-management-manual-review.md)

### Reporting

Reporting is available to show the impact of Fraud Protection on your business. To learn more about reporting, see the following articles:

- [Key metrics](scorecard.md)
- [Virtual fraud analyst](virtual-fraud-analyst.md)
- [Fraud tracker tool](fraud-tracker.md)
- [Long term report](long-term-report.md)
- [Rule performance report](rule-performance-report.md)

### Event tracing and Event Hub

Event tracing lets you track and audit events, and gives you the option to redirect your data to different destinations outside the Fraud Protection Portal. To use vent tracing functionality, you must have a subscription to additional Azure services, such as Event Hubs or Blob Storage. Contact your Microsoft Authorized Seller for details. If you have Azure global administrator credentials, sign in to the [Azure portal](https://ms.portal.azure.com) to determine available subscriptions. To learn more about event tracing and Event Hubs in Fraud Protection, see [Event tracing](event-tracing.md) and [Set up extensibility via Event Hubs](extensibility-via-event-hubs-overview.md).

### External calls

You can use external calls to ingest data from APIs outside Fraud Protection. You can then use that data to make informed decisions in real time. To learn more, see [External calls](external-calls.md).

### Upload historical data into Purchase Protection

You can use data upload capabilities to cold-start models or provide continuous batched data, such as chargebacks. To learn more, see [Upload historical data](data-upload.md).
