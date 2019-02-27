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

## HTTP content types

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
&nbsp;device_id: "a8d0e3ea-977a-4e90-899b-e350230f73b0"<br/>
&#160;mime_type_number: 2<br/>
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

<insert table>

## raw_tcpip_signature

Device fingerprinting uses a passive fingerprinting technique to silently analyze TCP/IP communication; TCP SYN packet. Its signature format follows.

```VER:TTL+dist:Options Size:MaximumSegmentSize:WindowSize,WindowScale:Options:Quirks```

<insert table>
 
 ## raw_ssl_signature
 
The SSL signature is computed by analyzing the unencrypted ClientHello packet exchanged between device and Web Server as part of the SSL protocol handshake. The ClientHello TCP packet is unaltered by proxies or routers en route. The SSL signature format follows.
 
 ```sslver:ciphers:extensions:sslflags```
 
 <insert table>
 
##  Error handling
 
 
 
 
 
 
 
 
 
 
