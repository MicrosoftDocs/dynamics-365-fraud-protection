---
author: josaw1
description: This article describes how to set up device fingerprinting in Microsoft Dynamics 365 Fraud Protection.
ms.author: josaw
ms.date: 02/27/2024
ms.topic: conceptual
search.audienceType:
  - admin
title: Set up device fingerprinting
---

# Set up device fingerprinting

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

## Set up device fingerprinting

The setup of device fingerprinting is done in two phases.

1. Configure the Domain Name Server (DNS) Secure Sockets Layer (SSL) certificate, and upload it to the Fraud Protection portal.
1. Implement device fingerprinting (on a website or a mobile app).

This section provides detailed instructions for both these phases. The first phase has to be completed only once. However, the second phase must be repeated once for each website or mobile app where device fingerprinting is implemented.

### Set up DNS and generate an SSL certificate

Complete the following procedures to set up DNS and generate an SSL certificate.

#### Set up DNS

To set up DNS, follow these steps.

1. Select a subdomain under your root domain, such as `fpt.contoso.com`. Any prefix can be used.
1. For the selected subdomain, create a canonical name (CNAME) that points to `fpt.dfp.microsoft.com`.

#### Generate and upload an SSL certificate

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

Client-side integration is useful for low latency scenarios where skipping the server-to-server call is advantageous. However, because client-side integration is a specialized class of integration that's simplified and secure, the following prerequisites must be met to enable it.

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
- **customer\_id** – This is a required value to integrate your website with device fingerprinting. Use the **Environment ID** value that's listed on the **Current environment** tile of the **Integration** page of the corresponding environment in the Fraud Protection portal.
- **assessment** – The API name of the device fingerprinting assessment set up with client-side integration enabled. The API name is case sensitive and pulled from the assessment configuration page.
- **request\_id** – A unique identifier for the request itself, separate from the session ID. This identifier should be a GUID of at least 32 characters in length.

The following sample shows the JavaScript code with example values.

```JavaScript
<script src="https://fpt.contoso.com/mdt.js?session_id=2b2a1f5e-afa7-4c6d-a905-ebf66eaedc83&customerId=b3f6d54b-961c-4193-95ee-b6b204c7fd23&assessment=CSI&requestId=b12e86a0-37b1-43a2-958b-3f04fe7cef6c" type="text/javascript"></script>
  ```

Once this script is set up and client-side integration is enabled, the fingerprinting response is returned as an encrypted payload in the client's browser. You still have to pass the payload to your server to decrypt it and use the response. We don't expect you to call the external call to get the encryption key that you host for decrypting the payload. You should store and access the key in the same secure way you get and manage other secrets used on your server.  

Once you set up a device fingerprinting assessment with client-side integration, you're also able to call standard Fraud Protection server-to-server APIs to retrieve the fingerprinting intelligence.

## Enable fingerprinting on a mobile app

For mobile apps, device fingerprinting integration supports Android, iOS, and React Native platforms via software development kit (SDK) integration. For more information about the mobile reference implementation, see the following articles:

- [Dynamics 365 Fraud Protection mobile SDK for Android](mobile-sdk-android.md)
- [Dynamics 365 Fraud Protection mobile SDK for iOS](mobile-sdk-ios.md)
- [Dynamics 365 Fraud Protection mobile SDK for React Native](mobile-sdk-react-native.md)

## Attribute category introduction reference

The following tables show the device fingerprinting attribute categories that we try to collect for web, iOS, and Android. The description of the attributes explains how each helps detect fraud. If your organization has specific needs, and you want some categories of data not to be processed by Fraud Protection, reach out to customer support before onboarding. Customer support can help you do the configuration correctly to meet your privacy needs.

## Device fingerprinting attribute list for web

