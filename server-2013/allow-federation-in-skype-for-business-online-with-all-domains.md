---
title: すべてのドメインとのフェデレーションの許可
TOCTitle: すべてのドメインとのフェデレーションの許可
ms:assetid: d26f1057-a76c-447a-9efe-72efdce4c15e
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362855(v=OCS.15)
ms:contentKeyID: 56270151
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# すべてのドメインとのフェデレーションの許可

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーに対して任意のドメインのユーザーとの通信を許可する場合、2 つの手順が必要です。まず、[New-CsEdgeAllowAllKnownDomains](new-csedgeallowallknowndomains.md) コマンドレットを使用して AllowAllKnownDomains オブジェクトのインスタンスを作成します。

    $x = New-CsEdgeAllowAllKnownDomains

次に [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) コマンドレットを呼び出して、AllowedDomains プロパティの値を AllowAllKnownDomains オブジェクトが含まれる変数 (この例では $x) に設定します。

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

