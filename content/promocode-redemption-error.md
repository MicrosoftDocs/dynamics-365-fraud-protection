---
author: josaw1
description: This topic provides troubleshooting guidance for when a global administrator encounters an error while attempting to redeem a Microsoft Dynamics 365 Fraud Protection promotion code.
ms.author: josaw
ms.date: 04/10/2024
ms.topic: reference
search.audienceType:
  - admin
title: Troubleshoot promotion code redemption error
ms.custom:
---

# Troubleshoot - Promotion code redemption error
## Cause: Trial account blocked by company policy

When attempting to redeem a Fraud Protection promotion code, a global administrator may encounter the following error: 

`Trial signup blocked by company policy`

This error is caused by your company disabling ad hoc subscriptions, which blocks accounts from redeeming trial promotion codes. To successfully redeem the promotion code, you must temporarily enable the **[AllowAdHocSubscriptions](/powershell/module/msonline/set-msolcompanysettings)** setting. You can then redeem the promotion code and disable the setting again afterwards.

This setting is not specific to Dynamics 365 Fraud Protection. It can also block your ability to redeem trial promotion codes for other Microsoft products.

> [!NOTE] 
> You or another administrator may have disabled the **AllowAdHocSubscriptions** PowerShell setting to prevent certain types of signups at your company. It is recommended that you check with your company colleagues before temporarily enabling ad hoc subscriptions.

## Solution: Temporarily enable ad hoc subscriptions

> [!NOTE]
> You'll need to be an Azure global administrator in your tenant to run this code.

1. Start PowerShell and run the following three commands. The second command will prompt you for your credentials.

    ```PowerShell
    Install-Module MSOnline
    Connect-MsolService
    Get-MsolCompanyInformation | fl AllowAdHocSubscriptions
    ```

1. If the third command outputs **False** and you're ready to temporarily allow these signups, run the following command.

    ```PowerShell
    Set-MsolCompanySettings -AllowAdHocSubscriptions $true
    ```

1. On the Fraud Protection site, try to redeem your promotion code again.
1. If you're able to redeem your Fraud Protection promotion code and ready to disable ad hoc subscriptions again, run the following commands. The output of the second command should again be **False**.

    ```PowerShell
    Set-MsolCompanySettings -AllowAdHocSubscriptions $false
    Get-MsolCompanyInformation | fl AllowAdHocSubscriptions
    ```

## Support

To log a support ticket, sign in to [Fraud Protection](https://dfp.microsoft.com) and select the question mark in the header bar.

[!INCLUDE[footer-include](includes/footer-banner.md)]