| Category | Name | Description of the attribute |
|----------|------|------------------------------|
|BrowserUserAgent|User Agent Browser |Browser name parsed from user agent.|
|BrowserUserAgent|User Agent Device Family|Device family parsed from user agent.|
|BrowserUserAgent|User Agent Mobile|Boolean value indicating whether the device is mobile or not parsed from user agent.|
|BrowserUserAgent|User Agent OS|Operating system parsed from user agent.|
|BrowserUserAgent|User Agent Platform|Browser name and version parsed from user agent.|
|BrowserUserAgent|User Agent String|User agent string from HTTP header.|
|BrowserUserAgent|User Agent Type|User agent type (computer, mobile, or spider).|
|Canvas/WebGL|Image Data URL Hash|Hash of image data drawn on canvas.|
|Canvas/WebGL|Renderer|WebGL renderer.|
|Canvas/WebGL|Unmasked Renderer|WebGL unmasked renderer.|
|Canvas/WebGL|Unmasked Vendor|WebGL unmasked vendor.|
|Canvas/WebGL|Vendor|WebGL vendor.|
|Derived Attributes|Device ID|Device ID generated by ML-based device match.|
|HTTP and Browser Info|Browser Languages|Languages accepted by browser.|
|HTTP and Browser Info|Cookie ID|Device ID cookie value.|
|HTTP and Browser Info|HTTP Headers|HTTP header name and value list.|
|HTTP and Browser Info|Is Cookie Enabled|Boolean value indicating whether a cookie is enabled.|
|HTTP and Browser Info|Is Proxy|Boolean value indicating whether a proxy or VPN is detected.|
|HTTP and Browser Info|Profiled Domain|HTTP request host name.|
|HTTP and Browser Info|Proxy IP|IP address of the proxy server.|
|HTTP and Browser Info|True IP|Client IP address.|
|HTTP and Browser Info|URL Referrer|Referrer URL.|
|IP Geo and Intelligence|Autonomous System Number|Autonomous system number.|
|IP Geo and Intelligence|City|City.|
|IP Geo and Intelligence|Connection Type|Internet connection type.|
|IP Geo and Intelligence|Continent|Continent.|
|IP Geo and Intelligence|Country Code|Country ISO code.|
|IP Geo and Intelligence|Defined Market Area|Defined market area.|
|IP Geo and Intelligence|Latitude|Latitude.|
|IP Geo and Intelligence|Line Speed|Speed of internet connection.|
|IP Geo and Intelligence|Longitude|Longitude.|
|IP Geo and Intelligence|Organization|Organization for the IP address.|
|IP Geo and Intelligence|Organization Type|Organization type.|
|IP Geo and Intelligence|Postal Code|Postal code.|
|IP Geo and Intelligence|Proxy Level|Degree of concealment provided by the proxy.|
|IP Geo and Intelligence|Proxy Type|Network or protocol used by the proxy server.|
|IP Geo and Intelligence|Region|Regional information.|
|IP Geo and Intelligence|State|State.|
|IP Geo and Intelligence|Time Zone|Time zone for IP geo location.|
|JavaScript Collected Info|Browser Automation|Browser automation detected.|
|JavaScript Collected Info|Daylight Saving Offset|Time zone daylight saving offset.|
|JavaScript Collected Info|Eval Function Length|Eval function string length.|
|JavaScript Collected Info|Fonts Hash and Count|System fonts hash and count.|
|JavaScript Collected Info|Headless App Version|Headless detection in navigator.appVersion.|
|JavaScript Collected Info|Is Chromium|Boolean value indicating whether window.chrome is defined.|
|JavaScript Collected Info|Is Flash Detected|Boolean value indicating whether Flash is detected.|
|JavaScript Collected Info|Is JavaScript Enabled|Boolean value indicating whether JavaScript is enabled. |
|JavaScript Collected Info|Is Opera|Boolean value indicating whether window.opera is defined.|
|JavaScript Collected Info|Logical Process Count|Logical processor count.|
|JavaScript Collected Info|Mime Type Hash and Count|Browser mime type hash and count.|
|JavaScript Collected Info|On Page Time|Time spent on the web page.|
|JavaScript Collected Info|Online Status|Online status of the browser.|
|JavaScript Collected Info|OS CPU|Current operating system (Firefox only).|
|JavaScript Collected Info|Plug-In Hash and Count|Browser plug-in hash and count.|
|JavaScript Collected Info|Processor Class|CPU class.|
|JavaScript Collected Info|Product Sub|Build number of the current browser.|
|JavaScript Collected Info|Realtime Time Zone Offset|Current time zone offset.|
|JavaScript Collected Info|Round Trip Time|Round trip time from the browser.|
|JavaScript Collected Info|Screen Color Depth|Screen color depth.|
|JavaScript Collected Info|Screen Resolution|Screen resolution.|
|JavaScript Collected Info|Script IP|IP address from JavaScript callback.|
|JavaScript Collected Info|Script OS|Operating system detected by JavaScript.|
|JavaScript Collected Info|Script User Agent|User agent string detected by JavaScript.|
|JavaScript Collected Info|Script User Agent Languages|Browser languages detected by JavaScript.|
|JavaScript Collected Info|Time Zone Offset|Time zone offset.|
|Model Output|Bot Score|Score from Bot model.|
|Network Stack|TCP Distance|TCP distance computed from TTL.|
|SSL/TLS Signature|Cipher Suites|List of supported encryption algorithms for SSL/TLS.|
|SSL/TLS Signature|Compression Suites|List of supported compression methods for SSL/TLS.|
|SSL/TLS Signature|Extensions|List of SSL extensions.|
|SSL/TLS Signature|SSL/TLS Version|SSL/TLS version.|
|TCP Signature|IP Version|IP protocol version (IPv4 and IPv6).|
|TCP Signature|Maximum Segment Size|Maximum segment size.|
|TCP Signature|Options Size|IPv4 options length.|
|TCP Signature|TCP Options|Ordered layout of TCP options.|
|TCP Signature|TCP Quirks|Quirks observed in IP or TCP headers.|
|TCP Signature|TTL|Time-To-Live from IP packet.|
|TCP Signature|Window Scaling Factor|TCP window scale factor.|
|TCP Signature|Window Size|TCP window size.|
|User Agent Client Hints|Architecture|Platform architecture.|
|User Agent Client Hints|Bitness|Architecture bitness ("32" or "64").|
|User Agent Client Hints|Mobile|Boolean value indicating whether the device is mobile from client hint.|
|User Agent Client Hints|Model|Model of mobile device.|
|User Agent Client Hints|Platform|Operating system from client hint.|
|User Agent Client Hints|Platform Version|Operating system version from client hint.|
|User Agent Client Hints|User Agent|Browser name and major version from client hint.|
|User Agent Client Hints|User Agent Full Version List|Full browser version list from client hint.|

