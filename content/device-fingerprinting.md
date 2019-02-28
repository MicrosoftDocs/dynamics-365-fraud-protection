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

> [!NOTE]
> Device fingerprinting does not require any software installation. 

1.	Insert HTML tags to engage device profiling. For more information, see 'To integrate device fingerprinting with your website.'
1.	Create a public DNS record fpt.Your_Root_Domain.com pointing to fpt.microsoft.com.

*Example*

Partner WebSite: account.windowsazure.com
DNS record     : fpt.windowsazure.com points to fpt.microsoft.com

1.	Onboard your root domain.

For contextual and sequential device fingerprinting flows, see the following diagrams.

2 diagrams for placeholders.

- Consumer opens Add PI, Sign In, or Check-out page (with device fingerprinting tag in iFrame):
    - Fetches bootstrapping code.
    - Fetches custom-generated JavaScript.
    - Uploads device forensic data JavaScript.
    - Using Flash, fetches Flash movie.
    - Upload device forensics data.
- If profiled domain is not rooted to .microsoft.com, fetches inner flash movie.
- Uploads flash cookie if profiled domain is not rooted to .microsoft.com. 

## To integrate device fingerprinting with your website

1.	Insert profiling tag on web pages for profiling user’s devices. Place the tag within an iFrame.
1.	If your website DNS name is not a subdomain of microsoft.com, let us  know your DNS domain name such that we can make necessary
changes on our side. This will enable maximum label collection (some browsers will attempt to block third-party domains).

## Profiling tag

A device fingerprinting profiling tag is placed in the HTML page of your web application. This step enables us to collect labels that
better describe a user’s device and browser. Your web application should serve the device fingerprinting before submitting a transaction
(such as Add PI, Sign in, or Check out). The following sample HTML shows the profiling tag.

**session_id**: A user session unique identifier.
**pctx**: Optional name value collection (partner-provided data about the user, FormId and SubmitId) for further processing.

*Example*

**PROD**:

```https://fpt.microsoft.com/tags?session_id=2da53453-ab08-40a0adc8705429bfd80&pctx=sim%3D8923440000000000003%26amp%3BuserId%3Dtest%40contoso.com```

**INT**

```https://fpt.microsoft-int.com/tags?session_id=2da53453-ab08-40a0-adc8-c705429bfd80&pctx=sim%3D8923440000000000003%26amp%3BuserId%3Dtest%40contoso.com```

Hide the iFrame to ensure that it does not interfere visually with your web page. This is commonly done by setting both the height and
width to zero. However, not all browsers behave the same with respect to downloading content into a zero-sized iFrame. To optimize
device fingerprinting, we recommend setting the dimensions of the iFrame to 100, and then position it out of view. The following example
shows a hidden iFrame to better expose embedding profiling tags.

**IFrame Example**

```<iframe  style="color:rgb(0,0,0);  float:left; position:absolute; top:-200px; left:-200px; border:0px" src="https://fpt.microsoft.com/tags?session_id=<session_id>" height=100  width=100></iframe>```

**session_id**: The session_id is an identifier that is unique to the device user’s session. It can be up to 128 bytes long and can only consist of the following characters: upper and lowercase English letters, digits, underscore or hyphen ([a-z], [A-Z], 0-9, _, -).

## Device fingerprinting API

After successfully profiling a user’s device, a REST API call is required to obtain labels from your back-end systems for further fraud
analysis. This REST API call returns all the labels that describe a customer’s device collected during its profiling. You must pass in
the session_id used to identify a profiling session.

### HTTP content types

All request/response payloads must be in the form of application/json with UTF-8 encoding.

