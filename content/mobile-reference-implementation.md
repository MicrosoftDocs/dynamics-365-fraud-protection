---
author: josaw1
description: This topic provides the information that is required for device fingerprinting in a Microsoft Dynamics 365 Fraud Protection mobile device implementation.
ms.author: josaw
ms.date: 12/07/2021
ms.topic: reference
search.app: 
  - Capaedac-fraudprotection
search.audienceType:
  - developer
title: Dynamics 365 Fraud Protection mobile reference implementation
ms.custom:
---

# Dynamics 365 Fraud Protection mobile reference implementation

Microsoft Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI), runs on Azure, is cloud-scalable and reliable, and has enterprise-grade security. The device fingerprinting functionality enables the identification, across multiple sessions or interactions, of devices that engage with your business and other businesses in the Fraud Protection fraud network. These devices might be, for example, computers, Xbox consoles, or tablets. Additionally, the functionality enables Fraud Protection to link together seemingly unrelated events in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by integrating the reference implementation that is provided in your app, you agree to the [Microsoft APIs Terms of Use](/legal/microsoft-apis/terms-of-use). Additionally, you direct Microsoft to process the following types of data from the devices that interact with the Fraud Protection services. (These types of data are referred to collectively as *the device fingerprinting data*.)

- Device attributes, such as the device ID, screen information, and processor class
- Operating system (OS) attributes, such as OS information, the OS version, and original equipment manufacturer (OEM) details
- Applicable browser-related attributes, such as the browser language and apps that are installed by default

You have the following responsibilities:

- Receive consent from your users to collect and allow Microsoft to process the device fingerprinting data.
- Inform your customers about your data collection and processing practices. For example, disclose the data that you collect, and explain how it is used.
- Disclose your use of third parties that work on your behalf to process the data that you collect. These third parties include Fraud Protection service providers.
- Comply with all laws and regulations that are applicable to the use of Fraud Protection. These laws and regulations include data protection laws.

To integrate device fingerprinting for Fraud Protection, you must complete the following tasks:

