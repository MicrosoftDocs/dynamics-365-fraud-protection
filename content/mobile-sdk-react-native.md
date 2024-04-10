---
author: josaw1
description: This topic provides information that is required for device fingerprinting in a mobile device implementation of Microsoft Dynamics 365 Fraud Protection for React Native.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile SDK for React Native
ms.custom:
---

# Dynamics 365 Fraud Protection mobile SDK for React Native

Dynamics 365 Fraud Protection provides a device fingerprinting feature that is designed and recommended for use with the Microsoft Dynamics 365 Fraud Protection service. The device fingerprinting feature is based on artificial intelligence (AI), runs on Azure, is cloud-scalable and reliable, and has enterprise-grade security. It also enables the identification of devices (for example, computers, Xbox consoles, tablets, and mobile phones) across multiple sessions or interactions that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, it enables Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by instrumenting your React Native application with a Dynamics 365 Fraud Protection software development kit (SDK) for React Native, you agree to the [terms of use for Microsoft application programming interfaces (APIs)](/legal/microsoft-apis/terms-of-use). You also direct Microsoft to process the following types of data from the devices that interact with the Fraud Protection services:

- Device attributes, such as the device ID, screen information, the processor, and the class.
- Operating system (OS) attributes, such as OS information, the OS version, and original equipment manufacturer (OEM) details.
- Applicable browser-related attributes, such as the browser language and installed default apps.

> [!NOTE]
> The types of data listed above are collectively referred to as *device fingerprinting data*.

You have the following responsibilities:

- To obtain consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- To inform your customers about your data collection and processing practices (for example, disclosing what data you collect and how the data are used).
- To disclose your use of third parties that work on your behalf to process the data that you collect. These third parties include Fraud Protection service providers.
- To comply with all laws and regulations that are applicable to the use of Fraud Protection. These laws and regulations include data protection laws.

## React Native library technical reference

1. Install the library.

    - From [npm](https://www.npmjs.com/package/@microsoft/fraud-protection):
    
    ```bash
    npm install @microsoft/fraud-protection --save
    ```

    - From yarn:
    
    ```bash
    yarn add @microsoft/fraud-protection
    ```

1. Link native code.

    - With autolinking (react-native 0.60+):
    
    ```bash
    cd ios && pod install
    ```

    - Pre 0.60:
    
    ```bash
    react-native link @microsoft/fraud-protection
    ```

1. Initiate the SDK so that it can start to collect device attributes.

    ```javascript
    import RNFraudProtection from '@microsoft/fraud-protection';

    RNFraudProtection.start($tenantId);
    ```

    In this code, **tenantId** is the globally unique identifier (GUID) or universally unique identifier (UUID) that is provided by Microsoft.

1. Send collected device attributes to Microsoft by calling **send()**. You can call **send()** anywhere before or on the page that has the operation that you need a risk assessment for. For a sign-in/sign-up scenario, you can call **send()** immediately after the **start()** call.

    ```javascript
    import RNFraudProtection from '@microsoft/fraud-protection';

    RNFraudProtection.send($pageId); // Or RNFraudProtection.send()
    ```

    In this code, **pageId** is optional and can be set in the following way, depending on the scenario:

    - **SI** – Sign In
    - **SU** – Sign Up
    - **P** – Purchase
    - **tst** – Test

1. Call **getSessionId()** to obtain the **SessionId** value that is required when the risk assessment APIs are called.

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

To log a support ticket, go to <https://dfp.microsoft.com>. Global administrator permissions are required.