Retrieve a session forensic resource:

    Get [Forensics](http://.../api/SessionForensics/{session_id})

Request payload:

    Not applicable.

Response payload:

    For a complete list, see Device labels.

*Example*

<table>
    <tr>
      <th>API Details</th>
      <th>Description</th>
    </tr>
    <tr>
      <td>URL</td>
      <td>http://.../api/SessionForensics/{session_id}</td>
    </tr>
    <tr>
      <td>HTTP Verb</td>
      <td>GET</td>
    </tr>
    <tr>
      <td>Request Payload</td>
      <td>None</td>
    </tr>
    <tr>
      <td>Response Payload</td>
      <td>{<br/>
      time_zone_dst_offset: 60<br/>
 time_zone: 480<br/>
device_id: "a8d0e3ea-977a-4e90-899b-e350230f73b0"<br/>
mime_type_number: 2<br/>
page_time_on: 157<br/>
profiled_domain: "forensicswd.microsoft.com"<br/>
profiled_url: "https://forensicswd.microsoft.com/"<br/>
location_header:"https://df.cp.microsoft.com/check"<br/>
profiling_datetime: 1422318249<br/>
browser_string_anomaly: true<br/>
browser_string_mismatch: true<br/>
browser_language_anomaly : false<br/>
plugin_number: 0<br/>
plugin_hash: ""<br/>
true_ip: "10.125.140.119"<br/>
os_fonts_number: 0<br/>
screen_dpi: 0<br/>
session_id: "20b90bbf-bd85-4c70-b2ae-6db18f79cac3"<br/>
session_anomaly: "yes"<br/>
processorClass: ""<br/>
session_control: 1030<br/>
device_control: 0<br/>
headers_name_value_hash: "F101A712C81F00861AF4603C54A43BDF"<br/>
headers_order_string_hash: "D1EF717C7AFA27A32CC246323DDA64C0"<br/>
browser_http_signature: "1:Connection=[Close],Content-Type=[application/json],Accept-Language=[en-US,en;q=0.8],?Cookie,Host,?Referer,User-Agent,api-version=[2014-09-30],x-ms-tracking-id=[0ede9403-849b-4336-b885-416718565cae],x-ms-correlation-id=[dcd9c043-1766-4c54-94fc-f3f4ec8852e"<br/>
flash_headers_name_value_hash: ""<br/>
flash_headers_order_string_hash: ""<br/>
flash_headers_nvp: ""<br/>
profiled_domain_first_seen: "1/26/2015 4:24:09 PM"<br/>
flashcallback_ip: ""<br/>
scriptcallback_ip: "10.125.140.119"<br/>
flash_os: ""<br/>
flash_lang: ""<br/>
flash_version: ""<br/>
flash_oem: ""<br/>
os_fonts_hash: ""<br/>
mime_type_hash: "N0ZGNkM2MTRBMzQwRkY1MjAwMzUxNjYwRkMyREE4ODI"<br/>
proxy_ip: ""<br/>
screen_color_depth: 0<br/>
screen_res: "1920x1080"<br/>
js_browser_string: ""<br/>
scriptUserAgentHashcode: ""<br/>
browser_string: "GreenID Client.exe"<br/>
browser_string_hash: "58537642C2D5E63995C18E4C31A0DF53"<br/>
browser_language: "en-gb,en"<br/>
raw_tcpip_signature: "4:128+0:0:1460:8192,8:mss,nop,ws,sok,ts:df,id+:0"<br/>
raw_tcpip_signature_hash: "80EE98730F3A1C1F8997A95CD840899B"<br/>
raw_ssl_signature: "3.1:002F,0035,0005,000A,C013,C014,C009,C00A,0032,0038,0013,0004:0000:65281,0,10,11:3.1"<br/>
raw_ssl_signature_hash: "026B0BEC6BF391EB7FE4F03FD5398768"<br/>
canvas_hash: ""<br/>
fuzzy_device_id: "0b4f2142-86d7-4373-b197-6c8b30601c50"<br/>
fuzzy_device_id_confidence: 100<br/>
fuzzy_device_result: "not found"<br/>
fuzzy_device_match_result: "new_device"<br/>
up_time: "0 Days 5 Hrs 7 Minutes"<br/>
tcp_os_signature: "Windows:7 or 8"<br/>
link-type: "Ethernet or modem"<br/>
detected_fl: true<br/>
plugin_flash: "true"<br/>
plugin_windows_media_player: "12.0.7601.17514"<br/>
plugin_adobe_acrobat: "7.0/later"<br/>
plugin_silverlight: "5.1.20913.0"<br/>
plugin_quicktime: "false"<br/>
plugin_shockwave: "false"<br/>
plugin_realplayer: "false"<br/>
plugin_vlc_player: "false"<br/>
plugin_devalvr: "false"<br/>
plugin_svg_viewer: "false"<br/>
plugin_java: "false"<br/>
flash_anomaly: "yes"<br/>
os: "other"<br/>
ua_os: "Unknown"<br/>
ua_browser: "Unknown"<br/>
ua_platform: "Unknown"<br/>
http_os_signature: "Unknown"<br/>
ua_mobile: "False"<br/>
agent_type: "browser_computer"<br/>
ssl_os_signature: "Windows2008 R2"<br/>
device_match_result: "known_device"<br/>
enabled_ck: "yes"<br/>
enabled_js: "yes"<br/>
enabled_fl: "no"<br/>
enabled_im: "yes"<br/>
}</td>
    </tr>
</table>

## Retrieve an IP address activity
```Get http://.../api/IpAddressActivity/{ip_address}```

Request payload

    Not applicable.
    
Response payload

    Array of IP address activity.
    
|SI |Name  |Description  |
|---|---|---|
|1   |device_id   |Cookie-based device ID.   |
|2   |fuzzy_device_id   |Device fuzzy ID.   |
|3   |profiled_domain   |Application domain IP visited.   |

*Example*

|API Item   |Description   |
|---|---|
|URL   |http://.../api/   |
|HTTP Verb   |GET   |
|Request Payload   |None   |
|Response Payload   |"[{\"device_id\":\"a6421486-3ea2-456d-94eb-23245aa21488\",\"fuzzy_device_id\":\"fb8ea081-96bb-4f25-a452-aab8cbf49060\",\"profiled_domain\":\"df.cp.microsoft.com\"}]"   |

## Device labels 

The labels query REST API return these labels.

| Sl. | Label name                      | Description                                                                                 |
|-----|---------------------------------|---------------------------------------------------------------------------------------------|
| 1   | agent_type                      | Device browser type.                                                                        |
| 2   | browser_http_signature          | Browser HTTP signature.                                                                     |
| 3   | browser_language                | Browser language.                                                                           |
| 4   | browser_language_anomaly        | Invalid language code.                                                                      |
| 5   | browser_string                  | UserAgent string communicated in the HTTP header.                                           |
| 6   | browser_string_anomaly          | Boolean indicating UserAgent is unusual.                                                    |
| 7   | browser_string_hash             | MD5 Hash of browser_string label.                                                           |
| 8   | browser_string_mismatch         | Boolean indicating JavaScript UserAgent is different from browser.                          |
| 9   | canvas_hash                     | Browser engine canvas hash.                                                                 |
| 10  | detected_fl                     | Boolean indicating if flash is detected by JavaScript.                                      |
| 11  | device_control                  | Device state bitmask.                                                                       |
| 12  | device_id                       | Globally unique identifier generated by Microsoft Device Fingerprinting.                    |
| 13  | device_match_result             |                                                                                             |
| 14  | enabled_ck                      | Boolean indicating whether cookie is enabled.                                               |
| 15  | enabled_fl                      | Boolean indicating whether Flash is enabled.                                                |
| 16  | enabled_im                      | Boolean indicating whether image is enabled.                                                |
| 17  | enabled_js                      | Boolean indicating whether JavaScript is enabled.                                           |
| 18  | flash_anomaly                   | Boolean indicating whether flash is disabled.                                               |
| 19  | flash_headers_name_value_hash   | Flash HTTP signature hash.                                                                  |
| 20  | flash_headers_nvp               | Flash HTTP signature.                                                                       |
| 21  | flash_headers_order_string_hash | Flash HTTP header order hash.                                                               |
| 22  | flash_lang                      | OS language reported by Flash.                                                              |
| 23  | flash_oem                       | Flash vendor.                                                                               |
| 24  | flash_os                        | OS detected by Flash.                                                                       |
| 25  | flash_version                   | Flash version.                                                                              |
| 26  | flashcallback_ip                | Flash callback IP address.                                                                  |
| 27  | fuzzy_device_id                 | Globally unique identifier generated by fuzzy matching all labels that describe the device. |
| 28  | fuzzy_device_id_confidence      |                                                                                             |
| 29  | fuzzy_device_match_result       |                                                                                             |
| 30  | fuzzy_device_result             |                                                                                             |
| 31  | headers_name_value_hash         | Browser HTTP signature hash.                                                                |
| 32  | headers_order_string_hash       | Browser HTTP header order hash.                                                             |
| 33  | http_os_signature               | OS as indicated by Browser UserAgent.                                                       |
| 34  | js_browser_string               | UserAgent string as visible to JavaScript.                                                  |
| 35  | link_type                       | Data connection type.                                                                       |
| 36  | Location_header                 | Script location header.                                                                     |
| 37  | mime_type_hash                  | Hash of all mime types supported by the browser.                                            |
| 38  | mime_type_number                | Mime types supported by the browser.                                                        |
| 39  | os                              | Operating system as indicated by the device browser.                                        |
| 40  | os_fonts_hash                   | Hash of fonts installed on the device.                                                      |
| 41  | os_fonts_number                 | Number of fonts install on the device.                                                      |
| 42  | page_time_on                    |                                                                                             |
| 43  | plugin_adobe_acrobat            | Version number or true.                                                                     |
| 44  | plugin_devalvr                  | Version number or true.                                                                     |
| 45  | plugin_flash                    | Version number or true.                                                                     |
| 46  | plugin_hash                     | Hash of all installed browser plug-ins.                                                     |
| 47  | plugin_java                     | Version number or true.                                                                     |
| 48  | plugin_number                   | Number of plug-ins.                                                                         |
| 49  | plugin_quicktime                | Version number or true.                                                                     |
| 50  | plugin_realplayer               | Version number or true.                                                                     |
| 51  | plugin_shockwave                | Version number or true.                                                                     |
| 52  | plugin_silverlight              | Version number or true.                                                                     |
| 53  | plugin_svg_viewer               | Version number or true.                                                                     |
| 54  | plugin_vlc_player               | Version number or true.                                                                     |
| 55  | plugin_windows_media_player     | Version number or true.                                                                     |
| 56  | Processor_class                 | Device processor.                                                                           |
| 57  | profiled_domain                 | Profile domain.                                                                             |
| 58  | profiled_domain_first_seen      | Profile domain first seen.                                                                  |
| 59  | profiled_url                    | Url of the page that profile tags.                                                          |
| 60  | profiling_datetime              | Profiled datetime Unix stamp.                                                               |
| 61  | proxy_ip                        |                                                                                             |
| 62  | raw_ssl_signature               | Device SSL signature.                                                                       |
| 63  | raw_ssl_signature_hash          | Device SSL signature hash.                                                                  |
| 64  | raw_tcpip_signature             | Device TCP/IP stack signature.                                                              |
| 65  | raw_tcpip_signature_hash        | Device TCP/IP stack signature hash.                                                         |
| 66  | screen_color_depth              | Device screen color depth.                                                                  |
| 67  | screen_dpi                      | Device screen DPI.                                                                          |
| 68  | screen_res                      | Device screen resolution.                                                                   |
| 69  | scriptcallback_ip               | Script call back IP.                                                                        |
| 70  | scriptUserAgentHashcode         | Hash code of js_browser_string.                                                             |
| 71  | session_anomaly                 | Its Boolean indicating whether any of the following detected:<br/>1. MUID cookie changed during profiling.<br/>2. IP changes detected.|
| 72  | session_control                 |                                                                                             |
| 73  | session_id                      | The device profiling session identifier.                                                    |
| 74  | ssl_os_signature                | OS detected by device SSL fingerprint.                                                      |
| 75  | tcp_os_signature                | OS detected by device TCP/IP fingerprint.                                                   |
| 76  | time_zone_dst_offset            | UTC day list time offset.                                                                   |
| 77  | time_zone                       | UTC Time zone.                                                                              |
| 78  | true_ip                         | Device IP.                                                                                  |
| 79  | ua_browser                      | Browse as indicated by UserAgent.                                                           |
| 80  | ua_mobile                       | Is mobile?                                                                                  |
| 81  | ua_os                           | OS as indicated by UserAgent.                                                               |
| 82  | ua_platform                     | Browser platform.                                                                           |
| 83  | up_time                         | System up time.                                                                             |

## raw_tcpip_signature

Device fingerprinting uses a passive fingerprinting technique to silently analyze TCP/IP communication; TCP SYN packet. Its signature format follows.

```VER:TTL+dist:Options Size:MaximumSegmentSize:WindowSize,WindowScale:Options:Quirks```

| Sl. | Name         | Description                                           |
|-----|--------------|-------------------------------------------------------|
| 1   | VER          | IP version; IPv4 (‘4’) or IPv6 (‘6’).                 |
| 2   | TTL          | Observed TTL + distance.                              |
| 3   | Options Size | IPv4 options length; 0 for IPv6.                      |
| 4   | MSS          | Maximum segment size.                                 |
| 5   | Windows Size | Windows size.                                         |
| 6   | WS           | Windows scaling factor.                               |
| 7   | Options      | Comma-delimited ordered layout of TCP options.        |
| 8   | Quirks       | Comma-delimited quirks observed in IP or TCP headers. |
 
 ## raw_ssl_signature
 
The SSL signature is computed by analyzing the unencrypted ClientHello packet exchanged between device and Web Server as part of the SSL protocol handshake. The ClientHello TCP packet is unaltered by proxies or routers en route. The SSL signature format follows.
 
 ```sslver:ciphers:extensions:sslflags```
 
| Sl. | Name       | Description                                          |
|-----|------------|------------------------------------------------------|
| 1   | sslver     | SSL record version; most of the web browsers use v3. |
| 2   | ciphers    | List of supported encryption algorithms.             |
| 3   | extensions | List of supported compression methods.               |
| 4   | sslFlags   | List of SSL extensions.                              |
 
##  Error handling
 
 The REST API typically returns either 200 or 404. Your application should
interpret these values as follows:

1.  The 200 HTTP status code means success, and the response contains key-value
    pairs of the user’s device labels.

2.  The 404 HTTP status code means session_id was not found.

>   If the request_result key is equal to “success,” this indicates that the
>   input parameters were formatted correctly, and the request was successfully
>   processed. Other values indicate an error condition (described in the
>   request_result description in the following table).

## Geoavailability

The following table shows the device fingerprinting solution availability in
different datacenters.

| Datacenter | Availability                | Remarks          |
|------------|-----------------------------|------------------|
| DM2C       | Available                   |                  |
| CO1C       | Being built                 |                  |
| C04        | Available                   | INT environment. |
| DB         | Available in April/May 2018 |                  |
| BN         | Available in April/May 2018 |                  |
| CYS        | Available in April/May 2018 |                  |
| HK         | Available in April/May 2018 |                  |
