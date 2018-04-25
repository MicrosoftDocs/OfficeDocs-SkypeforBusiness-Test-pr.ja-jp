---
title: 禁止ドメイン リストからのドメインの削除
TOCTitle: 禁止ドメイン リストからのドメインの削除
ms:assetid: a11ea475-bb8b-44be-a5a5-4abb2fed42b8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362830(v=OCS.15)
ms:contentKeyID: 56270118
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 禁止ドメイン リストからのドメインの削除

 

_**トピックの最終更新日:** 2015-06-22_

禁止ドメイン リストからドメインを削除するには、2 つの手順が必要です。まず [New-CsEdgeDomainPattern](new-csedgedomainpattern.md) コマンドレットを使用して、削除するドメインのドメイン オブジェクトを作成する必要があります。

    $x = New-CsEdgeDomainPattern "fabrikam.com"

このオブジェクトを作成したら、次の構文を使用して、禁止ドメイン リストからドメインを削除します (この例では、ドメインは変数 $x に保存されています)。

    Set-CsTenantFederationConfiguration -BlockedDomains @{Remove=$x}

禁止ドメイン リストからすべてのドメインを削除するには、BlockedDomains プロパティの値を NULL ($Null) に設定します。

    Set-CsTenantFederationConfiguration -BlockedDomains $Null

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

