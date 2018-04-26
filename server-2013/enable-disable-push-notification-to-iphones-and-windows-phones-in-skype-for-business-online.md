---
title: iPhone および Windows Phone へのプッシュ通知を有効化/無効化する
TOCTitle: iPhone および Windows Phone へのプッシュ通知を有効化/無効化する
ms:assetid: 64482dcb-6354-4fb5-a2e4-1564b3d0e047
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362792(v=OCS.15)
ms:contentKeyID: 56270086
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# iPhone および Windows Phone へのプッシュ通知を有効化/無効化する

 

_**トピックの最終更新日:** 2015-06-22_

プッシュ通知を iPhone または Windows Phone に送信しないようにするには、[Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) コマンドレットを使用し、EnableApplePushNotificationService プロパティと EnableMicrosoftPushNotificationService プロパティの値を False ($False) に設定します。

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $False

iPhone と Windows Phone の設定は個別に行うことができる点に注意してください。たとえば、次のコマンドは iPhone 上のプッシュ通知を無効にしますが、Windows Phone 上のプッシュ通知を有効にします。

    Set-CsPushNotificationConfiguration -EnableApplePushNotificationService $False -EnableMicrosoftPushNotificationService $True

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

