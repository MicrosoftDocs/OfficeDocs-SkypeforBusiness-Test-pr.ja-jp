---
title: 'Lync Online: 禁止されているドメインのリストにドメインを追加する'
TOCTitle: 禁止されているドメインのリストにドメインを追加する
ms:assetid: ea6ebeea-3031-4c42-9a2c-88eaab790636
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362853(v=OCS.15)
ms:contentKeyID: 56270157
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online で禁止されているドメインのリストにドメインを追加する

 

_**トピックの最終更新日:** 2015-06-22_

禁止されたドメイン リストにドメインを追加するには、次のような構文を使用します。

    $x = New-CsEdgeDomainPattern "fabrikam.com"
    Set-CsTenantFederationConfiguration -BlockedDomains @{Add=$x}

上記からわかるように、このコマンドには 2 つのステップが必要です。まず、[New-CsEdgeDomainPattern](new-csedgedomainpattern.md) を使用して、禁止リストに追加するドメインを表すドメイン オブジェクトを作成します。続いて、[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) コマンドレットと Add メソッドを使用して、リストにそのドメイン (この例では変数 $x に格納されているドメイン) を追加します。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