## Device fingerprinting attribute list for iOS

| Category | Name | Description of the attribute |
|----------|------|------------------------------|
|Accelerometer|Accelerometer Data Time Stamp|Time at which the accelerometer data is valid.|
|Accelerometer|Accelerometer Data|Accelerometer reading [X-axis, Y-axis, Z-axis].|
|Derived Attributes|Device ID|Device ID derived from device attributes.|
|Device Specification|Active Processor Count|Number of active processing cores available on the device.|
|Device Specification|Advertising ID|Alphanumeric string unique to each device, used only for serving advertisements. In iOS 10.0 and later, the value of the Advertising ID is all zeroes when the user has limited ad tracking. Unlike the identifierForVendor property of the UIDevice, the same value is returned to all vendors. This identifier may change if, for example, the user erases the device. For this reason, you shouldn't cache it.|
|Device Specification|Allows VOIP|Indicates if carrier allows VOIP calls to be made on its network.|
|Device Specification|App Version Code|App build code. For example, 230, A1160.|
|Device Specification|App Version Name|App version. For example, 4.3.1.|
|Device Specification|Available Internal Storage|Available internal storage in bytes for device.|
|Device Specification|Battery Level|Battery charge level for the device.|
|Device Specification|Bundle Identifier|Unique identifier for an application in Apple's ecosystem.|
|Device Specification|Bundle Name|Short name of the bundle.|
|Device Specification|CPU Usage|CPU usage by device. For example, 0.39. [System, User, Idle, Nice]|
|Device Specification|Data Network Type|Network reachable over Wi-Fi or mobile.|
|Device Specification|Device Model Name|Actual device model name used by Apple. For example, iPhone 7, iPhone 8 plus, iPhone XS Max.|
|Device Specification|Device System Name|Name of the operating system running on the device represented by the receiver. For example, iOS.|
|Device Specification|Device System Version|Current version of the operating system. For example, 12.0.1.|
|Device Specification|Identifier For Vendor|UUID that may be used to uniquely identify the device. This is the same across apps from a single vendor. The value of this property is the same for apps that come from the same vendor running on the same device. A different value is returned for apps on the same device that come from different vendors, and for apps on different devices regardless of vendor. Normally, the vendor is determined by data provided by the App Store. If the app wasn't installed from the app store (such as enterprise apps and apps still in development), then a vendor identifier is calculated based on the app’s bundle ID. The bundle ID is assumed to be in reverse-DNS format.|
|Device Specification|IP Address V4 (IPV4)|IP address V4.|
|Device Specification|IP Address V6 (IPV6)|IP address V6.|
|Device Specification|Is Battery Charging|Boolean value indicating whether the device battery is in a charging state.|
|Device Specification|Is Captured|Boolean value indicating whether the contents of the screen are being cloned to another destination. (iOS >= 11)|
|Device Specification|Is Connected|Boolean value indicating whether the network is currently reachable.|
|Device Specification|Is Device Emulator|Boolean value indicating whether the device is being run on a simulator. The iOS simulator allows the user to use features and run applications on the virtual iPhone on their MacBook as though it was the actual iPhone device. Also known as IsDeviceSimulator.|
|Device Specification|Is Device Rooted|Boolean value indicating whether the device is jailbroken. Jailbreaking/rooting changes the operating system running on an iPhone or iPod touch to give you more control. Also known as IsDeviceJailBroken.|
|Device Specification|Is Low Power Mode Enabled|Boolean value indicating whether low power mode is enabled on an iOS device.|
|Device Specification|Is Multitasking Supported|Boolean value indicating whether multitasking is supported on the current device. |
|Device Specification|Kernel OS Release Name|Kernel operating system release. For example, 18.0.3.|
|Device Specification|Kernel System Name|Kernel operating system name. For example, Darwin, Linux.|
|Device Specification|Memory Usage|RAM memory usage by device in bytes. [Free, Active, Inactive, Wired] |
|Device Specification|Mobile Country Code|Mobile country code for the subscriber's cellular service provider.|
|Device Specification|Mobile Network Code|Mobile network code for the subscriber's service provider.|
|Device Specification|Native Scale|Native scale factor for the physical screen.|
|Device Specification|Network Country ISO|Country code for the subscriber's cellular service provider, represented as an ISO 3166-1 country code string. Also known as ISOCountryCode.|
|Device Specification|Network Operator|The name of the subscriber's cellular service provider. For example, AT&T. Also known as CarrierName.|
|Device Specification|Process Globally Unique String|Global unique identifier for the process.|
|Device Specification|Process Identifier|Identifier of the process, often called process ID.|
|Device Specification|Process Name|Name of the process.|
|Device Specification|Processor Count|Number of processing cores available on the device.|
|Device Specification|Process OS Version String|String containing the version of the operating system on which the process is executing.|
|Device Specification|Refresh Rate|The maximum number of frames per second of which the screen is capable. Also known as MaxFramesPerSecond (iOS >= 10.3).|
|Device Specification|Scale|Natural scale factor associated with the screen.|
|Device Specification|Screen Size in Pixels |Absolute width and height of the available display size in pixels.|
|Device Specification|Screen Size in Points |Absolute width and height of the available display size in points.|
|Device Specification|Screen Wants Software Dimming|Whether the screen may be dimmed lower than the hardware is normally capable of by emulating it in software.|
|Device Specification|SDK Device ID|SDK device ID generated on first use.|
|Device Specification|SIM Network Type|The current radio access technology for each service of the device is registered with. May be nil if the device isn't registered on any network. Also known as RadioAccessTechnology.|
|Device Specification|Supports Focus |Whether the screen supports focus-based inputs.|
|Device Specification|System Uptime|Amount of time the system has been awake since the last time it was restarted.|
|Device Specification|Thermal State|Current thermal state to determine if your app should reduce system usage.|
|Device Specification|Total Internal Storage|Total internal storage in bytes for device.|
|Device Specification|Total Memory|Total RAM memory on device in bytes.|
|Device Specification|User Interface Idiom|Style of interface to use on the current device. For example, iPhone, iPad).|
|Gyroscope|Gyroscope Data |Gyroscope reading [X-axis, Y-axis, Z-axis].|
|Gyroscope|Gyroscope Data Time Stamp|Time at which the gyroscope data is valid. |
|Location|Altitude|Altitude of the location in meters. Can be positive (above sea level) or negative (below sea level).|
|Location|Horizontal Accuracy|Horizontal accuracy of the location in meters.|
|Location|Location Data|Current location data (latitude, longitude).|
|Location|Vertical Accuracy|Vertical accuracy of the location in meters.|
|Model Output|Bot Score|Score from Bot model.|
|User Preference|Auto Updating Current Locale|Locale which tracks the user's current preferences.|
|User Preference|Auto Updating Current Time Zone|Time zone currently used by the system, automatically updating to the user's current preference.|
|User Preference|Brightness|Screen brightness.|
|User Preference|Can Send Mail|Identifies if the user has set up the device for sending email.|
|User Preference|Current Locale|User's current locale.|
|User Preference|Current Pixel Aspect Ratio|Aspect ratio of a single pixel. Ratio is defined as X/Y.|
|User Preference|Current Screen Size in Pixels|Current maximum screen width in pixels.|
|User Preference|Current Time Zone|Time zone currently used by the system.|
|User Preference|Device Orientation|Physical orientation of the device.|
|User Preference|Is Assistive Touch Running|Boolean value indicating whether the system preference for assistive touch is enabled. This always returns **false** if Guided Access isn't enabled.|
|User Preference|Is Bold Text Enabled|Boolean value indicating whether the system preference for bold text is enabled.|
|User Preference|Is Closed Captioning Enabled|Boolean value indicating whether the system preference for closed captioning is enabled.|
|User Preference|Is Darker System Colors Enabled|Boolean value indicating whether the system preference for darker colors is enabled.|
|User Preference|Is Generating Device Orientation Notifications|Boolean value indicating whether the receiver generates orientation notifications.|
|User Preference|Is Grayscale Enabled|Boolean value indicating whether the system preference for grayscale is enabled.|
|User Preference|Is Guided Access Enabled|Boolean value indicating whether the app is running under guided access mode.|
|User Preference|Is Invert Colors Enabled|Boolean value indicating whether the system preference for invert colors is enabled.|
|User Preference|Is Mono Audio Enabled|Boolean value indicating whether system audio is mixed down from stereo to mono.|
|User Preference|Is On/Off Switch Labels Enabled|Boolean value indicating whether the system preference for on/off labels for toggles is enabled. |
|User Preference|Is Reduce Motion Enabled|Boolean value indicating whether the system preference for reduce motion is enabled.|
|User Preference|Is Reduce Transparency Enabled|Boolean value indicating whether the system preference for reduce transparency is enabled.|
|User Preference|Is Shake to Undo Enabled|Boolean value indicating whether the system preference for shake to undo is enabled.|
|User Preference|Is Speak Screen Enabled|Boolean value indicating whether the system preference for speak screen is enabled.|
|User Preference|Is Speak Selection Enabled|Boolean value indicating whether the system preference for speak selection is enabled.|
|User Preference|Is Switch Control Running|Boolean value indicating whether switch control is running.|
|User Preference|Is Valid Interface Orientation|Boolean value indicating whether the specified orientation is one of the portrait or landscape orientations.|
|User Preference|Is Video Autoplay Enabled|Boolean value indicating whether the system preference for autoplay videos is enabled.|
|User Preference|Passcode Or Biometry Is Enabled|Passcode or biometry authentication set by user. For example, PassCodeOrBiometrySet, BiometryNotAvailable, PassCodeNotSet.|
|User Preference|Preferred Languages|List of the user's preferred languages.|
|User Preference|Should Differentiate Without Color|Whether the system preference for differentiate without color is enabled.|

