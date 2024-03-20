---
author: josaw1
description: This article describes how to enable client-side integration for device fingerprinting in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 03/20/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Web setup of device fingerprinting
---

# Web setup of device fingerprinting

For certain web fingerprinting scenarios, Fraud Protection supports a specialized class of integration called *client-side integration*. Client-side integration differs from standard integration practices because the fingerprinting response is returned directly to the client as an encrypted payload, skipping the server-to-server assessment call.

Client-side integration is useful for low latency scenarios where skipping the server-to-server call is advantageous. However, because client-side integration is a specialized class of integration that's simplified and secure, the following prerequisites must be met to enable it.

- You must be in a root environment of a Fraud Protection tenant.
- You must set up an external call that returns an encryption key response in the [JSON Web Key Sets (JWKS) format](https://datatracker.ietf.org/doc/html/rfc7517). This external call returns the key that Fraud Protection uses to encrypt the payload. You can use this key afterward to decrypt the Fraud Protection response server-side that you initially receive client-side. You're responsible for providing the key for encryption and decryption. For information about setting up external calls, see [External calls](external-calls.md).

The following code shows an example of the JWKS format.

```json
{
  "keys":
  [
    {
      "kty":null,
      "use":null,
      "kid":null,
      "k":null
    }
  ]
}
```
- You must only use the metadata and device fingerprinting sections of the device fingerprinting assessment template. If there are additional schema sections, or if you're not using the device fingerprinting assessment template, the client-side integration option isn't available to you.

When you reach the **Settings** page of the assessment wizard for a device fingerprinting template, you'll see the client-side integration option available to you. After choosing to enable the client-side integration, you'll select the external call with the JWKS response format that you set up.

To complete the client-side integration setup, to return the encrypted response in the browser, you must use a modified version of the following JavaScript example.

```JavaScript
<script src="https://<Your_Sub_Domain>/mdt.js?session_id=<session_id>&customerId=<customer_id>&assessment=<assessment>&requestId=<request_id>" type="text/javascript"></script>
```

- **Your\_Sub\_Domain** – The subdomain under your root domain.
- **session\_id** – The unique session identifier of the device that was created by the client. It can be up to 128 characters long and can only contain the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). The session ID must contain at least 16 bytes of randomly generated data. When using hexadecimal encoding, this translates to 32 hexadecimal characters. Although Microsoft recommends that you use a globally unique identifier (GUID) for the session ID, it isn't required.
- **customer\_id** – This is a required value to integrate your website with device fingerprinting. Use the **Environment ID** value that's listed on the **Current environment** tile of the **Integration** page of the corresponding environment in the Fraud Protection portal. You must be in a root environment for client-side integration to work.
- **assessment** – The API name of the device fingerprinting assessment set up with client-side integration enabled. The API name is case-sensitive and pulled from the assessment configuration page.
- **request\_id** – A unique identifier for the request itself, separate from the session ID. This identifier should be a GUID of at least 32 characters in length.

The following sample shows the JavaScript code with example values.

```JavaScript
<script src="https://fpt.contoso.com/mdt.js?session_id=2b2a1f5e-afa7-4c6d-a905-ebf66eaedc83&customerId=b3f6d54b-961c-4193-95ee-b6b204c7fd23&assessment=CSI&requestId=b12e86a0-37b1-43a2-958b-3f04fe7cef6c" type="text/javascript"></script>
  ```

Once this script is set up and client-side integration is enabled, the fingerprinting response is returned as an encrypted payload in the client's browser. You still have to pass the payload to your server to decrypt it and use the response. We don't expect you to call the external call to get the encryption key that you host for decrypting the payload. You should store and access the key in the same secure way you get and manage other secrets used on your server.  




## Additional resources
- [Overview of device fingerprinting](device-fingerprinting.md)
- [Attributes in device fingerprinting](df-attribute.md)
- [Set up and implement device fingerprinting](df-setup-overview.md)
  - [Mobile SDK for iOS](mobile-sdk-ios.md)
  - [Mobile SDK for Android](mobile-sdk-android.md)
  - [Mobile SDK for React Native](mobile-sdk-react-native.md)
- Training: [Implement device fingerprinting in Dynamics 365 Fraud Protection](/training/modules/device-fingerprint-fraud-protection/).
