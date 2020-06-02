---
author: yvonnedeq
description: This topic provides information about creating and defining custom assessments.
ms.author: v-madeq
ms.service: fraud-protection
ms.date: 06/02/2020

ms.topic: conceptual
search.app: 
  - FraudProtection
search.audienceType:
  - admin
title: Custom assessment


---

# Custom assessment

## Overview

Effectively managing fraud is a multi-tiered strategy. In order to effectively maximize fraud detection and minimize customer friction, interactions at various phases of a user’s journey must be assessed and decisions must be made whether to allow, challenge, or block the user from proceeding further. Each business model is different and so are the associated user interactions that transmit signals about potential fraud. Profile updates such as address change or payment information change may be a key event for an e-commerce business while submission of reviews might be for another. Updating a seat preference on a travel site, adding family and friends on a subscription or gaming service, raising a support ticket, or submitting a complaint are other examples of user events which are specific to each business model.

Microsoft Dynamics 365 Fraud Protection understands the importance of including these types of business-specific events to help you in the overall fraud management strategy, and now offers the ability to add *custom assessments* in addition to the common assessment events such as account creation, account login, and purchase protection.
With custom assessments, you can create and define an assessment, including its name, the API path, and a payload that is appropriate to the specific event. You can then use the same assessment to make decisions on other events.

## Create assessments

You can quickly create a new custom assessment when you’ve decided on the specific *event* you want to assess, and the *data* you want to include, in the API. 

#### To create a new assessment:

1.	In the [Fraud Protection]( https://nam06.safelinks.protection.outlook.com/?url=https%3A%2F%2Fdfp.microsoft.com%2F&data=02%7C01%7Cv-madeq%40microsoft.com%7C86e8b55e29fd42e1c32508d806c77c4c%7C72f988bf86f141af91ab2d7cd011db47%7C1%7C0%7C637266801155879313&sdata=ildJrF5HjZLm3iUmRDEkA09BCEtiTvGDMhRJIglVFB8%3D&reserved=0) portal, select **Custom assessment link** on the left navigation.

1.	Select **Create assessment**.

1.	Enter a friendly name for the assessment. 

    This is the name you can use to refer to the event in additional pages, and a name that helps users easily refer to the event. 

1.	Enter an API name. 

    This defines the name of the API that you include in the API call to receive assessment decisions in real-time. The API path is automatically populated and displayed when you enter the API name.

1.	Update the sample payload. 

    As a starting point, the sample payload section is updated with the suggested API schema for an account profile update event. You can edit the payload and add any custom property bag that you include in your API call. This sample payload is used to provide a reference when you’re creating rules after the assessment is created.

## Call the custom assessment API

For detailed information on integrating with the API, see [Integrate Account Protection API](https://docs.microsoft.com/dynamics365/fraud-protection/integrate-ap-api).

When you integrate with the API, make sure you use the URI information you provided under the API path in step 4 in the previous section.

## Edit assessments

You can change the name, API name, or the sample payload for an assessment you’ve created at any time. Note that if you change the API name, you must make the same change in all your API calls as well, otherwise the API call will be unable to resolve and fail. Any changes made to the sample payload are reflected in the rules created after the change is saved. 

#### To edit an assessment:

1.	Select **Custom assessment**.

    All your current custom assessments are listed on this page.

1.	Select the assessment you want to edit and then select **Edit**. 

    This displays the **Edit assessment** window.
1.	Make the required changes and then select **Save**. 

    The changes are effective as soon as they are saved. If you've made changes to the API name, we recommend that you pause the API calls, make the changes on the Fraud Protection portal, and then restart the API call with the changes incorporated in the API payload.

## Related topics

- [Account protection overview](ap-overview.md)
- [Manage lists](lists.md)
- [Manage rules](rules.md)
- [Learn from the account protection scorecard](ap-scorecard.md)