## Device fingerprinting attribute list for Android

| Category | Name | Description of the attribute |
|----------|------|------------------------------|
|Accelerometer|Accelerometer Data|Accelerometer sensor reading.|
|Accelerometer|Accelerometer Name|Name of Accelerometer sensor. For example, MPU6515 Accelerometer.|
|Accelerometer|Accelerometer Power|Power in mA used by the accelerometer sensor while in use.|
|Accelerometer|Accelerometer Vendor Name|Vendor of accelerometer sensor. For example, InvenSense.|
|Accelerometer|Accelerometer Version|Version of the accelerometer sensor's module.|
|Derived Attributes |Device ID|Device ID derived from device attributes.|
|Device Specification|Advertising ID|User-resettable identifier and is appropriate for ads use cases. |
|Device Specification|Android ID |64-bit number (expressed as a hexadecimal string), unique to each combination of app-signing key, user, and device. The values of the Android ID (ANDROID_ID) are scoped by signing key and user. The value may change if a factory reset is performed on the device or if an APK signing key changes. On Android 8.0 (API level 26) and higher versions of the platform.|
|Device Specification|App Directory Path|The absolute path to the directory on the file system where files created with openFileOutput are stored.|
|Device Specification|App Package Name|Name of the application package.|
|Device Specification|Application Label|Label associated with the application.|
|Device Specification|App Version Code|Version number of this app.|
|Device Specification|App Version Name|Version name of this app.|
|Device Specification|Available External Storage|External storage available in bytes for the device.|
|Device Specification|Available Internal Storage|Internal storage available in bytes for the device.|
|Device Specification|Available Memory|RAM currently available for the device.|
|Device Specification|Battery Level|Current battery level.|
|Device Specification|Bluetooth Address|Hardware address of the local Bluetooth adapter. For example, 00:11:22:AA:BB:CC.|
|Device Specification|Bluetooth Adapter Name |Friendly Bluetooth name of the local Bluetooth adapter. This name is visible to remote Bluetooth devices.|
|Device Specification|Bluetooth State|Current state of the local Bluetooth adapter.|
|Device Specification|Board|Name of the underlying board. For example, goldfish.|
|Device Specification|Bootloader|System bootloader version number.|
|Device Specification|Brand|Consumer-visible brand with which the product or hardware is associated, if any.|
|Device Specification|Screen Size Category|Screen size category: SMALL, NORMAL, LARGE, XLARGE, UNDEFINED.|
|Device Specification|Cellular Data State|Current cellular data connection state: DISCONNECTED, CONNECTED, SUSPENDED.|
|Device Specification|Charge Type|Whether the device is plugged in to a power source. Zero (0) means it's on battery, other constants are different types of power sources.|
|Device Specification|Code Name|Current development code name, or the string "REL" if this is a release build.|
|Device Specification|Configured Networks SSIDs|List of all the networks configured SSIDs for the current foreground user.|
|Device Specification|CPU Info Hash|CPU info hashed by MD5.|
|Device Specification|CPU Number of Cores|Number of processors available to the Java virtual machine.|
|Device Specification|CPU Usage|Current CPU usage by device. For example, 0.39.|
|Device Specification|Data Network Type|Human-readable name that describes the type of the network. For example, "WI-FI," "MOBILE."|
|Device Specification|Device|Name of the industrial design. Device name provided by manufacturer. For example, Bravo, Passion, GT-I9000.|
|Device Specification|Display|Build ID which is displayed.|
|Device Specification|Display ID|Logical display ID. Each logical display has a unique ID.|
|Device Specification|Google Services Framework ID|Google Services Framework Identifier (GSF ID) is a unique 16 character hexadecimal number that your device automatically requests from Google when log into your Google Account for the first time. For a specific device, the GSF ID only changes after a factory reset.|
|Device Specification|Hardware|Name of the hardware from the kernel command line or /proc.|
|Device Specification|Host|Name of the host building the ROM and kernel.|
|Device Specification|Build ID|Build change list number or build label like "M4-rc20."|
|Device Specification|Is Battery Charging|Boolean value indicating whether the device battery is in a charging state.|
|Device Specification|Is External Memory Mounted|Boolean value indicating whether an external memory (SD) card is mounted. |
|Device Specification|Is Device Connected to the Network|Boolean value indicating whether network connectivity exists, and if it's possible to establish connections and pass data.|
|Device Specification|Is Device Roaming|Boolean value indicating whether the device is currently roaming on the network. When true, it suggests that use of data on this network may incur extra costs.|
|Device Specification|Is Wi-Fi Enabled|Boolean value indicating whether Wi-Fi is enabled.|
|Device Specification|Is Device Emulator|Boolean value indicating whether the device is being run on an emulator. The Android Emulator simulates Android devices on your computer so you can test your application on a variety of devices and Android API levels without needing to have each physical device. |
|Device Specification|Is Device Rooted|Boolean value indicating if the device is rooted. Rooting is a way to unlock the operating system so you can install unapproved apps, deleted unwanted unwanted software, update the OS, replace the firmware, overclock (or underclock) the processor, customize, and so on.|
|Device Specification|Line Speed|Wi-Fi line speed.|
|Device Specification|Low Memory |Indicates whether the OS considers itself to currently be in a low memory situation.|
|Device Specification|MAC Address|MAC address of the WLAN interface/Wi-Fi network adapter MAC.|
|Device Specification|Manufacturer|Manufacturer of the product/hardware.|
|Device Specification|Max CPU Frequency|Maximum CPU frequency that can run on the device.|
|Device Specification|Min CPU frequency|Minimum CPU frequency that can run on the device.|
|Device Specification|Model|End-user-visible name for the end product.|
|Device Specification|Network Country ISO|Country code for the subscriber’s cellular provider, represented as an ISO 3166-1 country code string. Only provided when the user is registered to a network. The result may be unreliable on CDMA networks.|
|Device Specification|Network Operator|Carrier that physically delivers the data. This value can change if the device moves.|
|Device Specification|OS Architecture|OS architecture. For example, armv7l.|
|Device Specification|OS Name|OS name. For example, Linux.|
|Device Specification|Phone Type|Type of radio used to transmit voice calls. For example, GSM, CDMA, SIP, None.|
|Device Specification|Product|Name of the overall product. |
|Device Specification|Radio Version|Radio firmware version.|
|Device Specification|Refresh Rate|Refresh rate of the display in frames per second.|
|Device Specification|Rotation|Orientation of this display.  Value is ROTATION_0, ROTATION_90, ROTATION_180 or ROTATION_270.|
|Device Specification|Screen Density|Logical density of the display.|
|Device Specification|Screen DPI|Screen density expressed as dots-per-inch.|
|Device Specification|Screen Size in Pixels|Absolute width and height of the available display size in pixels.|
|Device Specification|Screen DPI X |Exact physical pixels per inch of the screen in the X dimension.|
|Device Specification|Screen DPI Y |Exact physical pixels per inch of the screen in the Y dimension.|
|Device Specification|SDK Version |SDK version of the software currently running on this hardware device.|
|Device Specification|SDK Device ID|SDK device ID generated on first use.|
|Device Specification|Hardware Serial Number|Hardware serial number.|
|Device Specification|Signal Strength|Wi-Fi signal strength.|
|Device Specification|SIM Configured Count|Number of logical modems currently configured to be activated. Returns zero (0) if none of voice, SMS, data isn't supported. Returns one (1) for single standby mode (single SIM functionality). Returns two (2) for dual standby mode (dual SIM functionality). Returns three (3) for tri standby mode (tri SIM functionality).|
|Device Specification|SIM Country ISO|SIM provider's country code.|
|Device Specification|SIM Operator Name|SIM provider’s operator name.  |
|Device Specification|SIM Serial Number|SIM serial number used for international identification. Sometimes called the Integrated Circuit Card ID (ICC-ID).|
|Device Specification|SIM State|State of default SIM. For example, UNKNOWN, ABSENT, SIM locked requires PIN to unlock, SIM locked requires PUK to unlock.|
|Device Specification|SIM Network Type|Current data connection. For example, GPRS, EDGE, CDMA, 1xRTT, IDEN, UMTS, EVDO_0, EDO_A, HSDPA. |
|Device Specification|Subscriber ID|Unique subscriber ID. For example, the IMSI for a GSM phone. Returns null if it's unavailable.|
|Device Specification|Supported ABIs|Ordered list of ABIs supported by this device. For example, armeabi-v7a.|
|Device Specification|Supports Multiple Users|Indicates whether the device supports multiple users with their own login and customizable space.|
|Device Specification|System Uptime|Time since last reboot.|
|Device Specification|Tags|Comma-separated tags describing the build. For example, unsigned, debug.|
|Device Specification|Technology|Technology of the current battery.|
|Device Specification|Temperature|Current battery temperature.|
|Device Specification|Time|Time and date of when the ROM and Kernel were built together.|
|Device Specification|Total External Storage|Total external storage in bytes for device.|
|Device Specification|Total Internal Storage|Total internal storage in bytes for device.|
|Device Specification|Total Memory|Total RAM memory on device in bytes.|
|Device Specification|Type|Type of build. For example, user, eng.|
|Device Specification|Unique Number|Unique device number, if available. Can be IMEI, MEID, ESN, or IMSI.|
|Device Specification|User Serial Number|Serial number for a user. This is a device-unique number assigned to that user. If the user is deleted and a new user created, the new user isn't given the same serial number.|
|Device Specification|Voltage|Current battery voltage level.|
|Device Specification|Wi-Fi SSID|Service set identifier (SSID) of the current 802.11 network.|
|Device Specification|IP Address V4 (IPV4)|IP address V4.|
|Gyroscope|Gyroscope Data|Gyroscope sensor reading.|
|Gyroscope|Gyroscope Name|Name string of gyroscope sensor. For example, MPU6515 Gyroscope.|
|Gyroscope|Gyroscope Power|Power in mA used by gyroscope sensor while in use.|
|Gyroscope|Gyroscope Vendor Name |Vendor of gyroscope sensor. For example, InvenSense.|
|Gyroscope|Gyroscope Version |Version of the gyroscope sensor's module.|
|Location|Altitude|Altitude of the location in meters. Can be positive (above sea level) or negative (below sea level). |
|Location|Device GPS Location |Current location data (latitude, longitude).|
|Location|Is GPS Enabled|Boolean value indicating whether GPS is enabled.|
|Location|Is Network Provider Enabled|Boolean value indicating whether the network provider is enabled.|
|Model Output|Bot Score|Score from the Bot model.|
|User Preference|24 Hour Clock Format|Display times as 12 or 24 hours.|
|User Preference|Activity List on Launcher Screen|List of all home apps that can be used as starting apps when the device boots.|
|User Preference|Actual Default Alarm Ringtone|Type that refers to sounds that are used for the alarm. |
|User Preference|Actual Default Notification Ringtone|Type that refers to sounds that are used for notifications.|
|User Preference|Actual Default Ringtone|Type that refers to sounds that are used for the phone ringer.|
|User Preference|Date Format|Date format used by user. For example, mm/dd/yyyy, dd/mm/yyyy.|
|User Preference|Default Browser Package|Default browser app used by user. For example, Edge.|
|User Preference|Default Font Size in Pixels|Default font size (in pixels) in TextView.|
|User Preference|Default Input Language |Default input language used by user. For example, EN.|
|User Preference|Default Input Package |Default input method apps used by user. For example, Keyboards.|
|User Preference|Default Text-to-Speech Engine|Default text to speech engine.|
|User Preference|Default Text-to-Speech Engine Pitch|Default text-to-speech engine speech pitch. For example, 100 = 1x.|
|User Preference|Default Text-to-Speech Engine Speech Rate|Default text-to-speech engine speech rate. For example, 100 = 1x.|
|User Preference|End Call Behavior|Behavior when the user presses the end call button if they're not on a call.|
|User Preference|Font Scale|Scaling factor for fonts.|
|User Preference|HTTP Proxy |Host name and port for global HTTP proxy.|
|User Preference|Input Methods Package List |List of all input method apps installed by user.|
|User Preference|Installer Package Name|Name of the application that installed a package.|
|User Preference|Is ADB Enabled|Boolean value indicating whether ADB is enabled. Android Debug Bridge (ADB) is a versatile command-line tool that lets you communicate with a device.|
|User Preference|Is Airplane Mode Enabled|Boolean value indicating whether Airplane Mode is on.|
|User Preference|Is Auto Caps Enabled|Boolean value indicating whether the setting to enable Auto Caps in text editors is enabled.|
|User Preference|Is Auto Punctuate Enabled|Boolean value indicating whether the setting to enable Auto Punctuate in text editors is enabled.|
|User Preference|Is Auto Replace Enabled|Boolean value indicating whether the setting to enable Auto Replace (AutoText) in text editors is enabled.|
|User Preference|Is Auto Rotate Accelerometer Enabled|Boolean value indicating whether the accelerometer is used to change screen orientation.|
|User Preference|Is Auto Screen Brightness Enabled|Boolean value indicating whether automatic brightness mode is enabled.|
|User Preference|Is Auto Time Enabled|Boolean value indicating whether the user prefers the date, time, and time zone to be automatically fetched from the network.|
|User Preference|Is Auto Time Zone Enabled|Boolean value indicating whether the user prefers the time zone to be automatically fetched from the network.|
|User Preference|Is Bluetooth Enabled|Boolean value indicating whether Bluetooth is enabled.|
|User Preference|Is Development Setting Enabled|Boolean value indicating whether the user enabled development settings.|
|User Preference|Is Device Provisioned|Boolean value indicating whether the device is provisioned. On a multiuser device with a separate system user, the screen may be locked as soon as this attribute is set to **true** and further activities can't be launched on the system user unless they're marked to show over keyguard.|
|User Preference|Is Dial Pad Enabled|Boolean value indicating whether the audible DTMF tones are played by the dialer when dialing.|
|User Preference|Is Haptic Feedback Enabled|Boolean value indicating whether haptic feedback is enabled.|
|User Preference|Is Install Non-Market Apps Enabled|Boolean value indicating whether nonmarket applications, such as apps not from Google Play, can be installed for this user.|
|User Preference|Is Lock Pattern Enabled|Boolean value indicating whether auto lock is enabled (API <= 22).|
|User Preference|Is Lock Pattern Visible|Boolean value indicating whether lock pattern is visible as user enters (API <= 22).|
|User Preference|Is Show Password Enabled|Boolean value indicating whether the setting to show password characters in text editors is enabled.|
|User Preference|Is Sound Effects Enabled|Boolean value indicating whether sounds effects, such as key clicks and lid open are enabled.|
|User Preference|Is Stay On Plugged In Enabled|Boolean value indicating whether the setting to keep the device on while the device is plugged in (during charge) is enabled.|
|User Preference|Is Vibrate On|Boolean value indicating whether vibrate is on for different events.|
|User Preference|Is Wallpaper Present|Boolean value indicating if the current wallpaper is a live wallpaper component.|
|User Preference|Is Device Secure|Boolean value indicating whether the device is secured with a PIN, pattern, or password (API>22).|
|User Preference|Launcher Screen App Package Name|Home app, or the first app that is displayed when the Android device boots.|
|User Preference|List of Browser Packages|List of all browser apps installed by user. For example, Edge, Chrome.|
|User Preference|List of SMS Viewer Packages|List of all SMS viewer apps installed by user.|
|User Preference|List of Phone Call Packages|List of all phone call apps installed by user.|
|User Preference|Phone Call Package|Default phone call app used by user.|
|User Preference|Ringer Mode|Ringer mode. For example, silent, vibrate, normal.|
|User Preference|Screen Brightness|Screen backlight brightness value between 0 and 255.|
|User Preference|Screen Off Timeout|Amount of time in milliseconds before the device goes to sleep or begins to dream after a period of inactivity.|
|User Preference|Settings Class Name|Name shown when **Settings** is selected from **All Applications**. |
|User Preference|SMS Viewer Package |Default SMS viewer app used by user.|
|User Preference|Time Zone Offset|Amount of time in milliseconds to add to UTC to get standard time in current time zone. This value is referred to as raw offset since it's not affected by daylight saving time.|
|User Preference|Wallpaper Package Name|.apk package that implements the wallpaper.|

