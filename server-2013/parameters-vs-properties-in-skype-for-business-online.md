---
title: パラメーターとプロパティの対比
TOCTitle: パラメーターとプロパティの対比
ms:assetid: 65348f95-f4d4-40cd-8869-f9d72643792d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362796(v=OCS.15)
ms:contentKeyID: 56270088
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# パラメーターとプロパティの対比

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online のコマンドレットに関するヘルプ トピップを表示すると、パラメーターとプロパティという用語が同じような意味で使用されていることがあります。この用語に混乱することがないようにしてください。2 つの用語は、技術的には異なりますが、Skype for Business Online でこれらの用語は基本的には同じものを指します。

技術的に言えば、コマンドレットを実行する場合にパラメーターを使用します。たとえば、以下の Windows PowerShell コマンドでは、EnableMicrosoftPushNotificationService および EnableApplePushNotificationService は [Set-CsPushNotificationConfiguration](set-cspushnotificationconfiguration.md) コマンドレットのパラメーターです。

    Set-CsPushNotificationConfiguration -EnableMicrosoftPushNotificationService -EnableApplePushNotificationService $True

プロパティとは、Skype for Business Online のオブジェクト (たとえば、プッシュ通知構成設定のコレクション) の属性です。次のコマンドを実行するとします。

    Set-CsPushNotificationConfiguration

実行すると、次の項目が含まれる、プロパティとそれらに関連付けられた値のコレクションが戻されます。

    EnableMicrosoftPushNotificationService : True
    EnableApplePushNotificationService     : True

上記からわかるように、プロパティとパラメーターは同じ名前を共有しています。つまり、EnableMicrosoftPushNotificationService パラメーターを使用して EnableMicrosoftPushNotificationService プロパティの値を構成しています。

## 関連項目

#### 概念

[Windows PowerShell と Lync Online の概要](an-introduction-to-windows-powershell-and-skype-for-business-online.md)

