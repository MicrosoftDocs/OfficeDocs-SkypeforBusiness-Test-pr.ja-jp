---
title: 'Lync Online: 許可されたドメインのリストにドメインを追加する'
TOCTitle: 許可されたドメインのリストにドメインを追加する
ms:assetid: 7b7f76c8-3047-40be-a938-8ac2868a6bc8
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362818(v=OCS.15)
ms:contentKeyID: 56270104
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online で許可されたドメインのリストにドメインを追加する

 

_**トピックの最終更新日:** 2015-06-22_

許可されたドメイン リストに最初のドメインを追加するには、3 つの手順のプロセスを実行します。まず、[New-CsEdgeDomainPattern](new-csedgedomainpattern.md) コマンドレットを使用して、追加するドメインのドメイン オブジェクトを作成します。

    $x = New-CsEdgeDomainPattern -Domain "fabrikam.com"

次に、[New-CsEdgeAllowList](new-csedgeallowlist.md) コマンドレットを使用して、ドメイン オブジェクトが含まれる新しい許可されたリストを作成します。

    $newAllowList = New-CsEdgeAllowList -AllowedDomain $x

最後に、[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) コマンドレットを使用して、新しい許可されたリストを Skype for Business Online に書き込みます。

    Set-CsTenantFederationConfiguration -AllowedDomains $newAllowList

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

