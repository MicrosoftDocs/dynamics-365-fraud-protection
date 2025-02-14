---
author: josaw1
description: This article provides information that is required for device fingerprinting in a mobile device implementation of Microsoft Dynamics 365 Fraud Protection for Android.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile SDK for Android
ms.custom:
---

# Dynamics 365 Fraud Protection mobile SDK for Android

[!include[deprecation](includes/deprecation.md)]

This feature is designed and recommended for use with the Microsoft Dynamics 365 Fraud Protection service. Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI); runs on Azure; and is cloud-scalable and reliable, and has enterprise-grade security. Fraud Protection's device fingerprinting feature enables the identification of devices (for example, computers, Xbox consoles, tablets, and mobile phones) across multiple sessions or interactions that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, it enables Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by instrumenting your Android application with a Dynamics 365 Fraud Protection software development kit (SDK) for Android, you agree to the [terms of use for Microsoft application programming interfaces (APIs)](/legal/microsoft-apis/terms-of-use). You also direct Microsoft to process the following types of data from the devices that interact with the Fraud Protection services. (This data is collectively referred to as *device fingerprinting data*.)

- Device attributes, such as the device ID, screen information, the processor, and the class
- Operating system (OS) attributes, such as OS information, the OS version, and original equipment manufacturer (OEM) details
- Applicable browser-related attributes, such as the browser language and installed default apps

You have the following responsibilities:

- Receive consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- Inform your customers about your data collection and processing practices. For example, disclose what data you collect and how it's used.
- Disclose your use of third parties that work on your behalf to process the data that you collect. These third parties include Fraud Protection service providers.
- Comply with all laws and regulations that are applicable to the use of Fraud Protection. These laws and regulations include data protection laws.

## Android technical reference
[![Fraud Protection](https://img.shields.io/jitpack/version/com.github.microsoft/fraudprotection-sdk-android?label=Latest%20Version&style=for-the-badge)](https://jitpack.io/#microsoft/FraudProtection-SDK-Android/2.2.0)

**minSdkVersion: 21**

1. Add the JitPack repository to your root build.gradle.

    ```gradle
    allprojects {
        repositories {
            ...
            maven { url 'https://jitpack.io' }
        }
    }
    ```

2. Add the dependency.

    ```gradle
    dependencies {
        implementation ('com.github.microsoft:fraudprotection-sdk-android:$version@aar'){
            transitive = true
        }
    }
    ```

3. Select **Sync Project with Gradle Files**.
4. You can initiate the SDK in the base application class so that it can start to collect device attributes.

    ```java
    import com.microsoft.fraudprotection.androidsdk.FraudProtection;
    FraudProtection.start(getApplicationContext(), tenantId);
    ```

    In this code, **tenantId** is the globally unique identifier (GUID) or universally unique identifier (UUID) that is provided by Microsoft.

5. Send collected device attributes to Microsoft by calling **send()**. You can call **send()** in any fragment/activity before or on the page that has the operation that you need a risk assessment for. For a sign-in/sign-up scenario, you can call **send()** immediately after **start()** in the base application class.

    ```java
    import com.microsoft.fraudprotection.androidsdk.FraudProtection;
    FraudProtection.send(pageId);
    ```

    In this code, **pageId** is optional and can be set in the following ways, depending on the scenario:

    - **SI** – Sign in
    - **SU** – Sign up
    - **P** – Purchase
    - **tst** – Test

6. Call **getSessionId()** to obtain the **sessionId** value that is required when the risk assessment APIs are called.

    ```java
    import com.microsoft.fraudprotection.androidsdk.FraudProtection;
    String sessionId = FraudProtection.getSessionId();
    ```

### Android runtime permissions

The Android SDK relies on the following runtime permissions to collect various device data. The Android SDK doesn't ask for any runtime permissions. The app should obtain these runtime permissions from the user.

- android.permission.ACCESS\_COARSE\_LOCATION
- android.permission.READ\_PHONE\_STATE
- android.permission.BLUETOOTH\_CONNECT

## Android additional references

[Android API Reference](https://developer.android.com/reference)

[About permissions](https://developer.android.com/training/permissions/requesting)

[App manifest file](https://developer.android.com/guide/topics/manifest/manifest-intro)

[Add dependency](https://developer.android.com/studio/projects/android-library#AddDependency)

[Determine sensitive data access needs](https://developer.android.com/games/develop/permissions)

[Android Legal Notice](https://developer.android.com/legal)

## Support

To log a support ticket, go to <https://dfp.microsoft.com>. (Global admin permissions are required.)
