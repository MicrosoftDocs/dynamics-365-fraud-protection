---
author: josaw1
description: This topic provides the information needed for Dynamics 365 Fraud Protection mobile device implementation for device fingerprinting.
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

Microsoft Dynamics 365 Fraud Protection provides device fingerprinting that is based on artificial intelligence (AI), runs on Microsoft Azure, and is cloud-scalable, reliable, and has enterprise-grade security. Fraud Protection's device fingerprinting feature enables the identification of devices (for example, a computer, Xbox, tablet, etc.) across multiple sessions or interactions, and that engage with your business and other businesses in the Fraud Protection fraud network. Additionally, the device fingerprinting functionality allows Fraud Protection to link seemingly unrelated events to each other in the fraud network to identify patterns of fraud.

When you implement Fraud Protection device fingerprinting by integrating the reference implementation provided in your app, you agree to [Microsoft APIs Terms of Use](/legal/microsoft-apis/terms-of-use), and you direct Microsoft to process the following types of data from the devices interacting with the Fraud Protection services (collectively, "Device Fingerprinting Data"):

-  Device attributes such as device ID, screen information, processor class,
    etc.

-  Operating system (OS) attributes, such as OS information, OS version, OEM
    details, etc.

-  Browser-related attributes, if applicable, such as browser language, installed
    default apps, etc.

It is your responsibility to:

-  Receive consent from your users to collect and allow Microsoft to process
    the device fingerprinting data.

-  Inform your customers of your data collection and processing practices, for
    example by disclosing the data you collect and how it is used.

-  Disclose your use of third parties working on your behalf to process the
    data you collect, including Fraud Protection service providers.

-  Comply with all laws and regulations applicable to the use of Fraud
    Protection, including data protection laws.

To integrate device fingerprinting for Fraud Protection, you need to complete the following tasks:

1.  Set up Microsoft Azure DNS by following the steps under "Set-up Azure DNS" in [Set up device fingerprinting](device-fingerprinting.md).

1.  Integrate device fingerprinting with your mobile application using the reference implementation provided.


## Attribute category introduction reference

This section includes a list of the device fingerprinting data that we may process and the rationale for processing the data. Each of the data attributes described in the list below is optional. You can configure the number of attributes that best reflect the needs of your organization in relation to the privacy rights of device users in your corresponding jurisdiction.

Attributes are categorized as follows. Each attribute is identified with one of the categories below.

- **Core Features:** This group of attributes are core to Fraud Protection's ability to predict patterns of fraud. Based on prior experience, Microsoft has reason to believe that these attributes will be highly accretive to Fraud Protection's model performance and ability to discern distinctive patterns of fraud. If these core features are not supplied, device fingerprinting will be inaccurate.

- **Investigative Features:** This group of attributes have the potential to add or enhance Fraud Protection's ability to predict patterns of fraud more accurately. Statistical analysis of collected data is the only definitive way to determine whether these attributes are strong predictors of patterns of fraud. If the predictive capability of these attributes do not meet microsoft's expectations, then we will no longer utilize these attributes. While these group of attributes would allow Microsoft to determine whether they will be strong predictors of patterns of fraud, they are optional and are not required.

- **Potential Label:** This group of attributes are used for model supervision and labeling purposes. Each of these attributes on their own has a probability of not providing ground truth. However, combining the attributes increases the likelihood that the label used in training the Fraud Protection's model becomes ground truth and will therefore result in higher model performance. Although Fraud Protection can function without these attributes, the machine learning model will be unable to improve without them.

## Android attributes for mobile reference implementation

