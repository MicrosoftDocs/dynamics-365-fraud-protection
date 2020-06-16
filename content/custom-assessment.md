---
author: yvonnedeq
description: This topic provides information about creating and defining custom assessments.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/16/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Custom assessment


---

# Custom assessment

## Overview

Effectively managing fraud is a multi-tiered strategy. In order to effectively maximize fraud detection and minimize customer friction, interactions at various phases of a user’s journey must be assessed, and decisions must be made, whether to allow, challenge, or block the user from proceeding further. Each business is different and so are the associated user interactions that transmit signals about potential fraud. Profile updates such as an address change or a payment information change may be a key event for an e-commerce business while submission of reviews might be a key event for another. Updating a seat preference on a travel site, adding family and friends on a subscription or gaming service, submitting a service support ticket or a complaint are other examples of user events which may be key events depending on the business model.

Microsoft Dynamics 365 Fraud Protection understands the importance of including these types of business-specific events to help you with your overall fraud management strategy, and now offers the ability to add *custom assessments* in addition to the common assessment events such as account creation, account login, and purchase protection.
With custom assessments, you can create and define an assessment, including its name, the API path, and a payload that is appropriate to the specific event. You can then configure rules for this assessment to return a decision such as *Approve*, *Reject*, *Review*, or *Challenge*.

## Create assessments

You can quickly create a new custom assessment when you’ve decided on the specific *event* you want to assess, and the *data* you want to include, in the API. 

#### To create a new assessment:

1.	In the [Fraud Protection]( https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Custom assessments** on the left navigation.

1. Select **+new assessment**.

1. Enter a friendly name for the assessment. 

    This is the name you can use to refer to the event in additional pages, and a name that helps users easily refer to the event. 

1. Enter an API name. 

    This is the name of the API that you include in the API call to receive assessment decisions in real-time. As you type, the API name populates the API path and sample payload.

1. Update the sample payload. 

    The sample payload defaults to a suggested schema payload resembling the API schema for an account profile update event. You can edit the payload and add any custom properties that you plan to include in your API calls. This sample payload is used to provide a reference when creating rules for the assessment.

## Call the custom assessment API

For detailed information on integrating with the API, see [Integrate Account Protection API](https://go.microsoft.com/fwlink/?linkid=2132829).

When you integrate with the API, make sure you use the URI information you provided under the API path in step 4 in the previous section. The payload must include `name: <api name>` where the *API name* should match the name you entered in step 4 above.

> [!NOTE]
> For a successful completion of the API call, you must have at least one active rule created for the respective assessment. For detailed information on creating rules, see [Rules](rules.md).

## Edit assessments

You can change the name, API name, or the sample payload for an assessment you’ve created at any time. Note that if you change the API name, you must also make the same change in all your API calls, otherwise the API call will be unable to resolve and will fail. Any changes made to the sample payload are reflected in the rules created after the change is saved. 

#### To edit an assessment:

1. Select **Custom assessments**.

    All your current custom assessments are listed on this page.

1. Select the assessment you want to edit and then select **Edit**. 

    This displays the **Edit assessment** window.
1. Make the required changes and then select **Save**. 

    The changes are effective as soon as they are saved. If you've made changes to the API name, we recommend that you pause the API calls, make the changes on the Fraud Protection portal, and then restart the API call with the changes incorporated in the API payload.

## Delete assessments

Currently you can create up to 3 distinct assessments under custom assessments. If your business priorities or user scenarios have changed and you no longer want to use an assessment you've created , you can delete it.

Note that once you delete an assessment, the rules and scorecard associated with that assessment will be deleted and cannot be revoked. If you continue to make an API call with the deleted assessment name, the API will not resolve and will result in failure.

#### To delete an assessment:

1. Select **Custom assessments**.

    The page displays a list of all your current custom assessments.

1. Select the assessment you want to edit and then select **Delete**. 
1. Select **Delete** again to confirm you want to delete the assessment, and then select **Save**.

    The changes are effective as soon as they are saved.

## Related topics

- [Account protection overview](ap-overview.md)
- [Manage lists](lists.md)
- [Manage rules](rules.md)
- [Learn from the account protection scorecard](ap-scorecard.md)
