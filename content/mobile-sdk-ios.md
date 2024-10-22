---
author: josaw1
description: This article provides information that is required for device fingerprinting in a mobile device implementation of Microsoft Dynamics 365 Fraud Protection for iOS.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile SDK for iOS
ms.custom:
---

# Dynamics 365 Fraud Protection mobile SDK for iOS

This feature is designed and recommended for use with the Microsoft Dynamics 365 Fraud Protection service. Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI); runs on Azure; and is cloud-scalable and reliable, and has enterprise-grade security. Fraud Protection's device fingerprinting feature enables the identification of devices (for example, computers, Xbox consoles, tablets, and mobile phones) across multiple sessions or interactions that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, it enables Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by instrumenting your iOS application with a Dynamics 365 Fraud Protection software development kit (SDK) for iOS, you agree to the [terms of use for Microsoft application programming interfaces (APIs)](/legal/microsoft-apis/terms-of-use). You also direct Microsoft to process the following types of data from the devices that interact with the Fraud Protection services. (This data is collectively referred to as *device fingerprinting data*.)

- Device attributes, such as the device ID, screen information, the processor, and the class
- Operating system (OS) attributes, such as OS information, the OS version, and original equipment manufacturer (OEM) details
- Applicable browser-related attributes, such as the browser language and installed default apps

You have the following responsibilities:

- Receive consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- Inform your customers about your data collection and processing practices. For example, disclose what data you collect and how it's used.
- Disclose your use of third parties that work on your behalf to process the data that you collect. These third parties include Fraud Protection service providers.
- Comply with all laws and regulations that are applicable to the use of Fraud Protection. These laws and regulations include data protection laws.

## iOS technical reference
[![Fraud Protection](https://img.shields.io/cocoapods/v/FraudProtection?label=Latest%20Version&style=for-the-badge)](https://github.com/CocoaPods/Specs/blob/master/Specs/6/e/f/FraudProtection/2.2.1/FraudProtection.podspec.json)

**Minimum Deployment Target: 12.4**
1. Install CocoaPods.
2. Create a new file that is named **Podfile** inside your project's root directory, and add the following statements to it. Replace **YOUR\_TARGET\_PROJECT\_NAME** with the name of your Xcode project.

    ```swift
    platform :ios, '12.4'
    target '${YOUR\_TARGET\_PROJECT\_NAME}' do
        use\_frameworks!
        pod ' FraudProtection', '$version'
    end
    ```

3. Install the pod by running the following command: **pod install --repo-update**
4. You can initiate the SDK in the **AppDelegate** class so that it can start to collect device attributes.

    ```swift
    import FraudProtection
    FraudProtection.start(instanceId: $tenantId)
    ```

    In this code, **tenantId** is the globally unique identifier (GUID) or universally unique identifier (UUID) that is provided by Microsoft.

5. Send collected device attributes to Microsoft by calling **send()**. You can call **send()** in any UIViewController before or on the page that has the operation that you need a risk assessment for. For a sign-in/sign-up scenario, you can call **send()** immediately after **start()** in the base **AppDelegate** class.

    ```swift
    import FraudProtection
    FraudProtection.send(pageId: $pageId)
    ```

    In this code, **pageId** is optional and can be set in the following way, depending on the scenario:

    - **SI** – Sign In
    - **SU** – Sign Up
    - **P** – Purchase
    - **tst** – Test

6. Call **getSessionId()** to obtain the **SessionId** value that is required when the risk assessment APIs are called.

    ```swift
    import FraudProtection
    var sessionId = FraudProtection.getSessionId()
    ```

### iOS runtime permissions

- The iOS SDK uses CLLocationManager, and checks for **CLAuthorizationStatus.authorizedAlways** or **CLAuthorizationStatus.authorizedWhenInUse** before it requests location data. The app should obtain **CLLocationManager.requestWhenInUseAuthorization** Or **CLLocationManager.requestAlwaysAuthorization** permission from the user.
- The iOS SDK uses AppTrackingTransparency and checks for **ATTrackingManager.AuthorizationStatus.authorized** before it collects **AdvertisingId**. The app should obtain **ATTrackingManager.requestTrackingAuthorization** permission from the user.

## iOS additional references

[iOS Apple Developer](https://developer.apple.com/ios/)

[iOS Apple Development](https://developer.apple.com/develop/)

[Xcode](https://developer.apple.com/xcode/)

## Support

To log a support ticket, go to <https://dfp.microsoft.com>. (Global admin permissions are required.)