| Code | Name  | Permission if any  | Group  | Description of the Attribute   | Attribute Category   | Baseline Stack Level   |
|------|---------|--------------------------|--------------|----------------------------------|------------------------|--------------------------|
| A1   | DeviceId  | N/A   | DEVICE SPECIFICATION  | Generated on the device on first use (DeviceID)   | Core Features  | 31   |
| A2   | OS architecture   | N/A   | DEVICE SPECIFICATION  | OS Architecture (for example, armv7l)  | Potential Label  | 31   |
| A3   | OS name   | N/A   | DEVICE SPECIFICATION  | OS Name (for example, Linux)   | Potential Label  | 31   |
| A4   | AppVersionName  | N/A   | DEVICE SPECIFICATION  | The version Name of this app   | Potential Label  | 31   |
| A5   | AppVersionCode  | N/A   | DEVICE SPECIFICATION  | The version number of this app   | Potential Label  | 31   |
| A6   | Application label   | N/A   | DEVICE SPECIFICATION  | The label associated with the application  | Potential Label  | 31   |
| A7   | SystemUpTime  | N/A   | DEVICE SPECIFICATION  | Time since reboot  | Investigative Features | 31   |
| A8   | Advertising_ID  | N/A   | DEVICE SPECIFICATION  | The Advertising ID is an identifier that can be reset by the user and is appropriate for ads use cases. https://developer.android.com/training/articles/user-data-ids\#advertising-ids  | Core Features  | 31   |
| A9   | IsDeviceRooted  | N/A   | DEVICE SPECIFICATION  | Rooting is way to unlock the operating system so you can install unapproved apps, delete unwanted bloatware, update the OS, replace the firmware, overclock (or underclock) the processor, customize anything, etc.   | Potential Label  | 31   |
| B1   | IsDeviceEmulator  | N/A   | DEVICE SPECIFICATION  | The Android Emulator simulates Android devices on your computer so you can test your app on a variety of devices and Android API levels without needing to have each physical device.   | Potential Label  | 31   |
| B6   | SIM state   | N/A   | DEVICE SPECIFICATION  | State of default SIM (for example, UNKNOWN, ABSENT, SIM locked requires PIN to unlock, SIM locked requires PUK to unlock, etc.)   | Investigative Features | 31   |
| B7   | Phone type  | N/A   | DEVICE SPECIFICATION  | This indicates the type of radio used to transmit voice calls (GSM, CDMA, SIP, or None).   | Potential Label  | 31   |
| B8   | NetworkOperator   | N/A   | DEVICE SPECIFICATION  | Carrier that physically delivers the data. Changes if device moves.  | Potential Label  | 31   |
| B9   | NetworkCountryISO   | N/A   | DEVICE SPECIFICATION  | Only provided when user is registered to a network. Result may be unreliable on CDMA networks (use getPhoneType() to determine if on a CDMA network).  | Core Features  | 31   |
| C1   | Sim Operator Name   | N/A   | DEVICE SPECIFICATION  | Provider of your data.   | Core Features  | 31   |
| C3   | Sim Country ISO   | N/A   | DEVICE SPECIFICATION  | Country code of SIM provider.  | Investigative Features | 31   |
| C5   | Cellular DataState  | N/A   | DEVICE SPECIFICATION  | Current cellular data connection state (DISCONNECTED, CONNECTED, or SUSPENDED).   | Investigative Features | 31   |
| C6   | Sim configured count  | N/A   | DEVICE SPECIFICATION  | The number of logical modems currently configured to be activated. Returns "0" if voice, SMS, data is not supported. Returns "1" for single standby mode (single SIM functionality). Returns "2" for dual standby mode (dual SIM functionality). Returns "3" for tri-standby mode (tri SIM functionality).  | Investigative Features | 31   |
| D8   | Screen size in pixels   | N/A   | DEVICE SPECIFICATION  | The absolute width and height of the available display size in pixels.   | Investigative Features | 31   |
| D9   | Screen density  | N/A   | DEVICE SPECIFICATION  | The logical density of the display.    | Investigative Features | 31   |
| E1   | Screen xdpi   | N/A   | DEVICE SPECIFICATION  | The exact physical pixels per inch of the screen in the X dimension.   | Investigative Features | 31   |
| E2   | Screen ydpi   | N/A   | DEVICE SPECIFICATION  | The exact physical pixels per inch of the screen in the Y dimension.   | Investigative Features | 31   |
| E3   | Screen dpi  | N/A   | DEVICE SPECIFICATION  | The screen density expressed as dots-per-inch.   | Investigative Features | 31   |
| E4   | Category of screen size   | N/A   | DEVICE SPECIFICATION  | Small, normal, large, x-large, or undefined.   | Investigative Features | 31   |
| E5   | Display Id  | N/A   | DEVICE SPECIFICATION  | Each logical display has a unique ID.  | Core Features  | Deprecated (may be available from lower version of the stack). |
| E6   | RefreshRate   | N/A   | DEVICE SPECIFICATION  | Gets the refresh rate of the display in frames per second.  | Investigative Features | 31   |
| E7   | Rotation  | N/A   | DEVICE SPECIFICATION  | Orientation of the display (ROTATION_0, ROTATION_90, ROTATION_180 or ROTATION_270).   | Investigative Features | 31   |
| E8   | Battery level   | N/A   | DEVICE SPECIFICATION  | The current battery level.  | Potential Label  | 31   |
| E9   | Is battery charging   | N/A   | DEVICE SPECIFICATION  |  | Potential Label  | 31   |
| F1   | Charge type   | N/A   | DEVICE SPECIFICATION  | Whether the device is plugged in to a power source. "0" means it is on battery. Other values represent different types of power sources.  | Potential Label  | 31   |
| F2   | Temperature   | N/A   | DEVICE SPECIFICATION  | The current battery temperature.  | Potential Label  | 31   |
| F3   | Technology  | N/A   | DEVICE SPECIFICATION  | The technology of the current battery.   | Potential Label  | 31   |
| F4   | Voltage   | N/A   | DEVICE SPECIFICATION  | The current battery voltage level.  | Potential Label  | 31   |
| H5   | Board   | N/A   | DEVICE SPECIFICATION  | The name of the underlying board (for example, "goldfish").    | Potential Label  | 31   |
| H6   | Bootloader  | N/A   | DEVICE SPECIFICATION  | The system bootloader version number.  | Investigative Features | 31   |
| H7   | Brand   | N/A   | DEVICE SPECIFICATION  | The consumer-visible brand with which the product/hardware will be associated, if any.   | Potential Label  | 31   |
| H8   | Device  | N/A   | DEVICE SPECIFICATION  | The name of the industrial design. Device name provided by manufacturer (for example, Bravo, Passion, GT-I9000).   | Potential Label  | 31   |
| H9   | Display   | N/A   | DEVICE SPECIFICATION  | A build ID string to be displayed to the user.   | Investigative Features | 31   |
| I1   | Hardware  | N/A   | DEVICE SPECIFICATION  | The name of the hardware (from the kernel command line or /proc).  | Potential Label  | 31   |
| I2   | Host  | N/A   | DEVICE SPECIFICATION  | Name of the person building the ROM and kernel.  | Potential Label  | 31   |
| I3   | ID  | N/A   | DEVICE SPECIFICATION  | Either a build change list number, or a label (for example, "M4-rc20").  | Core Features  | 31   |
| I4   | Manufacturer  | N/A   | DEVICE SPECIFICATION  | The manufacturer of the product/hardware.  | Potential Label  | 31   |
| I5   | Model   | N/A   | DEVICE SPECIFICATION  | The end-user-visible name for the end product.   | Potential Label  | 31   |
| I6   | Product   | N/A   | DEVICE SPECIFICATION  | The name of the overall product.   | Potential Label  | 31   |
| I7   | Radio version   | N/A   | DEVICE SPECIFICATION  | The radio firmware version.   | Investigative Features | 31   |
| I9   | Type  | N/A   | DEVICE SPECIFICATION  | Type of build (for example, "user" or "eng").  | Potential Label  | 31   |
| J1   | Tags  | N/A   | DEVICE SPECIFICATION  | Comma-separated tags describing the build (for example, "unsigned" or "debug").  | Investigative Features | 31   |
| J2   | Supported ABIS  | N/A   | DEVICE SPECIFICATION  | An ordered list of ABIs supported by the device (for example, armeabi-v7a).   | Potential Label  | 31   |
| J3   | Time  | N/A   | DEVICE SPECIFICATION  | The time and date when the ROM and kernel were built together.  | Potential Label  | 31   |
| J4   | SDK version   | N/A   | DEVICE SPECIFICATION  | The SDK version of the software currently running on the hardware device.   | Potential Label  | 31   |
| J5   | Code name   | N/A   | DEVICE SPECIFICATION  | The current development code name, or the string "REL" if it is a release build.  | Potential Label  | 31   |
| J6   | Total memory  | N/A   | DEVICE SPECIFICATION  | Total RAM memory for the device.  | Investigative Features | 31   |
| J7   | Available memory  | N/A   | DEVICE SPECIFICATION  | Currently available RAM memory for the device.  | Investigative Features | 31   |
| J8   | Low memory  | N/A   | DEVICE SPECIFICATION  | The OS considers itself to currently be in a low memory situation.   | Investigative Features | 31   |
| J9   | CPU usage   | N/A   | DEVICE SPECIFICATION  | The current CPU usage by device (for example, 0.39).   | Investigative Features | Deprecated (may be available from lower version of the stack) |
| K1   | CPU info hash   | N/A   | DEVICE SPECIFICATION  | CPU info hashed by MD5.   | Core Features  | 31   |
| K2   | CPU number of cores   | N/A   | DEVICE SPECIFICATION  | The number of processors available to the Java virtual machine.   | Potential Label  | 31   |
| K3   | Max CPU frequency   | N/A   | DEVICE SPECIFICATION  | Max frequency CPU can run on the device.   | Potential Label  | 31   |
| K4   | Min CPU frequency   | N/A   | DEVICE SPECIFICATION  | Min frequency CPU can run on the device.   | Potential Label  | 31   |
| K5   | Total internal storage  | N/A   | DEVICE SPECIFICATION  | Total internal storage for device in bytes.  | Potential Label  | 31   |
| K6   | Available internal storage  | N/A   | DEVICE SPECIFICATION  | Available internal storage for device in bytes.   | Potential Label  | 31   |
| K7   | Is external memory mounted  | N/A   | DEVICE SPECIFICATION  | Whether the external memory card is mounted (SD Card).  | Potential Label  | 31   |
| K8   | Total external storage  | N/A   | DEVICE SPECIFICATION  | Total external storage for device in bytes.   | Potential Label  | 31   |
| K9   | Available external storage  | N/A   | DEVICE SPECIFICATION  | Available external storage for device in bytes.   | Potential Label  | 31   |
| G4   | Accelerometer name  | N/A   | ACCELEROMETER   | The name string of Accelerometer sensor (for example, MPU6515 Accelerometer).   | Investigative Features | 31   |
| G5   | Accelerometer vendor name   | N/A   | ACCELEROMETER   | The vendor of the Accelerometer sensor (for example, InvenSense).   | Investigative Features | 31   |
| G6   | Accelerometer power   | N/A   | ACCELEROMETER   | The power in mA used by the Accelerometer sensor while in use.  | Potential Label  | 31   |
| G7   | Accelerometer version   | N/A   | ACCELEROMETER   | The version of the Accelerometer sensor's module.   | Potential Label  | 31   |
| G8   | Accelerometer data  | N/A   | ACCELEROMETER   | Accelerometer sensor reading.   | Investigative Features | 31   |
| G9   | Gyroscope name  | N/A   | GYROSCOPE   | The name string of the Gyroscope sensor (for example, MPU6515 Gyroscope).   | Potential Label  | 31   |
| H1   | Gyroscope vendor name   | N/A   | GYROSCOPE   | The vendor of the Gyroscope sensor (for example, InvenSense).   | Potential Label  | 31   |
| H2   | Gyroscope power   | N/A   | GYROSCOPE   | The power in mA used by the Gyroscope sensor while in use.   | Investigative Features | 31   |
| H3   | Gyroscope version   | N/A   | GYROSCOPE   | The version of the Gyroscope sensor's module.   | Potential Label  | 31   |
| H4   | Gyroscope data  | N/A   | GYROSCOPE   | The Gyroscope sensor reading.   | Investigative Features | 31   |
| L2   | Is auto rotate accelerometer enabled?   | N/A   | USER PREFERENCE   | Controls whether the accelerometer will be used to change the screen orientation.  | Investigative Features | 31   |
| L3   | Is ADB enabled?   | N/A   | USER PREFERENCE   | Whether Android Debug Bridge (ADB) is enabled. ADB is a versatile command-line tool that lets you communicate with a device.   | Investigative Features | 31   |
| L4   | Is airplane mode on?  | N/A   | USER PREFERENCE   | Whether airplane mode is on.   | Investigative Features | 31   |
| L5   | Is auto time enabled?   | N/A   | USER PREFERENCE   | If the user prefers the date, time, and time zone to be automatically fetched from the network.  | Investigative Features | 31   |
| L6   | Is auto time zone enabled?  | N/A   | USER PREFERENCE   | If the user prefers the time zone to be automatically fetched from the network.   | Investigative Features | 31   |
| L7   | Is Bluetooth enabled?   | N/A   | USER PREFERENCE   | Whether Bluetooth is enabled or disabled.  | Investigative Features | 31   |
| L8   | Date format   | N/A   | USER PREFERENCE   | Date format used by user (for example, mm/dd/yyyy or dd/mm/yyyy).  | Potential Label  | Deprecated, may be available from lower version of the stack |
| L9   | Is device provisioned?  | N/A   | USER PREFERENCE   | On a multiuser device with a separate system user, the screen may be locked as soon as this is set to true. Further activities can not be launched on the system user unless they are marked to show over the keyguard.  | Investigative Features | 31   |
| M1   | Is development setting enabled?   | N/A   | USER PREFERENCE   | Whether the user has enabled development settings.  | Investigative Features | 31   |
| M2   | Is dial pad enabled?  | N/A   | USER PREFERENCE   | Whether the audible DTMF tones are played by the dialer when dialing.   | Investigative Features | 31   |
| M3   | End call behavior   | N/A   | USER PREFERENCE   | Determines what happens when the user presses the end call button if they are not on a call.   | Potential Label  | 31   |
| M4   | Font scale  | N/A   | USER PREFERENCE   | Scaling factor for fonts.   | Investigative Features | 31   |
| M5   | Is haptic feedback enabled?   | N/A   | USER PREFERENCE   | Whether the haptic feedback (for example, long presses) are enabled.  | Investigative Features | 31   |
| M6   | HTTP proxy  | N/A   | USER PREFERENCE   | Host name and port for global http proxy.   | Investigative Features | Deprecated (may be available from lower version of the stack). |
| M8   | Is lock pattern enabled?  | N/A   | USER PREFERENCE   | Whether autolock is enabled (API \<= 22).   | Investigative Features | Deprecated, may be available from lower version of the stack |
| M9   | Is lock pattern visible?  | N/A   | USER PREFERENCE   | Whether lock pattern is visible as user enters (API \<= 22).   | Investigative Features | Deprecated, may be available from lower version of the stack |
| N1   | Ringer mode   | N/A   | USER PREFERENCE   | Ringer mode (for example, silent, vibrate and normal).  | Investigative Features | 31   |
| N2   | Screen brightness   | N/A   | USER PREFERENCE   | The screen backlight brightness between 0 and 255.  | Investigative Features | 31   |
| N3   | Is auto screen brightness enabled?  | N/A   | USER PREFERENCE   | Controls whether to enable automatic brightness mode.  | Investigative Features | 31   |
| N4   | Screen off timeout  | N/A   | USER PREFERENCE   | The amount of time in milliseconds before the device goes to sleep or begins to dream after a period of inactivity.  | Investigative Features | 31   |
| N5   | Settings class name   | N/A   | USER PREFERENCE   | Settings class name to launch when **Settings** is selected from **All Applications**.  | Potential Label  | Deprecated, may be available from lower version of the stack |
| N6   | Is sound effects enabled?   | N/A   | USER PREFERENCE   | Whether the sounds effects (for example, key clicks or lid open) are enabled.  | Investigative Features | 31   |
| N7   | Is stay on plugged in enabled?  | N/A   | USER PREFERENCE   | Whether the user keeps the device on while the device is plugged in (during charge).   | Investigative Features | 31   |
| N8   | Is auto caps enabled?   | N/A   | USER PREFERENCE   | Setting to enable auto-caps in text editors is enabled.   | Investigative Features | 31   |
| N9   | Is auto punctuate?  | N/A   | USER PREFERENCE   | Setting to enable auto-punctuate in text editors is enabled.  | Investigative Features | 31   |
| O1   | Is auto replace enabled?  | N/A   | USER PREFERENCE   | Setting to enable auto-replace (auto text) in text editors is enabled.   | Investigative Features | 31   |
| O2   | Is show password enabled?   | N/A   | USER PREFERENCE   | Setting to show password characters in text editors is enabled.  | Investigative Features | 31   |
| O3   | 24 hour clock format  | N/A   | USER PREFERENCE   | Display times as 12 or 24 hours.  | Investigative Features | 31   |
| O4   | Is vibrate on?  | N/A   | USER PREFERENCE   | Whether vibrate is on for different events.   | Investigative Features | 31   |
| O5   | Default text-to-speech engine   | N/A   | USER PREFERENCE   | Default text-to-speech engine.  | Potential Label  | 31   |
| O6   | Default text-to-speech engine speech rate | N/A   | USER PREFERENCE   | Default text-to-speech engine speech rate (for example, 100 = 1x).   | Investigative Features | 31   |
| O7   | Default text-to-speech engine pitch   | N/A   | USER PREFERENCE   | Default text-to-speech engine speech pitch (for example, 100 = 1x).   | Investigative Features | 31   |
| O9   | Actual default ringtone   | N/A   | USER PREFERENCE   | Type that refers to sounds that are used for the phone ringer.  | Investigative Features | 31   |
| P1   | Actual default notification ringtone  | N/A   | USER PREFERENCE   | Type that refers to sounds that are used for notifications.   | Investigative Features | 31   |
| P2   | Actual default alarm ringtone   | N/A   | USER PREFERENCE   | Type that refers to sounds that are used for the alarm.  | Investigative Features | 31   |
| P3   | Launcher screen app package name  | N/A   | USER PREFERENCE   | This is the home app, which is the first app that is displayed when the android device boots.  | Investigative Features | 31   |
| P4   | Activity list on launcher screen  | N/A   | USER PREFERENCE   | List of all home apps that can used as the starting app when the device boots.  | Investigative Features | 31   |
| P5   | Default browser package   | N/A   | USER PREFERENCE   | Default browser app used by user (for example, Edge).   | Investigative Features | Deprecated (may be available from lower version of the stack) |
| P6   | List of browser packages  | N/A   | USER PREFERENCE   | List of all browser apps installed by the user (for example, Edge, Chrome).   | Investigative Features | Deprecated (may be available from lower version of the stack). |
| P7   | SMS viewer package  | N/A   | USER PREFERENCE   | Default SMS viewer app used by user.  | Investigative Features | Deprecated (may be available from lower version of the stack). |
| P8   | List of SMS viewer packages   | N/A   | USER PREFERENCE   | List of all SMS viewer apps installed by user.  | Investigative Features | Deprecated (may be available from lower version of the stack). |
| P9   | Phone call package  | N/A   | USER PREFERENCE   | Default phone call app used by user.  | Investigative Features | 31   |
| Q1   | List phone call packages  | N/A   | USER PREFERENCE   | List of all phone call apps installed by the user.  | Investigative Features | 31   |
| Q2   | Default input package   | N/A   | USER PREFERENCE   | Default input method app used by user (for example, keyboards).   | Potential Label  | 31   |
| Q3   | Input methods package list  | N/A   | USER PREFERENCE   | List of all input method apps installed by user.  | Investigative Features | 31   |
| Q4   | Default input language  | N/A   | USER PREFERENCE   | Default input language used by user (for example, en).   | Investigative Features | 31   |
| Q5   | Time zone offset  | N/A   | USER PREFERENCE   | The amount of time in milliseconds to add to UTC to get standard time in the time zone. Because this value is not affected by daylight savings time, it is called "raw offset".  | Investigative Features | 31   |
| Q6   | Default font size in pixels   | N/A   | USER PREFERENCE   | The default font size (in pixels) in TextView.  | Investigative Features | 31   |
| Q7   | Is wall paper present   | N/A   | USER PREFERENCE   | Whether the current wallpaper is a live wallpaper component.   | Investigative Features | 31   |
| Q8   | Wallpaper pkg name   | N/A   | USER PREFERENCE   | The .apk package that implements the wallpaper.  | Investigative Features | 31   |
| Q9   | IsDeviceSecure  | N/A   | USER PREFERENCE   | Whether the device is secured with a PIN, pattern, or password (API\>22).  | Potential Label  | 31   |
| R1   | Installer package name  | N/A   | USER PREFERENCE   | The package name of the app that installed a package.   | Investigative Features | 31   |
| R2   | Supports multiple users   | N/A   | DEVICE SPECIFICATION  | Whether the device supports multiple users with their own login and customizable space.  | Potential Label  | 31   |
| R3   | User serial number  | N/A   | DEVICE SPECIFICATION  | The serial number for a user. This is a device-unique number assigned to that user. If the user is deleted and a new user is created, the new user will not be given the same serial number.  | Potential Label  | 31   |
| R4   | App package name   | N/A   | DEVICE SPECIFICATION  | The name of app's package.   | Potential Label  | 31   |
| R5   | App directory path  | N/A   | DEVICE SPECIFICATION  | The absolute path to the directory on the filesystem where files created with openFileOutput are stored.   | Potential Label  | 31   |
| B2   | ANDROID_ID  | N/A   | DEVICE SPECIFICATION  | On Android 8.0 (API level 26) and higher versions of the platform, a 64-bit number (expressed as a hexadecimal string), unique to each combination of app-signing key, user, and device. Values of ANDROID_IDare scoped by signing key and user. The value may change if a factory reset is performed on the device or if an APK signing key changes. | Core Features  | 31   |
| B3   | GSF_ID  | com.google.android.providers.gsf.permission.READ_GSERVICES   | DEVICE SPECIFICATION  | The Google Services Framework Identifier (GSF ID) is a unique 16-character hexadecimal number that the device automatically requests from Google as soon as the user logs in to their Google account for the first time. For a specific device, the GSF ID will change only after a factory reset.  | Core Features  | 31   |
| B4   | Unique number   | android.permission.READ_PHONE_STATE (RunTime)  | DEVICE SPECIFICATION  | IMEI, MEID, ESN, or IMSI.  | Core Features  | Deprecated, may be available from lower version of the stack |
| B5   | Subscriber ID   | android.permission.READ_PHONE_STATE (RunTime)  | DEVICE SPECIFICATION  | The unique subscriber ID, (for example, the IMSI for a GSM phone). Return null if it is unavailable.   | Core Features  | Deprecated (may be available from lower version of the stack). |
| C2   | SIM serial number   | android.permission.READ_PHONE_STATE (RunTime)  | DEVICE SPECIFICATION  | SIM serial number, sometimes called the ICC-ID (Integrated Circuit Card ID), is for international identification.   | Core Features  | Deprecated (may be available from lower version of the stack). |
| I8   | Serial  | android.permission.READ_PHONE_STATE (RunTime)  | DEVICE SPECIFICATION  | The hardware serial number.   | Core Features  | Deprecated, may be available from lower version of the stack |
| C4   | SimNetworkType  | android.permission.READ_PHONE_STATE (RunTime)  | DEVICE SPECIFICATION  | The current data connection (GPRS, EDGE, CDMA, 1xRTT, IDEN, UMTS, EVDO_0, EDO_A, HSDPA, etc.)  | Investigative Features | 31   |
| C7   | DataNetworkType   | android.permission.ACCESS_NETWOR,K_STATE  | DEVICE SPECIFICATION  | Human-readable name to describe the type of the network (for example ,"WIFI" or "MOBILE").  | Investigative Features | 31   |
| C8   | Is the device connected to the network?   | android.permission.ACCESS_NETWORK_STATE  | DEVICE SPECIFICATION  | Whether network connectivity exists and it is possible to establish connections and pass data.   | Potential Label  | 31   |
| C9   | Is the device roaming?  | android.permission.ACCESS_NETWORK_STATE  | DEVICE SPECIFICATION  | Whether the device is currently roaming on the network. When true, it suggests that use of data on the network may incur extra costs.   | Potential Label  | 31   |
| D1   | Is WIFI enabled?  | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | Whether Wi-Fi is enabled or disabled.  | Investigative Features | 31   |
| D2   | MAC address   | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | Wi-Fi network adopter MAC. The MAC address of the WLAN interface.   | Core Features  | Deprecated (may be available from lower version of the stack). |
| D3   | Line speed  | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | Wi-Fi line speed.   | Investigative Features | 31   |
| D4   | Signal strength   | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | Wi-Fi signal strength.  | Investigative Features | 31   |
| D5   | WifiSSID  | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | The service set identifier (SSID) of the current 802.11 network.  | Core Features  | Deprecated (may be available from lower version of the stack). |
| D6   | IPAddressV4 (IPV4)  | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  |  | Core Features  | 31   |
| D7   | Configured networks SSIDs   | android.permission.ACCESS_WIFI_STATE   | DEVICE SPECIFICATION  | A list of all the network-configured SSIDs for the current foreground user.   | Core Features  | Deprecated (may be available from lower version of the stack). |
| F5   | Bluetooth address   | android.permission.BLUETOOTH   | DEVICE SPECIFICATION  | The hardware address of the local Bluetooth adapter. (for example, 00:11:22:AA:BB:CC).   | Core Features  | Deprecated (may be available from lower version of the stack). |
| F6   | Bluetooth adapter name  | android.permission.BLUETOOTHandroid.permission.BLUETOOTH_CONNECT (RunTime) | DEVICE SPECIFICATION  | The friendly Bluetooth name of the local Bluetooth adapter. This name is visible to remote Bluetooth devices.  | Investigative Features | 31   |
| F7   | BlueToothState  | android.permission.BLUETOOTH   | DEVICE SPECIFICATION  | The current state of the local Bluetooth adapter.  | Potential Label  | 31   |
| F9   | Is GPS enabled?   | android.permission.ACCESS_COARSE_LOCATION (RunTime)  | LOCATION  | Whether GPS is enabled or disabled   | Potential Label  | 31   |
| G1   | Device GPS location   | android.permission.ACCESS_COARSE_LOCATION (RunTime)  | LOCATION  | Current location data (latitude, longitude).  | Core Features  | 31   |
| G2   | Is network provider enabled?  | android.permission.ACCESS_COARSE_LOCATION (RunTime)  | LOCATION  | Whether the network is enabled or disabled.   | Core Features  | 31   |
| G3   | Altitude  | android.permission.ACCESS_COARSE_LOCATION (RunTime)  | LOCATION  | The altitude of the location in meters. Can be positive (above sea level) or negative (below sea level).   | Core Features  | 31   |
| M7   | Is install non-market apps enabled?   | android.permission.REQUEST_INSTALL_PACKAGES  | USER PREFERENCE   | Whether non-market applications (apps not from Google Play) can be installed for the user.  | Investigative Features | Deprecated (may be available from lower version of the stack). |



