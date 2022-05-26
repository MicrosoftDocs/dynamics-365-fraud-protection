---
author: josaw1
description: This topic provides information that is required for device fingerprinting in a mobile device implementation of Microsoft Dynamics 365 Fraud Protection for React Native.
ms.author: josaw
ms.date: 05/25/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile SDK for React Native
ms.custom:
---

# Dynamics 365 Fraud Protection mobile SDK for React Native

This feature is designed and recommended for use with the Microsoft Dynamics 365 Fraud Protection service. Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI); runs on Azure; and is cloud-scalable and reliable, and has enterprise-grade security. Fraud Protection's device fingerprinting feature enables the identification of devices (for example, computers, Xbox consoles, tablets, and mobile phones) across multiple sessions or interactions that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, it enables Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by instrumenting your React Native application with a Dynamics 365 Fraud Protection software development kit (SDK) for React Native, you agree to the [terms of use for Microsoft application programming interfaces (APIs)](/legal/microsoft-apis/terms-of-use). You also direct Microsoft to process the following types of data from the devices that interact with the Fraud Protection services. (This data is collectively referred to as *device fingerprinting data*.)

- Device attributes, such as the device ID, screen information, the processor, and the class
- Operating system (OS) attributes, such as OS information, the OS version, and original equipment manufacturer (OEM) details
- Applicable browser-related attributes, such as the browser language and installed default apps

You have the following responsibilities:

- Receive consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- Inform your customers about your data collection and processing practices. For example, disclose what data you collect and how it's used.
- Disclose your use of third parties that work on your behalf to process the data that you collect. These third parties include Fraud Protection service providers.
- Comply with all laws and regulations that are applicable to the use of Fraud Protection. These laws and regulations include data protection laws.

## Attribute category introduction reference

The following list shows the device fingerprinting attribute categories that we try to collect and explains how each helps detect fraud. If your organization has specific needs, and you want some categories of data not to be processed by us, reach out to customer support before onboarding. We can help you do the configuration correctly to meet your privacy needs.

- **Core Features** – This group of attributes is core to Fraud Protection's ability to predict patterns of fraud. Based on our previous experience, we believe that these attributes will be highly accretive to Fraud Protection's model performance and ability to discern distinctive patterns of fraud. If these attributes aren't supplied, the device fingerprinting will be inaccurate.
- **Investigative Features** – This group of attributes has the potential to add or enhance Fraud Protection's ability to predict patterns of fraud more accurately. Statistical analysis of collected data is the only definitive way to determine whether these attributes are strong predictors of patterns of fraud. If the predictive capability of these attributes doesn't meet our expectations, we will no longer use them. Although this group of attributes will enable us to determine whether they will be strong predictors of patterns of fraud, they are optional and don't have to be supplied.
- **Potential Label** – This group of attributes is used for model supervision and labeling purposes. There is a probability that each of these attributes, by itself, won't provide ground truth. However, the combination of these attributes increases the likelihood that the label that is used to train Fraud Protection's model will become ground truth and helps improve model performance.

## React Native library technical reference
[![Version](https://img.shields.io/npm/v/@microsoft/fraud-protection.svg)](https://www.npmjs.com/package/@microsoft/fraud-protection)

1. Install library

    from `npm`
    
    ```bash
    npm install @microsoft/fraud-protection --save
    ```

    from `yarn`
    
    ```bash
    yarn add @microsoft/fraud-protection
    ```

2. Link native code

    With autolinking (react-native 0.60+)
    
    ```bash
    cd ios && pod install
    ```

    Pre 0.60
    
    ```bash
    react-native link @microsoft/fraud-protection
    ```

3. You can initiate the SDK by following so it can start to collect device attributes.

    ```javascript
    import RNFraudProtection from '@microsoft/fraud-protection';

    RNFraudProtection.start($tenantId);
    ```

    In this code, **tenantId** is the globally unique identifier (GUID) or universally unique identifier (UUID) that is provided by Microsoft.

4. Send collected device attributes to Microsoft by calling **send()**. You can call **send()** in anywhere before or on the page that has the operation that you need a risk assessment for. For a sign-in/sign-up scenario, you can call **send()** immediately after **start()** call.

    ```javascript
    import RNFraudProtection from '@microsoft/fraud-protection';

    RNFraudProtection.send($pageId); // Or RNFraudProtection.send()
    ```

    In this code, **pageId** is optional and can be set in the following way, depending on the scenario:

    - **SI** – Sign In
    - **SU** – Sign Up
    - **P** – Purchase
    - **tst** – Test

5. Call **getSessionId()** to obtain the **SessionId** value that is required when the risk assessment APIs are called.

    ```javascript
    import RNFraudProtection from '@microsoft/fraud-protection';

    RNFraudProtection.getSessionId((sessionId) => {
        console.log(sessionId)
    });
    ```

### Runtime permissions

The React Native SDK relies on the following native runtime permissions to collect various device data. The SDK doesn't ask for any runtime permissions. The app should obtain these runtime permissions from the user.

- **Android**
    - android.permission.ACCESS\_COARSE\_LOCATION
    - android.permission.READ\_PHONE\_STATE
    - android.permission.BLUETOOTH\_CONNECT

- **iOS**
    - The iOS SDK uses CLLocationManager, and checks for **CLAuthorizationStatus.authorizedAlways** or **CLAuthorizationStatus.authorizedWhenInUse** before it requests location data. The app should obtain **CLLocationManager.requestWhenInUseAuthorization** Or **CLLocationManager.requestAlwaysAuthorization** permission from the user.
    - The iOS SDK uses AppTrackingTransparency and checks for **ATTrackingManager.AuthorizationStatus.authorized** before it collects **AdvertisingId**. The app should obtain **ATTrackingManager.requestTrackingAuthorization** permission from the user.


## Support

To log a support ticket, go to <https://dfp.microsoft.com>. (Global admin permissions are required.)
