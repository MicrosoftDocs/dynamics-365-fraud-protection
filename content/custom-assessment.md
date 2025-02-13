---
author: josaw1
description: This article provides information about custom assessments, and explains how to create and define them.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Custom assessment
---

# Custom assessments

[!include[deprecation](includes/deprecation.md)]

> [!IMPORTANT]
> Custom assessments will be deprecated in a future release of Fraud Protection and will be replaced by the more comprehensive [Assessments](assessment-create-new.md#assessment-wizard-overview) offering. Custom assessments will continue to work and be fully supported until the deprecation date.  Deprecation can take months and this notification is intended to allow you sufficient time to plan and update your implementation of Dynamics 365 Fraud Protection before deprecation. You will be notified when the deprecation date is set.

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
> If you delete an assessment, the rules and monitoring data that are associated with it are also deleted and can't be restored. If you continue to make API calls that use the name of the deleted assessment, the API calls can't be resolved and will fail.

1. In the [Fraud Protection](https://dfp.microsoft.com/) portal, in the left navigation, select **Custom assessments**.

    All your current custom assessments are listed.

1. Select the assessment to delete, and then select **Delete**. 
1. Select **Delete** again to confirm that you want to delete the assessment, and then select **Save**.

    The change takes effect as soon as it's saved.

## Use custom assessments with device fingerprinting

You can use custom assessments with device fingerprinting in Fraud Protection to help protect against several scenarios such as detecting the presence of bots on pages where a user has not been authenticated.

After you implement device fingerprinting on the relevant page in your website or app, use the fingerprinting session ID to retrieve the Fraud Protection bot model score and to access key attributes of a device such as TrueIP or device location. You can use this data to formulate policies that address your fraud protection needs.

To implement custom assessments with device fingerprinting, follow the steps below.

1. To implement device fingerprinting on the relevant pages in your app or website, refer to the appropriate instructions on the following pages.

    - For web pages, see [Web set up of device fingerprinting](df-web.md).

    - For Android apps, see [Fraud Protection mobile SDK for Android](mobile-sdk-android.md).

    - For iOS Apps, see [Fraud Protection mobile SDK for iOS](mobile-sdk-ios.md).

1. Create a custom assessment and a rule by following the steps in the [Custom assessment](custom-assessment.md#create-an-assessment) article. Ensure that the session ID from the device fingerprinting session is included in the payload for your custom assessment.

> [!NOTE]
> The session ID is referred to in this article as "deviceContextId". You can choose any name for this attribute, just be sure you refer to the correct name in the rules.

1. Open the rule you created for custom assessment and select **Edit**.

1. In the **Clauses** section, select **From template** and then select **See all.**

1. Select the **Use device fingerprinting** template and then select **Create.** The **Rules** page opens with two new clauses added. The new clauses contain reference statements that you can modify. If you chose a new name for the device fingerprinting session ID in your payload, replace the "deviceContextId" in the rules with the name that you chose.

1. You can modify the return statement as needed and add or remove clauses to implement the necessary conditions to make a decision. For more information on the fraud query language and other commands that can be used in rules, refer to the [Language reference guide](fpl-lang-ref.md).

1. When you are done editing the rule, select **Publish** and then **Activate**.

1. Finally, [call the custom assessment API](custom-assessment.md#call-the-custom-assessment-api).

> [!NOTE]
> Wait at least two seconds after you initiate the device fingerprinting session to make the custom assessment API call. That way, fingerprinting data can be collected and transmitted, and therefore used within the custom assessment rule execution.


## Related articles

- [Account protection overview](ap-overview.md)
- [Manage lists](lists.md)
- [Manage rules](rules.md)
- [Account protection monitoring dashboards](monitoring-dashboards.md)
- [Account protection schemas](ap-schema.md)


[!INCLUDE[footer-include](includes/footer-banner.md)]