## Android technical reference


1.  Download the [Android reference implementation](https://go.microsoft.com/fwlink/?linkid=2138490).

1.  Import the library module to your project. The library source becomes part of your project.

    1.  Select **File \> New \> Import Module**.

    1.  Enter the location of the library module directory, then select **Finish**.

The library module is copied to your project. You can edit the library code.

1.  Make sure the library is listed at the top of your settings.gradle file, as shown here for a library named " :DynamicsFP". `include ':Demo', ':DynamicsFP'`

1.  Open the app module's build.gradle file and add a new line to the dependencies block as shown in the following snippet: `dependencies { implementation project(":DynamicsFP") } `

1.  Select **Sync Project with Gradle Files**.

You can initiate reference implementation by calling the following process: 

```plaintext
import com.microsoft.dynamicsfp.androidsdk.DynamicsFP;

*DynamicsFP.start(getApplicationContext(), \$tenantId);*

\$tenantId :Provided by Microsoft(GUID/UUID)
```

You can initiate reference implementation code on base application class so it can start collecting device attributes. Reference implementation does not prompt the user for runtime permission.

You can send collected device attributes to Fraud Protection by calling Fraud Protection in the following way:


```plaintext
import com.microsoft.dynamicsfp.androidsdk.DynamicsFP;

*DynamicsFP.send(\$pageId);*

\$pageId(Optional): SI=SignIn, SU=SignUp, P= Purchase
```

You can call send() in any fragment/activity before or on the page that has the operation you need a risk assessment for. For a sign in/sign up scenario, you can call
send() immediate after start() in base application class.

Once you need sessionId, get it by calling:`*String sessionId = DynamicsFP.getSessionId();*` . SessionId is required when calling the risk assessment APIs.

### Android runtime permissions

Reference implementations rely on the following runtime permissions to collect various device data. Reference implementation does not request any runtime
permissions from the user, the app should obtain the runtime permissions from the user.

-   android.permission.ACCESS_COARSE_LOCATION

-   android.permission.READ_PHONE_STATE

-   android.permission.BLUETOOTH_CONNECT



## Android additional references


[Android API Reference](https://developer.android.com/reference)

[About permissions](https://developer.android.com/training/permissions/requesting)

[App manifest file](https://developer.android.com/guide/topics/manifest/manifest-intro)

[Add dependency](https://developer.android.com/studio/projects/android-library#AddDependency)

[Determine sensitive data access needs](https://developer.android.com/games/develop/permissions?hl=en)

[Android Legal Notice](https://developer.android.com/legal)


## iOS attributes for mobile reference implementation


| Code | Type   | Name   | Permission if any   | Group  | Description of the Attribute  | Attribute Category   |
|------|--------------|--------------|-----------------------|----------------------|-------------------------------------|------------------------|
| A1   | String   | DeviceId     |  N/A  |  DEVICE SPECIFICATION | Generated on the device on first use.   | Core Features  |
| A2   | String   | BundleIdentifier   |  N/A  |  DEVICE SPECIFICATION | Bundle identifier uniquely identifies an application in Apple's ecosystem.                             | Investigative Features |
| A3   | String   | BundleName   |  N/A  |  DEVICE SPECIFICATION | Identifies the short name of the bundle.        | Investigative Features |
| A4   | String   | AppVersionName   |  N/A  |  DEVICE SPECIFICATION | App version (for example, 4.3.1).         | Investigative Features |
| A5   | String   | AppVersionCode   |  N/A  |  DEVICE SPECIFICATION | App build code (for example, 230, A1160).          |  N/A |
| A7   | Long   | SystemUpTime   |  N/A  |  DEVICE SPECIFICATION | The amount of time the system has been awake since the last time it was restarted.      | Potential Label  |
| A8   | String   | Advertising_ID   |  N/A  |  DEVICE SPECIFICATION | An alphanumeric string unique to each device, used only for serving advertisements. In iOS 10.0 and later, the value of advertisingIdentifier is all zeroes when the user has limited ad tracking. Unlike the [identifierForVendor](https://developer.apple.com/documentation/uikit/uidevice/1620059-identifierforvendor) property of the [UIDevice](https://developer.apple.com/documentation/uikit/uidevice), the same value is returned to all vendors. This identifier may change (for example, if the user erases the device). For this reason, you should not cache it.       | Core Features  |
| A9   | Bool   | IsDeviceRooted   |  N/A  |  DEVICE SPECIFICATION | IsDeviceJailBroken: Jailbreaking changes the operating system running on an iPhone or iPod touch to give you more control.     | Potential Label  |
| B1   | Bool   | IsDeviceEmulator   |  N/A  |  DEVICE SPECIFICATION | IsDeviceSimulator: The iOS simulator allows the user to use features and run applications on the virtual iPhone on their MacBook as though it was the actual iPhone device                               | Potential Label  |
| B8   | String   | NetworkOperator  |  N/A  |  DEVICE SPECIFICATION | CarrierName: The name of the subscriber's cellular service provider (for example, AT&T). | Potential Label  |
| B9   | String   | NetworkCountryISO  |  N/A  |  DEVICE SPECIFICATION | ISOCountryCode: Country code for the subscriber's cellular service provider. Represented as an ISO 3166-1 country code string    | Potential Label  |
| C1   | String   | MobileCountryCode  |  N/A  |  DEVICE SPECIFICATION | The mobile country code for the subscriber's cellular service provider.       | Potential Label  |
| C2   | String   | MobileNetworkCode  |  N/A  |  DEVICE SPECIFICATION | The mobile network code for the subscriber's service provider.        | Potential Label  |
| C3   | Bool   | AllowsVOIP   |  N/A  |  DEVICE SPECIFICATION | Indicates whether the carrier allows VOIP calls to be made on its network.        | Investigative Features |
| C4   | String   | SimNetworkType   |  N/A  |  DEVICE SPECIFICATION | RadioAccessTechnology: The current radio access technology for each service of the device is registered with. May be nil if the device is not registered on any network.                              | Potential Label  |
| C7   | String   | DataNetworkType  |  N/A  |  DEVICE SPECIFICATION | Network reachable over the WIFI or mobile.        | Potential Label  |
| C8   | Bool   | IsConnected  |  N/A  |  DEVICE SPECIFICATION | Whether the network is currently reachable.        | Investigative Features |
| D6   | String   | IPAddressV4 (IPV4)   |  N/A  |  DEVICE SPECIFICATION | IP address V4.          | Core Features  |
| D7   | String   | IPAddressV6 (IPV6)   |  N/A  |  DEVICE SPECIFICATION | IP Address V6.          | Core Features  |
| D8   | Int  | Screen size in pixels  |  N/A  |  DEVICE SPECIFICATION | The absolute width and height of the available display size in pixels.       | Investigative Features |
| D9   | Int  | Screen size in points  |  N/A  |  DEVICE SPECIFICATION | The absolute width and height of the available display size in points.       | Investigative Features |
| E1   | Float  | Scale    |  N/A  |  DEVICE SPECIFICATION | The natural scale factor associated with the screen.         | Investigative Features |
| E2   | Float  | NativeScale  |  N/A  |  DEVICE SPECIFICATION | The native scale factor for the physical screen.         | Investigative Features |
| E3   | Bool   | IsCaptured   |  N/A  |  DEVICE SPECIFICATION | Whether the contents of the screen are being cloned to another destination (iOS \>= 11).       | Investigative Features |
| E4   | Bool   | ScreenWantsSoftwareDimming   |  N/A  |  DEVICE SPECIFICATION | Whether the screen may be dimmed lower than the hardware is normally capable of by emulating it in software.     | Investigative Features |
| E5   | Bool   | supportsFocus  |  N/A  |  DEVICE SPECIFICATION | Whether the screen supports focus-based inputs.  | Investigative Features |
| E6   | Float  | RefreshRate  |  N/A  |  DEVICE SPECIFICATION | MaxFramesPerSecond: The maximum number of frames per second that the screen is capable of (iOS \>= 10.3).     | Potential Label  |
| E8   | Int  | BatteryLevel   |  N/A  |  DEVICE SPECIFICATION | The battery charge level for the device.    | Potential Label  |
| E9   | Bool   | IsBatteryCharging  |  N/A  |  DEVICE SPECIFICATION | The battery power state of the device.   | Potential Label  |
| H4   | String   | IdentifierForVendor  |  N/A  |  DEVICE SPECIFICATION | A UUID that can be used to uniquely identify the device. The value of this property is the same for apps that come from the same vendor running on the same device. A different value is returned for apps on the same device that come from different vendors, and for apps on different devices regardless of vendor. Normally, the vendor is determined by data provided by the App Store. If the app was not installed from the App Store (for example, enterprise apps and apps still in development), then a vendor identifier is calculated based on the app's bundle ID. The bundle ID is assumed to be in reverse-DNS format. | Core Features  |
| H6   | String   | DeviceSystemName   |  N/A  |  DEVICE SPECIFICATION | The name of the operating system running on the device represented by the receiver (for example, iOS).       | Investigative Features |
| H7   | String   | DeviceSystemVersion  |  N/A  |  DEVICE SPECIFICATION | The current version of the operating system (for example, 12.0.1).        | Investigative Features |
| H8   | String   | UserInterfaceIdiom   |  N/A  |  DEVICE SPECIFICATION | The style of interface to use on the current device(for example, iPhone or iPad).       | Investigative Features |
| H9   | String   | DeviceModelName  |  N/A  |  DEVICE SPECIFICATION | Actual device model name used by Apple (for example, iPhone 7, iPhone 8 plus, or iPhone XS Max).      | Potential Label  |
| I1   | String   | KernelSysName  |  N/A  |  DEVICE SPECIFICATION | Kernel operating system name (for example, Darwin or Linux).        | Investigative Features |
| I2   | String   | KernelOsReleaseName  |  N/A  |  DEVICE SPECIFICATION | Kernel operating system release (for example, 18.0.3).        | Investigative Features |
| I4   | Bool   | IsMultitaskingSupported  |  N/A  |  DEVICE SPECIFICATION | A boolean value indicating whether multitasking is supported on the current device.      | Investigative Features |
| I6   | String   | ProcessName  |  N/A  |  DEVICE SPECIFICATION | The name of the process.  | Investigative Features |
| I7   | Int  | ProcessIdentifier  |  N/A  |  DEVICE SPECIFICATION | The identifier of the process (often called process ID).  | Investigative Features |
| I8   | String   | ProcessGloballyUniqueString  |  N/A  |  DEVICE SPECIFICATION | Global unique identifier for the process.   | Investigative Features |
| I9   | String   | ProcessOSVersionString   |  N/A  |  DEVICE SPECIFICATION | A string containing the version of the operating system on which the process is executing.  | Investigative Features |
| J1   | String   | ThermalState   |  N/A  |  DEVICE SPECIFICATION | The current thermal state to determine if your app should reduce system usage.  | Investigative Features |
| J2   | Bool   | IsLowPowerModeEnabled  |  N/A  |  DEVICE SPECIFICATION | Whether low power mode is enabled on an iOS device.   | Investigative Features |
| J3   | Int  | ActiveProcessorCount   |  N/A  |  DEVICE SPECIFICATION | The number of active processing cores available on the device. | Investigative Features |
| J4   | Int  | ProcessorCount   |  N/A  |  DEVICE SPECIFICATION | The number of processing cores available on the device.  | Investigative Features |
| J5   | DoubleArray  | CPUUsage     |  N/A  |  DEVICE SPECIFICATION | The CPU usage by device (0.39, System, User, Idle, Nice).        | Investigative Features |
| J6   | Long   | TotalMemory  |  N/A  |  DEVICE SPECIFICATION | Total RAM memory on device in bytes.           | Potential Label  |
| J7   | LongArray  | MemoryUsage  |  N/A  |  DEVICE SPECIFICATION | RAM memory usage by device in bytes (Free, Active, Inactive, Wired).        | Potential Label  |
| K5   | Long   | TotalInternalStorage   |  N/A  |  DEVICE SPECIFICATION | Total iInternal storage in bytes for device.        | Potential Label  |
| K6   | Long   | AvailableInternalStorage   |  N/A  |  DEVICE SPECIFICATION | Available internal storage in bytes for device.        | Potential Label  |
| L1   | DoubleArray  | AccelerometerData  |  N/A  | ACCELEROMETER  | Accelerometer reading (X-axis, Y-axis, Z-axis).         | Investigative Features |
| L2   | Double   | AccelerometerDataTimeStamp   |  N/A  | ACCELEROMETER  | Time at which the accelerometer data is valid.         | Investigative Features |
| M1   | DoubleArray  | GyroscopeData  |  N/A  | GYROSCOPE  | Gyroscope reading (X-axis, Y-axis, Z-axis).         | Investigative Features |
| M2   | Double   | GyroscopeDataTimeStamp   |  N/A  | GYROSCOPE  | Time at which the gyroscope data is valid.         | Investigative Features |
| O1   | Double   | Brightness   |  N/A  |USER PREFERENCE  | Screen brightness.         | Investigative Features |
| O2   | String   | CurrentScreenSizeInPixel   |  N/A  | USER PREFERENCE  | Current max screen width in pixels.          | Investigative Features |
| O4   | Float  | CurrentPixelAspectRatio  |  N/A  | USER PREFERENCE  | The aspect ratio of a single pixel. The ratio is defined as X/Y.  | Investigative Features |
| O5   | String   | DeviceOrientation  |  N/A  | USER PREFERENCE  | The physical orientation of the device.  | Investigative Features |
| O6   | Bool   | IsValidInterfaceOrientation  |  N/A  | USER PREFERENCE  | Whether the specified orientation is a portrait or landscape orientation.| Investigative Features |
| O7   | Bool   | IsGeneratingDeviceOrientationNotifications |  N/A  | USER PREFERENCE  | Whether the receiver generates orientation notifications.    | Investigative Features |
| O8   | String   | PassCodeOrBiometryIsEnabled  |  N/A  | USER PREFERENCE  | Passcode or biometry authentication set by user (for example, PassCodeOrBiometrySet, BiometryNotAvailable, PassCodeNotSet, etc.).     | Core Features  |
| O9   | String   | CurrentTimeZone  |  N/A  | USER PREFERENCE  | The time zone currently used by the system.   | Potential Label  |
| P1   | String   | AutoUpdatingCurrentTimeZone  |  N/A  | USER PREFERENCE  | The time zone currently used by the system. Automatically updates to the user's current preference.  | Investigative Features |
| P2   | String   | CurrentLocale  |  N/A  | USER PREFERENCE  | The user's current locale.   | Potential Label  |
| P3   | String   | AutoUpdatingCurrentLocale  |  N/A  | USER PREFERENCE  | A locale which tracks the user's current preferences.   | Investigative Features |
| P4   | String Array | PreferredLanguages   |  N/A  | USER PREFERENCE  | A list of the user's preferred languages.   | Potential Label  |
| P5   |  | IsMonoAudioEnabled   |  N/A  | USER PREFERENCE  | Whether system audio is mixed down from stereo to mono.  | Investigative Features |
| P6   | Bool   | IsClosedCaptioningEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for closed captioning is enabled.  | Investigative Features |
| P7   | Bool   | IsInvertColorsEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for invert colors is enabled. | Investigative Features |
| P8   | Bool   | IsGuidedAccessEnabled  |  N/A  | USER PREFERENCE  | Whether the app is running under guided access mode.   | Investigative Features |
| P9   | Bool   | IsBoldTextEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for bold text is enabled. | Investigative Features |
| Q1   | Bool   | IsGrayscaleEnabled   |  N/A  | USER PREFERENCE  | Whether the system preference for grayscale is enabled.      | Investigative Features |
| Q2   | Bool   | IsReduceTransparencyEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for reduce transparency is enabled.   | Investigative Features |
| Q3   | Bool   | IsReduceMotionEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for reduce motion is enabled.     | Investigative Features |
| Q4   | Bool   | IsVideoAutoplayEnabled   |  N/A  | USER PREFERENCE  | Whether the system preference for auto-play videos is enabled.      | Investigative Features |
| Q5   | Bool   | IsDarkerSystemColorsEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for darker colors is enabled.   | Investigative Features |
| Q6   | Bool   | IsSwitchControlRunning   |  N/A  | USER PREFERENCE  | Determine if switch control is running.    | Investigative Features |
| Q7   | Bool   | IsSpeakSelectionEnabled  |  N/A  | USER PREFERENCE  | Whether the system preference for speak selection is enabled.   | Investigative Features |
| Q8   | Bool   | IsSpeakScreenEnabled   |  N/A  | USER PREFERENCE  | Whether the system preference for speak screen is enabled.   | Investigative Features |
| Q9   | Bool   | IsShakeToUndoEnabled   |  N/A  | USER PREFERENCE  | Whether the system preference for shake to undo is enabled.         | Investigative Features |
| R1   | Bool   | IsAssistiveTouchRunning  |  N/A  | USER PREFERENCE  | Whether the system preference for assistive touch is enabled. Always returns false if guided access is not enabled.     | Investigative Features |
| R2   | Bool   | shouldDifferentiateWithoutColor  |  N/A  | USER PREFERENCE  | Whether the system preference for differentiate without color is enabled.      | Investigative Features |
| R3   | Bool   | IsOnOffSwitchLabelsEnabled   |  N/A  | USER PREFERENCE  | Whether the system preference for On/Off labels is enabled.        | Investigative Features |
| R4   | Bool   | CanSendMail  |  N/A  | USER PREFERENCE  | If the user has set up the device for sending email.         | Investigative Features |
| K1   | DoubleArray  | LocationData   | Location Services Authorization | LOCATION   | Current location data (latitude, longitude)    | Core Features  |
| K2   | Double   | Altitude     | Location Services Authorization | LOCATION   | The altitude of the location in meters. Can be positive (above sea level) or negative (below sea level).     | Core Features  |
| K3   | Double   | HorizontalAccuracy   | Location Services Authorization | LOCATION   | The horizontal accuracy of the location in meters.        | Core Features  |
| K4   | Double   | VerticalAccuracy   | Location Services Authorization | LOCATION   | The vertical accuracy of the location in meters.        | Core Features  |



## iOS technical reference


1.  Download the [iOS reference implementation](https://go.microsoft.com/fwlink/?linkid=2139005).

1.  Unzip the downloaded file and add all of the files to your iOS app project. 
 
1. You can initiate the reference implementation by calling: 

```plaintext
DynamicsFP.start(instanceId: \$tenantId) 

\$tenantId: Provided by Microsoft (GUID/UUID) 
```

You can initiate reference implementation on AppDelegate class so it can start collecting device attributes on app startup. Reference implementation does prompt for location permission. 

You can send collected device attributes to Fraud Protection by calling: 

```plaintext
DynamicsFP.send(pageId: \$pageId) 

\$pageId(Optional): SI=SignIn, SU=SignUp, P=Purchase 
```

You can call send() in any UIViewController before or on the page that has the  operation you need a risk assessment for. For sign in/sign up scenarios, you can call send() immediate after start() in AppDelegate class. 

Once you need the sessionId, get it by calling: `**var** sessionId = DynamicsFP.getSessionId() `  
 
SessionId is required when calling the risk assessment APIs. 

### iOS runtime permissions

-   Reference implementation uses CLLocationManager and checks for CLAuthorizationStatus.authorizedAlways or CLAuthorizationStatus.authorizedWhenInUse before requesting **location** data. The app should obtain CLLocationManager.requestWhenInUseAuthorization or CLLocationManager.requestAlwaysAuthorization permission from the user.

-   Reference implementation uses AppTrackingTransparency and checks for ATTrackingManager.AuthorizationStatus.authorized before collecting **AdvertisingId**. The app should obtain ATTrackingManager.requestTrackingAuthorization permission from the user.

## iOS additional references


[iOS Apple Developer](https://developer.apple.com/ios/)

[iOS Apple Development](https://developer.apple.com/develop/)

[Xcode](https://developer.apple.com/xcode/)


## Additional resources

[Dynamics 365 Fraud Protection API](https://apidocs.microsoft.com/services/dynamics365fraudprotection)

[Contact us](mailto:DFPHelp@microsoft.com)

