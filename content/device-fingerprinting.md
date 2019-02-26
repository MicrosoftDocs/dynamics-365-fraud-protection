---
author: jackwi111
description: Adopt and integrate device fingerprinting
ms.author: v-jowigh
ms.date: 02/25/2019
ms.service:
 - d365-fraud-protection
ms.topic: conceptual
title: Adopt and integrate device fingerprinting
---


# Adopt and integrate device fingerprinting

## Device fingerprinting

Based on cutting-edge machine learning and artificial intelligence, Dynamics 365 Fraud Protection offers device fingerprinting. This
enables the service to identify the devices (not individuals) across multiple sessions or interactions that engage with your business,
all while respecting customer privacy. By tracking elements related to a device (computer, Xbox, tablets, and so on), you can link
individual devices to events. Using device fingerprinting, you can link seemingly unassociated events to each other by capturing and
identifying unique device characteristics during the Add PI, sign in, or checkout processes. 

Device fingerprinting runs on Azure. It is cloud-scalable, reliable, and provides enterprise-grade security. A major advantage over
similar products in the marketplace is that device fingerprinting is being continually tested against the latest fingerprinting-evasion
fraudster tools.

## Adopt and integrate device fingerprinting

Traditional fraud mitigation strategies have always focused on data elements relating to the user such as Credit Card (CC) information,
billing address, shipping address, e-mail, phone number, name, and so on. These elements are valuable; however, they can be compromised
via phishing and identity theft, and are increasingly difficult to detect in a world of the internet of things (IoT). 

By tracking elements related to a device (computer, Xbox, Tablets, and so on), we may more readily link individual fraudsters to events.
In most cases, malicious fraudsters are unlikely to use a unique device for each unique payment instrument (PI) involved in an attempted
fraud. 

Device fingerprinting technology detects variables not previously recorded within the risk engine. With this optimization, the engine
can better identify fraudulent behavior, and link seemingly unassociated events to each other by capturing and identifying unique device
characteristics during the Add PI, sign in, or checkout process. 

Uniqueness determination includes:

- Device fingerprinting fuzzy device ID
- HTTP fingerprinting
- TCPIP fingerprinting
- SSL fingerprinting

Suspicious activity determination includes:

- Mismatches between local transaction time and browser time.
- Derogatory IP address information. 

This topic describes:

- Adopting and integrating device fingerprinting with your web portal, as well as back-end labels processing fraud detection systems.
- Placing the code snippets in your web portal either on Add PI, sign in, checkout, or pages to initiate device profiling.
- Using the API for deeper integration with your backend systems.

## To adopt device fingerprinting 

[!NOTE]   Device fingerprinting does not require any software installation. 


