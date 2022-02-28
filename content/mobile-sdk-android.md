---
author: josaw1
description: This topic provides the information that is required for device fingerprinting in a Microsoft Dynamics 365 Fraud Protection mobile device implementation for Android.
ms.author: josaw
ms.date: 03/01/2022
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile SDK for Android
ms.custom:
---

# Dynamics 365 Fraud Protection mobile SDK for Android

## Introduction

This feature is designed and recommended for use with Microsoft Dynamics 365 Fraud Protection service. Microsoft Dynamics 365 Fraud Protection provides device fingerprinting that (i) is based on artificial intelligence (AI); (ii) runs on Microsoft Azure; and (iii) is cloud-scalable, reliable, and has enterprise-grade security. Fraud Protection's device fingerprinting feature enables the identification of devices (computer, Xbox, tablet, mobile phone, and so on) across multiple sessions or interactions that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, this feature allows Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by instrumenting your Android application with a Dynamics 365 Fraud Protection SDK for Android, you (i) agree to Microsoft's APIs terms of use located [here](https://docs.microsoft.com/en-us/legal/microsoft-apis/terms-of-use), and (ii) you direct Microsoft to process the following types of data from the devices interacting with the Fraud Protection services (collectively, "Device Fingerprinting Data"):

1.  Device attributes such as device ID, screen information, processor class, etc.

2.  Operating system (OS) attributes, such as OS information, OS version, OEM details, etc.

3.  Browser related attributes, if applicable, such as browser language, installed default apps, etc.

It is your responsibility to:

1.  Receive consent from your users to collect and allow Microsoft to process the Device Fingerprinting Data.

2.  Inform your customers of your data collection and processing practices, for example, by disclosing the data you collect and how it is used.

3.  Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers.

4.  Comply with all laws and regulations applicable to the use of Fraud Protection, including data protection laws.

## Attribute category introduction reference

Below is a list of the device fingerprinting attribute categories that we try to collect and how it helps in detecting Fraud. If your organization has specific needs and you would like certain categories of data to not be processed by us, you can reach out to customer support before onboarding, and we can help you configure this correctly to meet your privacy needs.

**Core Features:** This group of attributes is core to Fraud Protection's ability to predict patterns of fraud. Based on our prior experience we believe that these attributes will be highly accretive to Fraud Protection's model performance and ability to discern distinctive patterns of fraud. If these are not supplied, then the device fingerprinting will be inaccurate.

**Investigative Features:** This group of attributes has the potential to add or enhance Fraud Protection's ability to predict patterns of fraud more accurately. Statistical analysis of collected data is the only definitive way of determining whether these attributes are strong predictors of patterns of fraud. If the predictive capability of these attributes does not live up to our expectations, then we will no longer utilize these attributes. While these group of attributes would allow us to determine whether they will be strong predictors of patterns of fraud, they are optional and are not required to be provided.

**Potential Label:** This group of attributes is utilized for model supervision and labeling purposes. Each of these attributes by itself has a probability of not providing ground truth. However, combining these attributes increases the likelihood that the label used in training the Fraud Protection's model becomes ground truth and results in higher model performance.

## Android technical reference

1.  Add the JitPack repository to your root build.gradle.

allprojects {

  repositories {

    ...

    maven { url 'https://jitpack.io' }

  }

 }

2.  Add the dependency.

dependencies {

  implementation ('com.github.microsoft:fraudprotection-sdk-android:2.0.0@aar'){

    transitive = true

  }

}

3.  Select **Sync Project with Gradle Files**.

4.  You can initiate the SDK in the base Application class so it can start collecting device attributes.

```plaintext
import com.microsoft.fraudprotection.androidsdk.FraudProtection;

FraudProtection.start(getApplicationContext(), tenantId);

- **TenantId—**Provided by Microsoft (GUID/UUID).
```

5.  Send collected device attributes to Microsoft by calling send(). You can call send() in any fragment/activity before or on the page that has the operation you need a risk assessment for. For a Sign In/Up scenario, you can call send() immediately after start() in base Application class.

```plaintext
import com.microsoft.fraudprotection.androidsdk.FraudProtection;

FraudProtection.send(pageId);
```

The pageId is optional and can be set as follows based on the scenario.

- **SI—**Sign in

- **SU—** Sign up

- **P—** Purchase

- **tst—** Test

6.  Obtain the SessionId required when calling the risk assessment APIs by calling getSessionId().

```plaintext
import com.microsoft.fraudprotection.androidsdk.FraudProtection;

String sessionId = FraudProtection.getSessionId();
```

### Android runtime permissions

The Android SDK relies on the following runtime permissions to collect various device data. The Android SDK does not ask for any runtime permissions. The app should obtain these runtime permissions from the user.

-   android.permission.ACCESS\_COARSE\_LOCATION

-   android.permission.READ\_PHONE\_STATE

-   android.permission.BLUETOOTH\_CONNECT


## Android additional references

[Android API Reference](https://developer.android.com/reference)

[About permissions](https://developer.android.com/training/permissions/requesting)

[App manifest file](https://developer.android.com/guide/topics/manifest/manifest-intro)

[Add dependency](https://developer.android.com/studio/projects/android-library#AddDependency)

[Determine sensitive data access needs](https://developer.android.com/games/develop/permissions)

[Android Legal Notice](https://developer.android.com/legal)

## Support 

To log a support ticket, go to: https://dfp.microsoft.com (requires global admin permissions).