1. Set up the Azure Domain Name System (DNS) by following the steps in [Set up DNS and SSL certificate](device-fingerprinting.md#set-up-dns-and-ssl-certificate).
1. Integrate device fingerprinting with your mobile application by using the reference implementation that is provided.

## Attribute categories

This section provides a list of the device fingerprinting data that Microsoft might process and the reason for processing that data. Each data attribute that is described in the following list is optional. You can configure the number of attributes that best reflects the needs of your organization in relation to the privacy rights of device users in your jurisdiction.

Each attribute belongs to one of the following categories:

- **Core Features** – Attributes in this category are core to Fraud Protection's ability to predict patterns of fraud. Based on previous experience, Microsoft believes that these attributes will be highly accretive to Fraud Protection's model performance and its ability to detect distinctive patterns of fraud. If these core features aren't provided, device fingerprinting will be inaccurate.
- **Investigative Features** – Attributes in this category might be able to increase or enhance Fraud Protection's ability to accurately predict patterns of fraud. Statistical analysis of collected data is the only definitive way to determine whether these attributes are strong predictors of patterns of fraud. If the predictive capability of these attributes doesn't meet Microsoft expectations, we will no longer use them. Although this category of attributes will enable Microsoft to determine whether the attributes will be strong predictors of patterns of fraud, they are optional.
- **Potential Label** – Attributes in this category are used for model supervision and labeling purposes. There is some probability that each of these attributes on its own won't provide ground truth. However, when the attributes are combined, it's more likely that the label that is used during training of Fraud Protection's model will become ground truth and that model performance will therefore increase. Although Fraud Protection can work without these attributes, the machine learning model won't be able to improve without them.

## Android attributes for the mobile reference implementation

| Code | Name | Permission | Group | Attribute description | Attribute category | Baseline stack level |
|------|------|------------|-------|-----------------------|--------------------|----------------------|
| A1 | DeviceId | Not applicable | DEVICE SPECIFICATION | The device ID that is generated on the device at first use. | Core Features | 31 |
| A2 | OS architecture | Not applicable | DEVICE SPECIFICATION | The OS architecture (for example, armv7l). | Potential Label | 31 |
| A3 | OS name | Not applicable | DEVICE SPECIFICATION | The OS name (for example, Linux). | Potential Label | 31 |
| A4 | AppVersionName | Not applicable | DEVICE SPECIFICATION | The version name of the app. | Potential Label | 31 |
| A5 | AppVersionCode | Not applicable | DEVICE SPECIFICATION | The version number of the app. | Potential Label | 31 |
| A6 | Application label | Not applicable | DEVICE SPECIFICATION | The label that is associated with the app. | Potential Label | 31 |
| A7 | SystemUpTime | Not applicable | DEVICE SPECIFICATION | The time since restart. | Investigative Features | 31 |
| A8 | Advertising_ID | Not applicable | DEVICE SPECIFICATION | The advertising ID. This identifier is appropriate for ad use cases. It can be reset by the user. For more information, see [Work with advertising IDs](https://developer.android.com/training/articles/user-data-ids#advertising-ids). | Core Features | 31 |
| A9 | IsDeviceRooted | Not applicable | DEVICE SPECIFICATION | Rooting is a way to unlock the OS so that you can install unapproved apps, delete unwanted bloatware, update the OS, replace the firmware, overclock (or underclock) the processor, customize anything, and perform other operations. | Potential Label | 31 |
| B1 | IsDeviceEmulator | Not applicable | DEVICE SPECIFICATION | The Android Emulator simulates Android devices on your computer so that you can test your app on a variety of devices and at a variety of Android application programming interface (API) levels without having to have each physical device. | Potential Label | 31 |
| B6 | SIM state | Not applicable | DEVICE SPECIFICATION | The state of the default subscriber identification module (SIM) (for example, UNKNOWN, ABSENT, SIM locked requires PIN to unlock, or SIM locked requires PUK to unlock). | Investigative Features | 31 |
| B7 | Phone type | Not applicable | DEVICE SPECIFICATION | The type of radio that is used to transmit voice calls (GSM, CDMA, SIP, or None). | Potential Label | 31 |
| B8 | NetworkOperator | Not applicable | DEVICE SPECIFICATION | The carrier that physically delivers the data. The carrier changes if the device moves. | Potential Label | 31 |
| B9 | NetworkCountryISO | Not applicable | DEVICE SPECIFICATION | A value is provided only when the user is registered to a network. The result might be unreliable on code-division multiple access (CDMA) networks. (Use **getPhoneType()** to determine whether the user is on a CDMA network.) | Core Features | 31 |
| C1 | Sim Operator Name | Not applicable | DEVICE SPECIFICATION | The provider of your data. | Core Features | 31 |
| C3 | Sim Country ISO | Not applicable | DEVICE SPECIFICATION | The country/region code of the SIM provider. | Investigative Features | 31 |
| C5 | Cellular DataState | Not applicable | DEVICE SPECIFICATION | The current cellular data connection state (DISCONNECTED, CONNECTED, or SUSPENDED). | Investigative Features | 31 |
| C6 | Sim configured count | Not applicable | DEVICE SPECIFICATION | <p>The number of logical modems that are currently configured to be activated. The following values are returned:</p><ul><li>"0" (zero) if voice, Short Message Service (SMS), and data aren't supported</li><li>"1" for single standby mode (single-SIM functionality)</li><li>"2" for dual standby mode (dual-SIM functionality)</li><li>"3" for tri-standby mode (tri-SIM functionality)</li></ul> | Investigative Features | 31 |
| D8 | Screen size in pixels | Not applicable | DEVICE SPECIFICATION | The absolute width and height of the available display, in pixels. | Investigative Features | 31 |
| D9 | Screen density | Not applicable | DEVICE SPECIFICATION | The logical density of the display. | Investigative Features | 31 |
| E1 | Screen xdpi | Not applicable | DEVICE SPECIFICATION | The exact physical pixels per inch of the screen in the X dimension. | Investigative Features | 31 |
| E2 | Screen ydpi | Not applicable | DEVICE SPECIFICATION | The exact physical pixels per inch of the screen in the Y dimension. | Investigative Features | 31 |
| E3 | Screen dpi | Not applicable | DEVICE SPECIFICATION | The screen density expressed in dots per inch (DPI). | Investigative Features | 31 |
| E4 | Category of screen size | Not applicable | DEVICE SPECIFICATION | Small, normal, large, x-large, or undefined. | Investigative Features | 31 |
| E5 | Display Id | Not applicable | DEVICE SPECIFICATION | Each logical display has a unique ID. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| E6 | RefreshRate | Not applicable | DEVICE SPECIFICATION | The refresh rate of the display expressed in frames per second (FPS). | Investigative Features | 31 |
| E7 | Rotation | Not applicable | DEVICE SPECIFICATION | The orientation of the display (ROTATION_0, ROTATION_90, ROTATION_180, or ROTATION_270). | Investigative Features | 31 |
| E8 | Battery level | Not applicable | DEVICE SPECIFICATION | The current battery level. | Potential Label | 31 |
| E9 | Is battery charging | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the battery is being charged. | Potential Label | 31 |
| F1 | Charge type | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the device is plugged in to a power source. A value of "0" (zero) indicates that the device is on battery power. Other values represent different types of power sources. | Potential Label | 31 |
| F2 | Temperature | Not applicable | DEVICE SPECIFICATION | The current battery temperature. | Potential Label | 31 |
| F3 | Technology | Not applicable | DEVICE SPECIFICATION | The technology of the current battery. | Potential Label | 31 |
| F4 | Voltage | Not applicable | DEVICE SPECIFICATION | The current voltage level of the battery. | Potential Label | 31 |
| H5 | Board | Not applicable | DEVICE SPECIFICATION | The name of the underlying board (for example, "goldfish"). | Potential Label | 31 |
| H6 | Bootloader | Not applicable | DEVICE SPECIFICATION | The version number of the system bootloader. | Investigative Features | 31 |
| H7 | Brand | Not applicable | DEVICE SPECIFICATION | Any consumer-visible brand that the product/hardware will be associated with. | Potential Label | 31 |
| H8 | Device | Not applicable | DEVICE SPECIFICATION | The name of the industrial design. This name is the device name that is provided by the manufacturer (for example, Bravo, Passion, or GT-I9000). | Potential Label | 31 |
| H9 | Display | Not applicable | DEVICE SPECIFICATION | A build ID string that is shown to the user. | Investigative Features | 31 |
| I1 | Hardware | Not applicable | DEVICE SPECIFICATION | The name of the hardware (from the kernel command line or /proc). | Potential Label | 31 |
| I2 | Host | Not applicable | DEVICE SPECIFICATION | The name of the person who builds the read-only memory (ROM) and kernel. | Potential Label | 31 |
| I3 | ID | Not applicable | DEVICE SPECIFICATION | A build change list number, or a label (for example, "M4-rc20"). | Core Features | 31 |
| I4 | Manufacturer | Not applicable | DEVICE SPECIFICATION | The manufacturer of the product/hardware. | Potential Label | 31 |
| I5 | Model | Not applicable | DEVICE SPECIFICATION | The end product name that is visible to the end user. | Potential Label | 31 |
| I6 | Product | Not applicable | DEVICE SPECIFICATION | The name of the overall product. | Potential Label | 31 |
| I7 | Radio version | Not applicable | DEVICE SPECIFICATION | The radio firmware version. | Investigative Features | 31 |
| I9 | Type | Not applicable | DEVICE SPECIFICATION | The type of build (for example, "user" or "eng"). | Potential Label | 31 |
| J1 | Tags | Not applicable | DEVICE SPECIFICATION | Comma-separated tags that describe the build (for example, "unsigned" or "debug"). | Investigative Features | 31 |
| J2 | Supported ABIS | Not applicable | DEVICE SPECIFICATION | An ordered list of application binary interfaces (ABIs) that the device supports (for example, armeabi-v7a). | Potential Label | 31 |
| J3 | Time | Not applicable | DEVICE SPECIFICATION | The time and date when the ROM and kernel were built together. | Potential Label | 31 |
| J4 | SDK version | Not applicable | DEVICE SPECIFICATION | The software development kit (SDK) version of the software that is currently running on the hardware device. | Potential Label | 31 |
| J5 | Code name | Not applicable | DEVICE SPECIFICATION | The current development code name, or the string "REL" for a release build. | Potential Label | 31 |
| J6 | Total memory | Not applicable | DEVICE SPECIFICATION | The total random-access memory (RAM) for the device. | Investigative Features | 31 |
| J7 | Available memory | Not applicable | DEVICE SPECIFICATION | The currently available RAM for the device. | Investigative Features | 31 |
| J8 | Low memory | Not applicable | DEVICE SPECIFICATION | A value that indicates that the OS currently considers itself to be in a low-memory situation. | Investigative Features | 31 |
| J9 | CPU usage | Not applicable | DEVICE SPECIFICATION | The current central processing unit (CPU) usage by the device (for example, 0.39). | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| K1 | CPU info hash | Not applicable | DEVICE SPECIFICATION | The CPU information hashed by MD5. | Core Features | 31 |
| K2 | CPU number of cores | Not applicable | DEVICE SPECIFICATION | The number of processors that are available to the Java virtual machine. | Potential Label | 31 |
| K3 | Max CPU frequency | Not applicable | DEVICE SPECIFICATION | The maximum frequency that the CPU can run at on the device. | Potential Label | 31 |
| K4 | Min CPU frequency | Not applicable | DEVICE SPECIFICATION | The minimum frequency that the CPU can run at on the device. | Potential Label | 31 |
| K5 | Total internal storage | Not applicable | DEVICE SPECIFICATION | The total internal storage for the device, in bytes. | Potential Label | 31 |
| K6 | Available internal storage | Not applicable | DEVICE SPECIFICATION | The available internal storage for the device, in bytes. | Potential Label | 31 |
| K7 | Is external memory mounted | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the external memory card (SD Card) is mounted. | Potential Label | 31 |
| K8 | Total external storage | Not applicable | DEVICE SPECIFICATION | The total external storage for the device, in bytes. | Potential Label | 31 |
| K9 | Available external storage | Not applicable | DEVICE SPECIFICATION | The available external storage for the device, in bytes. | Potential Label | 31 |
| G4 | Accelerometer name | Not applicable | ACCELEROMETER | The name string of the Accelerometer sensor (for example, MPU6515 Accelerometer). | Investigative Features | 31 |
| G5 | Accelerometer vendor name | Not applicable | ACCELEROMETER | The vendor of the Accelerometer sensor (for example, InvenSense). | Investigative Features | 31 |
| G6 | Accelerometer power | Not applicable | ACCELEROMETER | The power that is used by the Accelerometer sensor while it's in use, in milliamps (mA). | Potential Label | 31 |
| G7 | Accelerometer version | Not applicable | ACCELEROMETER | The version of the Accelerometer sensor's module. | Potential Label | 31 |
| G8 | Accelerometer data | Not applicable | ACCELEROMETER | The Accelerometer sensor reading. | Investigative Features | 31 |
| G9 | Gyroscope name | Not applicable | GYROSCOPE | The name string of the Gyroscope sensor (for example, MPU6515 Gyroscope). | Potential Label | 31 |
| H1 | Gyroscope vendor name | Not applicable | GYROSCOPE | The vendor of the Gyroscope sensor (for example, InvenSense). | Potential Label | 31 |
| H2 | Gyroscope power | Not applicable | GYROSCOPE | The power that is used by the Gyroscope sensor while it's in use, in mA. | Investigative Features | 31 |
| H3 | Gyroscope version | Not applicable | GYROSCOPE | The version of the Gyroscope sensor's module. | Potential Label | 31 |
| H4 | Gyroscope data | Not applicable | GYROSCOPE | The Gyroscope sensor reading. | Investigative Features | 31 |
| L2 | Is auto rotate accelerometer enabled? | Not applicable | USER PREFERENCE | This attribute controls whether the accelerometer will be used to change the screen orientation. | Investigative Features | 31 |
| L3 | Is ADB enabled? | Not applicable | USER PREFERENCE | A value that indicates whether Android Debug Bridge (ADB) is enabled. ADB is a versatile command-line tool that lets you communicate with a device. | Investigative Features | 31 |
| L4 | Is airplane mode on? | Not applicable | USER PREFERENCE | A value that indicates whether airplane mode is on. | Investigative Features | 31 |
| L5 | Is auto time enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the user prefers that the date, time, and time zone be automatically fetched from the network. | Investigative Features | 31 |
| L6 | Is auto time zone enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the user prefers that the time zone be automatically fetched from the network. | Investigative Features | 31 |
| L7 | Is Bluetooth enabled? | Not applicable | USER PREFERENCE | A value that indicates whether Bluetooth is enabled or disabled. | Investigative Features | 31 |
| L8 | Date format | Not applicable | USER PREFERENCE | The date format that is used by user (for example, mm/dd/yyyy or dd/mm/yyyy). | Potential Label | Deprecated (However, it might be available from an earlier version of the stack.) |
| L9 | Is device provisioned? | Not applicable | USER PREFERENCE | On a multiuser device that has a separate system user, the screen might be locked as soon as this attribute is set to true. No further activities can be started on the system user unless they are marked to appear over the keyguard. | Investigative Features | 31 |
| M1 | Is development setting enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the user has enabled development settings. | Investigative Features | 31 |
| M2 | Is dial pad enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the audible dual-tone multi-frequency signaling (DTMF) tones are played by the dialer during dialing. | Investigative Features | 31 |
| M3 | End call behavior | Not applicable | USER PREFERENCE | This attribute determines what happens when the user presses the end call button if they aren't on a call. | Potential Label | 31 |
| M4 | Font scale | Not applicable | USER PREFERENCE | The scaling factor for fonts. | Investigative Features | 31 |
| M5 | Is haptic feedback enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the haptic feedback (for example, long presses) is enabled. | Investigative Features | 31 |
| M6 | HTTP proxy | Not applicable | USER PREFERENCE | The host name and port for the global HTTP proxy. | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| M8 | Is lock pattern enabled? | Not applicable | USER PREFERENCE | A value that indicates whether autolock is enabled (API \<= 22). | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| M9 | Is lock pattern visible? | Not applicable | USER PREFERENCE | A value that indicates whether the lock pattern is visible as the user enters it (API \<= 22). | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| N1 | Ringer mode | Not applicable | USER PREFERENCE | The ringer mode (for example, silent, vibrate, or normal). | Investigative Features | 31 |
| N2 | Screen brightness | Not applicable | USER PREFERENCE | The brightness of the screen backlight expressed as a value between 0 (zero) and 255. | Investigative Features | 31 |
| N3 | Is auto screen brightness enabled? | Not applicable | USER PREFERENCE | This attribute controls whether automatic brightness mode is enabled. | Investigative Features | 31 |
| N4 | Screen off timeout | Not applicable | USER PREFERENCE | The amount of time in milliseconds before the device goes to sleep or begins to dream after a period of inactivity. | Investigative Features | 31 |
| N5 | Settings class name | Not applicable | USER PREFERENCE | The settings class name to open when **Settings** is selected from **All Applications**. | Potential Label | Deprecated (However, it might be available from an earlier version of the stack.) |
| N6 | Is sound effects enabled? | Not applicable | USER PREFERENCE | A value that indicates whether sounds effects (for example, key clicks or lid open) are enabled. | Investigative Features | 31 |
| N7 | Is stay on plugged in enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the user keeps the device on while it's plugged in (during charge). | Investigative Features | 31 |
| N8 | Is auto caps enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the setting to enable auto-caps in text editors is enabled. | Investigative Features | 31 |
| N9 | Is auto punctuate? | Not applicable | USER PREFERENCE | A value that indicates whether the setting to enable auto-punctuation in text editors is enabled. | Investigative Features | 31 |
| O1 | Is auto replace enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the setting to enable auto-replace (auto text) in text editors is enabled. | Investigative Features | 31 |
| O2 | Is show password enabled? | Not applicable | USER PREFERENCE | A value that indicates whether the setting to show password characters in text editors is enabled. | Investigative Features | 31 |
| O3 | 24 hour clock format | Not applicable | USER PREFERENCE | A value that indicates whether times are shown in 12-hour or 24-hour format. | Investigative Features | 31 |
| O4 | Is vibrate on? | Not applicable | USER PREFERENCE | A value that indicates whether vibrate is on for different events. | Investigative Features | 31 |
| O5 | Default text-to-speech engine | Not applicable | USER PREFERENCE | The default text-to-speech engine. | Potential Label | 31 |
| O6 | Default text-to-speech engine speech rate | Not applicable | USER PREFERENCE | The speech rate of the default text-to-speech engine (for example, 100 = 1×). | Investigative Features | 31 |
| O7 | Default text-to-speech engine pitch | Not applicable | USER PREFERENCE | The speech pitch of the default text-to-speech engine (for example, 100 = 1×). | Investigative Features | 31 |
| O9 | Actual default ringtone | Not applicable | USER PREFERENCE | The type that refers to sounds that are used for the phone ringer. | Investigative Features | 31 |
| P1 | Actual default notification ringtone | Not applicable | USER PREFERENCE | The type that refers to sounds that are used for notifications. | Investigative Features | 31 |
| P2 | Actual default alarm ringtone | Not applicable | USER PREFERENCE | The type that refers to sounds that are used for the alarm. | Investigative Features | 31 |
| P3 | Launcher screen app package name | Not applicable | USER PREFERENCE | The home app, which is the first app that is shown when the Android device starts. | Investigative Features | 31 |
| P4 | Activity list on launcher screen | Not applicable | USER PREFERENCE | A list of all home apps that can used as the starting app when the device starts. | Investigative Features | 31 |
| P5 | Default browser package | Not applicable | USER PREFERENCE | The default browser app that is used by the user (for example, Edge). | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| P6 | List of browser packages | Not applicable | USER PREFERENCE | A list of all browser apps that have been installed by the user (for example, Edge, Chrome). | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| P7 | SMS viewer package | Not applicable | USER PREFERENCE | Th default SMS viewer app that is used by the user. | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| P8 | List of SMS viewer packages | Not applicable | USER PREFERENCE | A list of all SMS viewer apps that have been installed by the user. | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| P9 | Phone call package | Not applicable | USER PREFERENCE | The default phone call app that is used by the user. | Investigative Features | 31 |
| Q1 | List phone call packages | Not applicable | USER PREFERENCE | A list of all phone call apps that have been installed by the user. | Investigative Features | 31 |
| Q2 | Default input package | Not applicable | USER PREFERENCE | The default input method app that is used by the user (for example, keyboards). | Potential Label | 31 |
| Q3 | Input methods package list | Not applicable | USER PREFERENCE | A list of all input method apps that have been installed by the user. | Investigative Features | 31 |
| Q4 | Default input language | Not applicable | USER PREFERENCE | The default input language that is used by the user (for example, en). | Investigative Features | 31 |
| Q5 | Time zone offset | Not applicable | USER PREFERENCE | The amount of time in milliseconds to add to Coordinated Universal Time (UTC) to get standard time in the time zone. Because this value isn't affected by daylight saving time, it's known as *raw offset*. | Investigative Features | 31 |
| Q6 | Default font size in pixels | Not applicable | USER PREFERENCE | The default font size in TextView, in pixels. | Investigative Features | 31 |
| Q7 | Is wall paper present | Not applicable | USER PREFERENCE | A value that indicates whether the current wallpaper is a live wallpaper component. | Investigative Features | 31 |
| Q8 | Wallpaper pkg name | Not applicable | USER PREFERENCE | The .apk package that implements the wallpaper. | Investigative Features | 31 |
| Q9 | IsDeviceSecure | Not applicable | USER PREFERENCE | A value that indicates whether the device is secured by using a personal identification number (PIN), pattern, or password (API \> 22). | Potential Label | 31 |
| R1 | Installer package name | Not applicable | USER PREFERENCE | The package name of the app that installed a package. | Investigative Features | 31 |
| R2 | Supports multiple users | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the device supports multiple users who have their own sign-in and customizable space. | Potential Label | 31 |
| R3 | User serial number | Not applicable | DEVICE SPECIFICATION | The serial number for a user. The serial number is a device-unique number that is assigned to the user. If the user is deleted, and a new user is created, the same serial number won't be assigned to the new user. | Potential Label | 31 |
| R4 | App package name | Not applicable | DEVICE SPECIFICATION | The name of app's package. | Potential Label | 31 |
| R5 | App directory path | Not applicable | DEVICE SPECIFICATION | The absolute path of the directory on the filesystem where files that are created by using openFileOutput are stored. | Potential Label | 31 |
| B2 | ANDROID_ID | Not applicable | DEVICE SPECIFICATION | On Android 8.0 (API level 26) and later versions of the platform, a 64-bit number (expressed as a hexadecimal string) that is unique to each combination of an app signing key, a user, and a device. Values of **ANDROID_ID** are scoped by signing key and user. The value might change if a factory reset is done on the device, or if an Android Package (APK) signing key changes. | Core Features | 31 |
| B3 | GSF_ID | com.google.android.providers.gsf.permission.READ_GSERVICES | DEVICE SPECIFICATION | The Google Services Framework Identifier (GSF ID), which is a unique 16-character hexadecimal number that the device automatically requests from Google as soon as a user signs in to their Google account for the first time. For a specific device, the GSF ID changes only after a factory reset. | Core Features | 31 |
| B4 | Unique number | android.permission.READ_PHONE_STATE (RunTime) | DEVICE SPECIFICATION | The International Mobile Equipment Identity (IMEI), mobile equipment identifier (MEID), electronic serial numbers (ESN), or international mobile subscriber identity (IMSI). | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| B5 | Subscriber ID | android.permission.READ_PHONE_STATE (RunTime) | DEVICE SPECIFICATION | The unique subscriber ID (for example, the IMSI for a Global System for Mobile Communications \[GSM\] phone). If the subscriber ID is unavailable, null is returned. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| C2 | SIM serial number | android.permission.READ_PHONE_STATE (RunTime) | DEVICE SPECIFICATION | The SIM serial number, which is used for international identification. It's sometimes referred to as the Integrated Circuit Card ID (ICC-ID). | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| I8 | Serial | android.permission.READ_PHONE_STATE (RunTime) | DEVICE SPECIFICATION | The hardware serial number. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| C4 | SimNetworkType | android.permission.READ_PHONE_STATE (RunTime) | DEVICE SPECIFICATION | The current data connection (for example, GPRS, EDGE, CDMA, 1xRTT, IDEN, UMTS, EVDO_0, EDO_A, or HSDPA) | Investigative Features | 31 |
| C7 | DataNetworkType | android.permission.ACCESS_NETWOR,K_STATE | DEVICE SPECIFICATION | A human-readable name that describes the type of the network (for example, "WIFI" or "MOBILE"). | Investigative Features | 31 |
| C8 | Is the device connected to the network? | android.permission.ACCESS_NETWORK_STATE | DEVICE SPECIFICATION | A value that indicates whether network connectivity exists, connections can be established, and data can be passed. | Potential Label | 31 |
| C9 | Is the device roaming? | android.permission.ACCESS_NETWORK_STATE | DEVICE SPECIFICATION | A value that indicates whether the device is currently roaming on the network. A value of true suggests that use of data on the network might incur extra costs. | Potential Label | 31 |
| D1 | Is WIFI enabled? | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | A value that indicates whether Wi-Fi is enabled or disabled. | Investigative Features | 31 |
| D2 | MAC address | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | The Wi-Fi network adopter media access control (MAC). The value specifies the MAC address of the wireless local area network (WLAN) interface. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| D3 | Line speed | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | The Wi-Fi line speed. | Investigative Features | 31 |
| D4 | Signal strength | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | The Wi-Fi signal strength. | Investigative Features | 31 |
| D5 | WifiSSID | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | The service set identifier (SSID) of the current 802.11 network. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| D6 | IPAddressV4 (IPV4) | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | The Internet Protocol version 4 (IPv4) address. | Core Features | 31 |
| D7 | Configured networks SSIDs | android.permission.ACCESS_WIFI_STATE | DEVICE SPECIFICATION | A list of all the network-configured SSIDs for the current foreground user. | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| F5 | Bluetooth address | android.permission.BLUETOOTH | DEVICE SPECIFICATION | The hardware address of the local Bluetooth adapter (for example, 00:11:22:AA:BB:CC). | Core Features | Deprecated (However, it might be available from an earlier version of the stack.) |
| F6 | Bluetooth adapter name | android.permission.BLUETOOTHandroid.permission.BLUETOOTH_CONNECT (RunTime) | DEVICE SPECIFICATION | The friendly Bluetooth name of the local Bluetooth adapter. This name is visible to remote Bluetooth devices. | Investigative Features | 31 |
| F7 | BlueToothState | android.permission.BLUETOOTH | DEVICE SPECIFICATION | The current state of the local Bluetooth adapter. | Potential Label | 31 |
| F9 | Is GPS enabled? | android.permission.ACCESS_COARSE_LOCATION (RunTime) | LOCATION | A value that indicates whether the Global Positioning System (GPS) is enabled or disabled. | Potential Label | 31 |
| G1 | Device GPS location | android.permission.ACCESS_COARSE_LOCATION (RunTime) | LOCATION | The current location data (latitude, longitude). | Core Features | 31 |
| G2 | Is network provider enabled? | android.permission.ACCESS_COARSE_LOCATION (RunTime) | LOCATION | A value that indicates whether the network is enabled or disabled. | Core Features | 31 |
| G3 | Altitude | android.permission.ACCESS_COARSE_LOCATION (RunTime) | LOCATION | The altitude of the location, in meters. The value can be positive (above sea level) or negative (below sea level). | Core Features | 31 |
| M7 | Is install non-market apps enabled? | android.permission.REQUEST_INSTALL_PACKAGES | USER PREFERENCE | A value that indicates whether non-market applications (that is, apps that aren't from Google Play) can be installed for the user. | Investigative Features | Deprecated (However, it might be available from an earlier version of the stack.) |

## Android technical reference

1. Download the [Android reference implementation](https://go.microsoft.com/fwlink/?linkid=2138490).
1. Import the library module into your project by following these steps. The library source becomes part of your project.

    1. Select **File \> New \> Import Module**.
    1. Enter the location of the library module directory, and then select **Finish**.

The library module is copied to your project. You can edit the library code.

1. Make sure that the library is listed at the top of your settings.gradle file, as shown here for a library that is named "&nbsp;:DynamicsFP".

    `include ':Demo', ':DynamicsFP'`

1. Open the app module's build.gradle file, and add a new line to the dependencies block, as shown in the following example.

    `dependencies { implementation project(":DynamicsFP") }`

1. Select **Sync Project with Gradle Files**.

You can initiate the reference implementation by calling the following process.

```plaintext
import com.microsoft.dynamicsfp.androidsdk.DynamicsFP;

*DynamicsFP.start(getApplicationContext(), \$tenantId);*

\$tenantId :Provided by Microsoft(GUID/UUID)
```

You can initiate the reference implementation code on the base application class, so that it can start to collect device attributes. The reference implementation doesn't prompt the user for runtime permission.

You can send the collected device attributes to Fraud Protection by calling Fraud Protection in the following way.


```plaintext
import com.microsoft.dynamicsfp.androidsdk.DynamicsFP;

*DynamicsFP.send(\$pageId);*

\$pageId(Optional): SI=SignIn, SU=SignUp, P= Purchase
```

You can call **send()** in any fragment/activity either before or on the page that has the operation that you need a risk assessment for. For a sign-in/sign-up scenario, you can call **send()** immediately after **start()** in the base application class.

A session ID is required when you call the risk assessment APIs. To get the session ID when you need it, call `*String sessionId = DynamicsFP.getSessionId();*`. 

### Android runtime permissions

Reference implementations rely on the following runtime permissions to collect different device data:

- android.permission.ACCESS_COARSE_LOCATION
- android.permission.READ_PHONE_STATE
- android.permission.BLUETOOTH_CONNECT

However, the reference implementation doesn't prompt the user for any runtime permissions. The app should obtain the runtime permissions from the user.

## Android additional references

[Android API Reference](https://developer.android.com/reference)

[About permissions](https://developer.android.com/training/permissions/requesting)

[App manifest file](https://developer.android.com/guide/topics/manifest/manifest-intro)

[Add dependency](https://developer.android.com/studio/projects/android-library#AddDependency)

[Determine sensitive data access needs](https://developer.android.com/games/develop/permissions)

[Android Legal Notice](https://developer.android.com/legal)

## iOS attributes for the mobile reference implementation

| Code | Type | Name | Permission | Group | Attribute description | Attribute category |
|------|------|------|------------|-------|-----------------------|--------------------|
| A1 | String | DeviceId | Not applicable | DEVICE SPECIFICATION | The device ID that is generated on the device at first use. | Core Features |
| A2 | String | BundleIdentifier | Not applicable | DEVICE SPECIFICATION | The bundle identifier that uniquely identifies an application in Apple's ecosystem. | Investigative Features |
| A3 | String | BundleName | Not applicable | DEVICE SPECIFICATION | The short name of the bundle. | Investigative Features |
| A4 | String | AppVersionName | Not applicable | DEVICE SPECIFICATION | The app version (for example, 4.3.1). | Investigative Features |
| A5 | String | AppVersionCode | Not applicable | DEVICE SPECIFICATION | The app build code (for example, 230, A1160). | Not applicable |
| A7 | Long | SystemUpTime | Not applicable | DEVICE SPECIFICATION | The amount of time that the system has been awake since it was last restarted. | Potential Label |
| A8 | String | Advertising_ID | Not applicable | DEVICE SPECIFICATION | An alphanumeric string that is unique to each device. It's used only to serve advertisements. In iOS 10.0 and later, the value of advertisingIdentifier is all zeroes when the user has limited ad tracking. Unlike the [identifierForVendor](https://developer.apple.com/documentation/uikit/uidevice/1620059-identifierforvendor) property of [UIDevice](https://developer.apple.com/documentation/uikit/uidevice), the same value is returned to all vendors. This identifier might change (for example, if the user erases the device). Therefore, you should not cache it. | Core Features |
| A9 | Bool | IsDeviceRooted | Not applicable | DEVICE SPECIFICATION | IsDeviceJailBroken: Jailbreaking changes the OS that is running on an iPhone or iPod touch to give you more control. | Potential Label |
| B1 | Bool | IsDeviceEmulator | Not applicable | DEVICE SPECIFICATION | IsDeviceSimulator: The iOS simulator lets users use features and run applications on the virtual iPhone on their MacBook as though it were an actual iPhone device. | Potential Label |
| B8 | String | NetworkOperator | Not applicable | DEVICE SPECIFICATION | CarrierName: The name of the subscriber's cellular service provider (for example, AT&T). | Potential Label |
| B9 | String | NetworkCountryISO | Not applicable | DEVICE SPECIFICATION | ISOCountryCode: The country/region code for the subscriber's cellular service provider. It's represented by an International Organization for Standardization (ISO) 3166-1 country/region code string. | Potential Label |
| C1 | String | MobileCountryCode | Not applicable | DEVICE SPECIFICATION | The mobile country/region code for the subscriber's cellular service provider. | Potential Label |
| C2 | String | MobileNetworkCode | Not applicable | DEVICE SPECIFICATION | The mobile network code for the subscriber's service provider. | Potential Label |
| C3 | Bool | AllowsVOIP | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the carrier allows Voice over Internet Protocol (VoIP) calls to be made on its network. | Investigative Features |
| C4 | String | SimNetworkType | Not applicable | DEVICE SPECIFICATION | RadioAccessTechnology: The current radio access technology for each service that the device is registered with. The value can be nil if the device isn't registered on any network. | Potential Label |
| C7 | String | DataNetworkType | Not applicable | DEVICE SPECIFICATION | The network that is reachable over Wi-Fi or mobile. | Potential Label |
| C8 | Bool | IsConnected | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the network is currently reachable. | Investigative Features |
| D6 | String | IPAddressV4 (IPV4) | Not applicable | DEVICE SPECIFICATION | The IPv4 address. | Core Features |
| D7 | String | IPAddressV6 (IPV6) | Not applicable | DEVICE SPECIFICATION | IPv6 address. | Core Features |
| D8 | Int | Screen size in pixels | Not applicable | DEVICE SPECIFICATION | The absolute width and height of the available display, in pixels. | Investigative Features |
| D9 | Int | The screen size, in points. | Not applicable | DEVICE SPECIFICATION | The absolute width and height of the available display, in points. | Investigative Features |
| E1 | Float | Scale | Not applicable | DEVICE SPECIFICATION | The natural scale factor that is associated with the screen. | Investigative Features |
| E2 | Float | NativeScale | Not applicable | DEVICE SPECIFICATION | The native scale factor for the physical screen. | Investigative Features |
| E3 | Bool | IsCaptured | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the contents of the screen are being cloned to another destination (iOS \>= 11). | Investigative Features |
| E4 | Bool | ScreenWantsSoftwareDimming | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the screen can be dimmed lower than the hardware is usually capable of by emulating it in software. | Investigative Features |
| E5 | Bool | supportsFocus | Not applicable | DEVICE SPECIFICATION | A value that indicates whether the screen supports focus-based inputs. | Investigative Features |
| E6 | Float | RefreshRate | Not applicable | DEVICE SPECIFICATION | MaxFramesPerSecond: The maximum number of frames per second that the screen is capable of (iOS \>= 10.3). | Potential Label |
| E8 | Int | BatteryLevel | Not applicable | DEVICE SPECIFICATION | The battery charge level for the device. | Potential Label |
| E9 | Bool | IsBatteryCharging | Not applicable | DEVICE SPECIFICATION | The battery power state of the device. | Potential Label |
| H4 | String | IdentifierForVendor | Not applicable | DEVICE SPECIFICATION | A universally unique identifier (UUID) that can be used to uniquely identify the device. The value of this attribute is the same for apps that run on the same device and come from the same vendor and. A different value is returned for apps that run on the same device but come from different vendors, and for apps that run on different devices, regardless of the vendor. Usually, the vendor is determined based on data that is provided by the App Store. If the app wasn't installed from the App Store (for example, if it's an enterprise app or is still in development), a vendor identifier is calculated based on the app's bundle ID. The bundle ID is assumed to be in reverse DNS format. | Core Features |
| H6 | String | DeviceSystemName | Not applicable | DEVICE SPECIFICATION | The name of the OS that is running on the device that is represented by the receiver (for example, iOS). | Investigative Features |
| H7 | String | DeviceSystemVersion | Not applicable | DEVICE SPECIFICATION | The current version of the OS (for example, 12.0.1). | Investigative Features |
| H8 | String | UserInterfaceIdiom | Not applicable | DEVICE SPECIFICATION | The style of interface to use on the current device (for example, iPhone or iPad). | Investigative Features |
| H9 | String | DeviceModelName | Not applicable | DEVICE SPECIFICATION | The actual device model name that is used by Apple (for example, iPhone 7, iPhone 8 plus, or iPhone XS Max). | Potential Label |
| I1 | String | KernelSysName | Not applicable | DEVICE SPECIFICATION | The kernel OS name (for example, Darwin or Linux). | Investigative Features |
| I2 | String | KernelOsReleaseName | Not applicable | DEVICE SPECIFICATION | The kernel OS release (for example, 18.0.3). | Investigative Features |
| I4 | Bool | IsMultitaskingSupported | Not applicable | DEVICE SPECIFICATION | A Boolean value that indicates whether multitasking is supported on the current device. | Investigative Features |
| I6 | String | ProcessName | Not applicable | DEVICE SPECIFICATION | The name of the process. | Investigative Features |
| I7 | Int | ProcessIdentifier | Not applicable | DEVICE SPECIFICATION | The identifier of the process (often referred to as the process ID). | Investigative Features |
| I8 | String | ProcessGloballyUniqueString | Not applicable | DEVICE SPECIFICATION | The globally unique identifier (GUID) for the process. | Investigative Features |
| I9 | String | ProcessOSVersionString | Not applicable | DEVICE SPECIFICATION | A string that contains the version of the OS that the process is running on. | Investigative Features |
| J1 | String | ThermalState | Not applicable | DEVICE SPECIFICATION | The current thermal state, which is used to determine whether your app should reduce system usage. | Investigative Features |
| J2 | Bool | IsLowPowerModeEnabled | Not applicable | DEVICE SPECIFICATION | A value that indicates whether low power mode is enabled on an iOS device. | Investigative Features |
| J3 | Int | ActiveProcessorCount | Not applicable | DEVICE SPECIFICATION | The number of active processing cores that are available on the device. | Investigative Features |
| J4 | Int | ProcessorCount | Not applicable | DEVICE SPECIFICATION | The number of processing cores that are available on the device. | Investigative Features |
| J5 | DoubleArray | CPUUsage | Not applicable | DEVICE SPECIFICATION | The CPU usage by device (0.39, System, User, Idle, Nice). | Investigative Features |
| J6 | Long | TotalMemory | Not applicable | DEVICE SPECIFICATION | The total RAM on the device, in bytes. | Potential Label |
| J7 | LongArray | MemoryUsage | Not applicable | DEVICE SPECIFICATION | The RAM usage by the device, in bytes (Free, Active, Inactive, Wired). | Potential Label |
| K5 | Long | TotalInternalStorage | Not applicable | DEVICE SPECIFICATION | The total internal storage for the device, in bytes. | Potential Label |
| K6 | Long | AvailableInternalStorage | Not applicable | DEVICE SPECIFICATION | The available internal storage for the device, in bytes. | Potential Label |
| L1 | DoubleArray | AccelerometerData | Not applicable | ACCELEROMETER | The accelerometer reading (X-axis, Y-axis, Z-axis). | Investigative Features |
| L2 | Double | AccelerometerDataTimeStamp | Not applicable | ACCELEROMETER | The time when the accelerometer data is valid. | Investigative Features |
| M1 | DoubleArray | GyroscopeData | Not applicable | GYROSCOPE | The gyroscope reading (X-axis, Y-axis, Z-axis). | Investigative Features |
| M2 | Double | GyroscopeDataTimeStamp | Not applicable | GYROSCOPE | The time when the gyroscope data is valid. | Investigative Features |
| O1 | Double | Brightness | Not applicable | USER PREFERENCE | The screen brightness. | Investigative Features |
| O2 | String | CurrentScreenSizeInPixel | Not applicable | USER PREFERENCE | The current maximum screen width, in pixels. | Investigative Features |
| O4 | Float | CurrentPixelAspectRatio | Not applicable | USER PREFERENCE | The aspect ratio of a single pixel. The ratio is defined as X ÷ Y. | Investigative Features |
| O5 | String | DeviceOrientation | Not applicable | USER PREFERENCE | The physical orientation of the device. | Investigative Features |
| O6 | Bool | IsValidInterfaceOrientation | Not applicable | USER PREFERENCE | A value that indicates whether the specified orientation is a portrait or landscape orientation.| Investigative Features |
| O7 | Bool | IsGeneratingDeviceOrientationNotifications | Not applicable | USER PREFERENCE | A value that indicates whether the receiver generates orientation notifications. | Investigative Features |
| O8 | String | PassCodeOrBiometryIsEnabled | Not applicable | USER PREFERENCE | The passcode or biometry authentication that was set by the user (for example, PassCodeOrBiometrySet, BiometryNotAvailable, or PassCodeNotSet). | Core Features |
| O9 | String | CurrentTimeZone | Not applicable | USER PREFERENCE | The time zone that is currently used by the system. | Potential Label |
| P1 | String | AutoUpdatingCurrentTimeZone | Not applicable | USER PREFERENCE | The time zone that is currently used by the system. It's automatically updated to the user's current preference. | Investigative Features |
| P2 | String | CurrentLocale | Not applicable | USER PREFERENCE | The user's current locale. | Potential Label |
| P3 | String | AutoUpdatingCurrentLocale | Not applicable | USER PREFERENCE | A locale that tracks the user's current preferences. | Investigative Features |
| P4 | String Array | PreferredLanguages | Not applicable | USER PREFERENCE | A list of the user's preferred languages. | Potential Label |
| P5 | | IsMonoAudioEnabled | Not applicable | USER PREFERENCE | A value that indicates whether system audio is mixed down from stereo to mono. | Investigative Features |
| P6 | Bool | IsClosedCaptioningEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for closed captioning is enabled. | Investigative Features |
| P7 | Bool | IsInvertColorsEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for inverted colors is enabled. | Investigative Features |
| P8 | Bool | IsGuidedAccessEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the app is running under guided access mode. | Investigative Features |
| P9 | Bool | IsBoldTextEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for bold text is enabled. | Investigative Features |
| Q1 | Bool | IsGrayscaleEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for grayscale is enabled. | Investigative Features |
| Q2 | Bool | IsReduceTransparencyEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for reduced transparency is enabled. | Investigative Features |
| Q3 | Bool | IsReduceMotionEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for reduced motion is enabled. | Investigative Features |
| Q4 | Bool | IsVideoAutoplayEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for auto-play videos is enabled. | Investigative Features |
| Q5 | Bool | IsDarkerSystemColorsEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for darker colors is enabled. | Investigative Features |
| Q6 | Bool | IsSwitchControlRunning | Not applicable | USER PREFERENCE | A value that is used to determine whether switch control is running. | Investigative Features |
| Q7 | Bool | IsSpeakSelectionEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for speaking the selection is enabled. | Investigative Features |
| Q8 | Bool | IsSpeakScreenEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for speaking the screen is enabled. | Investigative Features |
| Q9 | Bool | IsShakeToUndoEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for shaking to undo is enabled. | Investigative Features |
| R1 | Bool | IsAssistiveTouchRunning | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for assistive touch is enabled. This attribute always returns false if guided access isn't enabled. | Investigative Features |
| R2 | Bool | shouldDifferentiateWithoutColor | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for differentiation without color is enabled. | Investigative Features |
| R3 | Bool | IsOnOffSwitchLabelsEnabled | Not applicable | USER PREFERENCE | A value that indicates whether the system preference for On/Off labels is enabled. | Investigative Features |
| R4 | Bool | CanSendMail | Not applicable | USER PREFERENCE | A value that indicates whether the user has set up the device to send email. | Investigative Features |
| K1 | DoubleArray | LocationData | Location Services Authorization | LOCATION | The current location data (latitude, longitude) | Core Features |
| K2 | Double | Altitude | Location Services Authorization | LOCATION | The altitude of the location, in meters. The value can be positive (above sea level) or negative (below sea level). | Core Features |
| K3 | Double | HorizontalAccuracy | Location Services Authorization | LOCATION | The horizontal accuracy of the location, in meters. | Core Features |
| K4 | Double | VerticalAccuracy | Location Services Authorization | LOCATION | The vertical accuracy of the location, in meters. | Core Features |

## iOS technical reference

1. Download the [iOS reference implementation](https://go.microsoft.com/fwlink/?linkid=2139005).
1. Unzip the downloaded file, and add all the files to your iOS app project.
1. You can initiate the reference implementation by making the following call.

    ```plaintext
    DynamicsFP.start(instanceId: \$tenantId)
    
    \$tenantId: Provided by Microsoft (GUID/UUID)
    ```

You can initiate the reference implementation on the **AppDelegate** class, so that it can start to collect device attributes on app startup. The reference implementation prompts for location permission.

You can send the collected device attributes to Fraud Protection in the following way.

```plaintext
DynamicsFP.send(pageId: \$pageId)

\$pageId(Optional): SI=SignIn, SU=SignUp, P=Purchase
```

You can call **send()** in any UIViewController either before or on the page that has the operation that you need a risk assessment for. For sign-in/sign-up scenarios, you can call **send()** immediately after **start()** in the **AppDelegate** class.

A session ID is required when you call the risk assessment APIs. To get the session ID when you need it, call `**var** sessionId = DynamicsFP.getSessionId()`.

### iOS runtime permissions

- The reference implementation uses CLLocationManager and checks for **CLAuthorizationStatus.authorizedAlways** or **CLAuthorizationStatus.authorizedWhenInUse** before it requests location data. The app should obtain **CLLocationManager.requestWhenInUseAuthorization** or **CLLocationManager.requestAlwaysAuthorization** permission from the user.
- The reference implementation uses AppTrackingTransparency and checks for **ATTrackingManager.AuthorizationStatus.authorized** before it collects **AdvertisingId** values. The app should obtain **ATTrackingManager.requestTrackingAuthorization** permission from the user.

## iOS additional references

[iOS Apple Developer](https://developer.apple.com/ios/)

[iOS Apple Development](https://developer.apple.com/develop/)

[Xcode](https://developer.apple.com/xcode/)

## Additional resources

[Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection)

[Contact us](mailto:DFPHelp@microsoft.com)
