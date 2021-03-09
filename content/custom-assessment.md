---
author: yvonnedeq
description: This topic provides information about custom assessments, and explains how to create and define them.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 07/07/2020

ms.topic: conceptual
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - admin
title: Custom assessment

---

# Custom assessment

## Overview

Effective fraud management is a multi-tier strategy. To maximize fraud detection and minimize customer friction, you must assess interactions at various phases of a user's journey, and decide whether the interactions should be allowed, challenged, or prevented. Every business is different, and so are the associated user interactions that transmit signals about potential fraud. For example, profile updates, such as changes to a user's address or payment information, might be a key event for an e-commerce business. Other examples of user interactions that might be key events, depending on the business model, include submission of reviews, updates of seat preferences on a travel site, the addition of family and friends on a subscription or gaming service, and submission of a service support ticket or a complaint.

Microsoft understands the importance of including these types of business-specific events to help you with your overall fraud management strategy. Therefore, Microsoft Dynamics 365 Fraud Protection now lets you add *custom assessments* in addition to the common assessment events, such as account creation, account login, and purchase protection events. You can create and define a custom assessment, including its name, the API path, and a payload that is appropriate to the specific event. You can then configure rules that the assessment uses to return a decision, such as **Approve**, **Reject**, **Review**, or **Challenge**.

## Create an assessment

When you've determined the specific *event* that you want to assess and the *data* that you want to include, you can quickly create a new custom assessment in the API. 

1. In the [Fraud Protection](https://dfp.microsoft.com/) portal, in the left navigation, select **Custom assessments**.
1. Select **New assessment**.
1. Enter a friendly name for the assessment.

    The friendly name is a name that helps users easily refer to the event. You can use it to refer to the event on other pages.

1. Enter an API name.

    The API name is the name of the API that you include in API calls to receive assessment decisions in real time. The API path is automatically entered and shown when you enter the API name.

1. Update the sample payload.

    The default sample payload is a recommended schema payload that resembles the API schema for an account profile update event. You can edit the payload and add any custom property that you plan to include in your API calls. This sample payload serves as a reference when you create rules for the assessment.

## Call the custom assessment API

For detailed information about how to integrate with the API, see [Integrate account protection APIs](./integrate-ap-api.md).

When you integrate with the API, make sure that you use the URI information that is provided is the API path in step 4 in the previous section. The payload must include **name: \<API name\>**, where **API name** is the name that you entered in step 4.

> [!NOTE]
> At least one active rule must be created for an assessment. Otherwise, the associated API calls can't be successfully completed. For detailed information about how to create rules, see [Manage rules](rules.md).

## Edit an assessment

At any time, you can change the name, API name, or sample payload for an assessment that you've created. Changes that you make to the sample payload are reflected in the rules that are created after you save those changes.

> [!NOTE]
> If you change the API name, you must make the same change in all your API calls. Otherwise, the API calls can't be resolved and will fail.

1. In the [Fraud Protection](https://dfp.microsoft.com/) portal, in the left navigation, select **Custom assessments**.

    All your current custom assessments are listed.

1. Select the assessment to edit, and then select **Edit**.

    The **Edit assessment** page appears.

1. Make the required changes, and then select **Save**.

    The changes take effect as soon as they are saved. If you changed the API name, we recommend that you pause the API calls, incorporate the change into the API payload in the Fraud Protection portal, and then restart the API calls.

## Delete an assessment

Currently, you can create up to three distinct assessments under custom assessments. If your business priorities or user scenarios have changed, and you no longer want to use an assessment that you've created, you can delete it.

> [!NOTE]
> If you delete an assessment, the rules and scorecard that are associated with it are also deleted and can't be restored. If you continue to make API calls that use the name of the deleted assessment, the API calls can't be resolved and will fail.

1. In the [Fraud Protection](https://dfp.microsoft.com/) portal, in the left navigation, select **Custom assessments**.

    All your current custom assessments are listed.

1. Select the assessment to delete, and then select **Delete**. 
1. Select **Delete** again to confirm that you want to delete the assessment, and then select **Save**.

    The change takes effect as soon as it's saved.

## Related topics

- [Account protection overview](ap-overview.md)
- [Manage lists](lists.md)
- [Manage rules](rules.md)
- [Learn from the account protection scorecard](ap-scorecard.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]