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

The setup of device fingerprinting is done in two phases.

1. Configure the Domain Name Server (DNS) Secure Sockets Layer (SSL) certificate, and upload it to the Fraud Protection portal.
1. Implement device fingerprinting.

This section provides detailed instructions for both these phases. The first phase has to be completed only once. However, the second phase must be repeated once for each website or mobile app where device fingerprinting is implemented.

## Set up DNS and generate an SSL certificate

Complete the following procedures to set up DNS and generate an SSL certificate. The DNS and SSL setup, while optional, is strongly recommended to ensure optimal fingerprinting coverage and performance. DNS and SSL setup allows for the fingerprinting script to be considered a first party integration, not a third party cookie.

### Set up DNS

To set up DNS, follow these steps.

1. Select a subdomain under your root domain, such as `fpt.contoso.com`. Any prefix can be used.
1. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

### Generate and upload an SSL certificate

To generate and upload an SSL certificate, follow these steps.

1. For back-end onboarding, generate the SSL certificate for the selected subdomain. You can create one SSL certificate and add all the subdomains in the **Certificate's Subject Alternative Name** field.
2. Go to the [Fraud Protection portal](https://dfp.microsoft.com), and then, in the left navigation pane, select **Integration**.
3. On the **Integration** page, select **Edit**, and then, on the next page, select **Next** to open the **Upload SSL certificate** page.
4. Select **Select Certificate**, and then upload the SSL certificate that you generated. If your certificate has a password, enter it in the text box. Then select **Upload**.

> [!NOTE]
> Only .pfx files are supported. Propagation of the certificate to the device fingerprinting servers might take a few minutes. 

## Implement device fingerprinting

Your website or application must initiate device fingerprinting requests a few seconds before a transaction is sent to Fraud Protection for risk evaluation (such as a transaction for adding a payment instrument, sign-in, or checkout). This requirement ensures that Fraud Protection receives all the data that it requires to make an accurate assessment. This section provides detailed instructions for implementing device fingerprinting on websites and mobile apps. 

To implement device fingerprinting, follow these steps.

1. Modify the following JavaScript script code, and insert it on the webpage or in the application where you want to collect device fingerprinting information.

    ```JavaScript
    <script src="https://<Your_Sub_Domain>/mdt.js?session_id=<session_id>&instanceId=<instance_id>" type="text/javascript"></script>
    ```

    - **Your\_Sub\_Domain** – The subdomain under your root domain.
    - **session\_id** – The unique session identifier of the device that was created by the client. It can be up to 128 characters long and can contain only the following characters: uppercase and lowercase Roman letters, digits, underscore characters, and hyphens (a–z, A–Z, 0–9, \_, -). The session ID should contain at least 16 bytes of randomly generated data. When using hexadecimal encoding, this translates to 32 hexadecimal characters. Although Microsoft recommends that you use a globally unique identifier (GUID) for the session ID, it isn't required.
    - **instance\_id** – This is a required value to integrate your website with device fingerprinting. Use the **Device fingerprinting ID** value that's listed on the **Current environment** tile on the **Integration** page of the corresponding environment in the Fraud Protection portal.

    **Example**

    ```JavaScript
    <script src="https://fpt.contoso.com/mdt.js?session_id=211d403b-2e65-480c-a231-fd1626c2560e&instanceId=b472dbc3-0928-4577-a589-b80090117691" type="text/javascript"></script>
    ```

    Here's an example of a response for mdt.js.

    ```JavaScript
    window.dfp={url:"https://fpt.contoso.com/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",sessionId:"211d403b-2e65-480c-a231-fd1626c2560e",customerId:"b472dbc3-0928-4577-a589-b80090117691",dc:"uswest"};window.dfp.doFpt=function(doc){var frm,src;true&&(frm=doc.createElement("IFRAME"),frm.id="fpt_frame",frm.style.width="1px",frm.style.height="1px",frm.style.position="absolute",frm.style.visibility="hidden",frm.style.left="10px",frm.style.bottom="0px",frm.setAttribute("style","color:#000000;float:left;visibility:hidden;position:absolute;top:-100;left:-200;border:0px"),src="https://Your_Sub_Domain/?session_id=211d403b-2e65-480c-a231-fd1626c2560e&CustomerId=b472dbc3-0928-4577-a589-b80090117691",frm.setAttribute("src",src),doc.body.appendChild(frm))};
    ```

2. Load device fingerprinting after the page's elements are loaded.

    ```JavaScript
    window.dfp.doFpt(this.document);
    ```

3. When you submit transactions in the Fraud Protection API, set a session ID in the **deviceContextId** field. For Assessments, set a session ID in the **deviceFingerprinting.id** field.
4. Set the **device.ipAddress** field to the customer IP address that your website receives when a customer uses your site. For Assessments, set the customer IP address in the **deviceFingerprinting.ipAddress** field. This field is optional and doesn't need to be set if you don't have it.

## Enable client-side integration for device fingerprinting

For certain web fingerprinting scenarios, Fraud Protection supports a specialized class of integration called *client-side integration*. Client-side integration differs from standard integration practices because the fingerprinting response is returned directly to the client as an encrypted payload, skipping the server-to-server assessment call.


Client-side integration is useful for low latency scenarios where skipping the server-to-server call is advantageous. To determine whether or not client-side integration is the right fit for your scenario, look through the following question guide.

1. **Is my scenario device fingerprinting only?**

   If your scenario is not device fingerprinting only, then client-side integration is not a fit for your scenario.

2. **Do I want my fingerprinting data to be in the browser as opposed to my server fetching it?**

   In traditional server-to-server integration, once attribute collection is complete on the website, the data is pushed to Fraud Protection's servers, where you can obtain the assessment response on your server by making the standard assessment API call. In client-side integration however, when the attribute collection data is pushed to Fraud Protection's servers, the assessment response comes back and is returned directly in the browser. This way, your server can extract the assessment response from the browser itself instead of making the server-to-server call, thereby saving some time. Keep in mind that the fingerprinting itself takes a couple of seconds, so the assessment response will only be present in the browser if the user is on the page for a few seconds. If your scenario benefits from the data already being present in the browser, then client-side integration may be right for you.

In general, the majority of fingerprinting scenarios are solved by the standard server-to-server integration, and client-side integration is beneficial for a few specific scenarios where the latency decrease is critical. Since client-side integration is a specialized class of integration that's simplified and secure, the following prerequisites must be met to enable it.

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

Once this script is set up and client-side integration is enabled, the fingerprinting response is returned as an encrypted payload in the client's browser. You can use a callback function to grab the encrypted response payload. The example below shows the callback function in use:

```JavaScript
window.dfp.doFpt(document, function (response) {
    if(response == null || response.startsWith('ServerError'))
        console.log("Error Scenario");
    else
        console.log("Success Scenario"); // pass to server so it can decrypt and use response
});
  ```


You still have to pass the payload to your server to decrypt it and use the response. We don't expect you to call the external call to get the encryption key that you host for decrypting the payload. You should store and access the key in the same secure way you get and manage other secrets used on your server.  




## Additional resources
- [Overview of device fingerprinting](device-fingerprinting.md)
- [Attributes in device fingerprinting](df-attribute.md)
- Set up and implement device fingerprinting
  - [Mobile SDK for iOS](mobile-sdk-ios.md)
  - [Mobile SDK for Android](mobile-sdk-android.md)
  - [Mobile SDK for React Native](mobile-sdk-react-native.md)
- Training: [Implement device fingerprinting in Dynamics 365 Fraud Protection](/training/modules/device-fingerprint-fraud-protection/).
