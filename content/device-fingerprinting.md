---
author: josaw1
description: This article describes device fingerprinting in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/20/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Overview of device fingerprinting
---

# Overview of device fingerprinting

This article describes how to set up device fingerprinting in Microsoft Dynamics 365 Fraud Protection.

A *device fingerprint*, also known as a *machine fingerprint*, contains information that's collected about a remote computing device, such as a computer, Xbox, tablet, or smartphone, for the purpose of identifying that device. Device fingerprinting lets you collect crucial device telemetry during online actions. This information includes hardware information, browser information, geographic information, and the Internet Protocol (IP) address.

Fraud Protection provides a device fingerprinting feature that's based on artificial intelligence (AI), so that device identification can be used as input to the process of fraud assessment. This feature helps the Fraud Protection service track and link seemingly unrelated events in the fraud network to help identify patterns of fraud. The data collected isn't just a static list of attributes but also includes data that's dynamically captured based on the evaluation of specific combinations of attributes, such as browser, system, network, and geo-location attributes. When device characteristics and attributes are collected, the device fingerprinting service uses machine learning to probabilistically identify the device. When using the device ID in rules and velocities, remember that this device ID is probabilistic and not deterministic. While the device ID has a high accuracy, it can still produce false positives.

Device fingerprinting runs on Azure, and includes benefits from proven cloud scalability, reliability, and enterprise-grade security. To help you better understand the impact that device fingerprinting has on fraud detection, this document includes some results from a study that Microsoft did. The study compared six months' worth of data for various Microsoft businesses through two different models: one that used device fingerprinting and one that didn't.

In summary, the results showed that device fingerprinting has a significant positive impact on the model detection rate for all businesses. Because it reduces false negatives, less fraud is detected on approved transactions after the fact.

## Goals 

The purpose of this setup guide is to help you understand how you can:

- Call the Fraud Protection device fingerprinting service.
- Collect the required data, and send it to Fraud Protection.
- Include device fingerprinting session ID information in the subsequent risk assessment API call to Fraud Protection (for example, for an online purchase or creation of a new user account).

## Prerequisites

Before you begin the tasks in this document, you must set up Fraud Protection in a Microsoft Entra tenant, as described in [Set up a trial version of Fraud Protection](promocode-set-up-dfp-trial-version.md) and [Set up a purchased version of Fraud Protection](promocode-set-up-DFP-purchased-version.md).

It's your responsibility to:

- Receive consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- Inform your customers of your data processing practices by, for example, disclosing the data that you collect and how it's used. 
- Disclose your use of third parties working on your behalf to process the data you collect, including Fraud Protection service providers. 
- Comply with all laws and regulations applicable to its use of Fraud Protection, including data protection laws. 

### Important notice regarding data collection

When you implement Fraud Protection device fingerprinting by integrating the script on your online services, you direct Microsoft to collect the following types of data from the devices interacting with such services:

- Device attributes such as plugins installed, processor class, and so on.
- Operating system attributes, such as OS Information.
- Browser-related attributes if applicable such as browser language, font, and so on.
- Network attributes, such as IP address, signature hash, and so on.

Cookies are used in Fraud Protection to collect information for a device, not for a particular individual. You can opt out of using cookies, but that degrades the device fingerprinting.

## Additional resources
- [Attribute categories](df-attribute.md)
- [Set up and implement device fingerprinting](df-setup-overview.md)
  - [Web setup of device fingerprinting](df-web.md)
  - [Mobile SDK for iOS](mobile-sdk-ios.md)
  - [Mobile SDK for Android](mobile-sdk-android.md)
  - [Mobile SDK for React Native](mobile-sdk-react-native.md)
- Training: [Implement device fingerprinting in Dynamics 365 Fraud Protection](/training/modules/device-fingerprint-fraud-protection/).

[!INCLUDE[footer-include](includes/footer-banner.md)]
