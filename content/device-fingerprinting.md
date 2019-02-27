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

[!NOTE] Device fingerprinting does not require any software installation. 

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

| API Details  |Description   |
|---|---|
| URL  | http://.../api/SessionForensics/{session_id} |
| HTTP Verb  |GET   |
|Request Payload   | None  |
| Response Payload  |{ time_zone_dst_offset: 60
time_zone: 480
device_id: "a8d0e3ea-977a-4e90-899b-e350230f73b0"
mime_type_number: 2
page_time_on: 157
profiled_domain: "forensicswd.microsoft.com"
profiled_url: "https://forensicswd.microsoft.com/"
location_header:"https://df.cp.microsoft.com/check"
profiling_datetime: 1422318249
browser_string_anomaly: true
browser_string_mismatch: true
browser_language_anomaly : false
plugin_number: 0
plugin_hash: ""
true_ip: "10.125.140.119"
os_fonts_number: 0
screen_dpi: 0
session_id: "20b90bbf-bd85-4c70-b2ae-6db18f79cac3"
session_anomaly: "yes"
processorClass: ""
session_control: 1030
device_control: 0
headers_name_value_hash: "F101A712C81F00861AF4603C54A43BDF"
headers_order_string_hash: "D1EF717C7AFA27A32CC246323DDA64C0"
browser_http_signature: "1:Connection=[Close],Content-Type=[application/json],Accept-Language=[en-US,en;q=0.8],?Cookie,Host,?Referer,User-Agent,api-version=[2014-09-30],x-ms-tracking-id=[0ede9403-849b-4336-b885-416718565cae],x-ms-correlation-id=[dcd9c043-1766-4c54-94fc-f3f4ec8852e"
flash_headers_name_value_hash: ""
flash_headers_order_string_hash: ""
flash_headers_nvp: ""
profiled_domain_first_seen: "1/26/2015 4:24:09 PM"
flashcallback_ip: ""
scriptcallback_ip: "10.125.140.119"
flash_os: ""
flash_lang: ""
flash_version: ""
flash_oem: ""
os_fonts_hash: ""
mime_type_hash: "N0ZGNkM2MTRBMzQwRkY1MjAwMzUxNjYwRkMyREE4ODI"
proxy_ip: ""
screen_color_depth: 0
screen_res: "1920x1080"
js_browser_string: ""
scriptUserAgentHashcode: ""
browser_string: "GreenID Client.exe"
browser_string_hash: "58537642C2D5E63995C18E4C31A0DF53"
browser_language: "en-gb,en"
raw_tcpip_signature: "4:128+0:0:1460:8192,8:mss,nop,ws,sok,ts:df,id+:0"
raw_tcpip_signature_hash: "80EE98730F3A1C1F8997A95CD840899B"
raw_ssl_signature: "3.1:002F,0035,0005,000A,C013,C014,C009,C00A,0032,0038,0013,0004:0000:65281,0,10,11:3.1"
raw_ssl_signature_hash: "026B0BEC6BF391EB7FE4F03FD5398768"
canvas_hash: ""
fuzzy_device_id: "0b4f2142-86d7-4373-b197-6c8b30601c50"
fuzzy_device_id_confidence: 100
fuzzy_device_result: "not found"
fuzzy_device_match_result: "new_device"
up_time: "0 Days 5 Hrs 7 Minutes"
tcp_os_signature: "Windows:7 or 8"
link-type: "Ethernet or modem"
detected_fl: true
plugin_flash: "true"
plugin_windows_media_player: "12.0.7601.17514"
plugin_adobe_acrobat: "7.0/later"
plugin_silverlight: "5.1.20913.0"
plugin_quicktime: "false"
plugin_shockwave: "false"
plugin_realplayer: "false"
plugin_vlc_player: "false"
plugin_devalvr: "false"
plugin_svg_viewer: "false"
plugin_java: "false"
flash_anomaly: "yes"
os: "other"
ua_os: "Unknown"
ua_browser: "Unknown"
ua_platform: "Unknown"
http_os_signature: "Unknown"
ua_mobile: "False"
agent_type: "browser_computer"
ssl_os_signature: "Windows2008 R2"
device_match_result: "known_device"
enabled_ck: "yes"
enabled_js: "yes"
enabled_fl: "no"
enabled_im: "yes"
}
   |