## Interpreting fingerprinting response to detect VPNs

There are two fields that exist in the **Account Create**, **Account Login**, and **Purchase API** response that can be used to identify VPNs:
- Proxy: A boolean indicating if Fraud Protection detected a proxy or not.
- ProxyType: An enum. The following table provides the enum values for each ProxyType.

  |ProxyType |Description|
  |----------|-----------|
  | http | The proxy uses the HTTP protocol and has open ports, which are accessible by any Internet user. |
  | service | The proxy is operated by an organization (often for profit) that provides access to subscribers as a service. The proxy is one of an array of proxies (often internationally distributed) that are part of a Virtual Private Network (VPN) that subscribers connect to by installing an application. The network may have different proxy locations or bandwidth options depending on the user’s membership level, whether it's paid or free. |
  | socks | The proxy uses the Socket Secure (SOCKS) protocol and has open ports, which are accessible by any Internet user. |
  | socks http | The proxy has both the HTTP and SOCKS protocols set up and has open ports, which are accessible by any Internet user. |
  | tor | The proxy is part of the onion router (Tor) network. Encrypted user Internet traffic is routed through a regularly changing series of nodes operated by volunteers. |
  | unknown | The proxy’s type couldn't be determined. |
  | web | The proxy operates by using an Internet web browser. Navigate to the web proxy website, enter the URL of the site you wish to visit, and the contents of the requested URL are returned by the web proxy website within the browser. |

For example, to identify a VPN, Proxy would be **TRUE** and ProxyType would be **service**.

## Additional resources

[Implement device fingerprinting in Dynamics 365 Fraud Protection](/training/modules/device-fingerprint-fraud-protection/).

[!INCLUDE[footer-include](includes/footer-banner.md)]
