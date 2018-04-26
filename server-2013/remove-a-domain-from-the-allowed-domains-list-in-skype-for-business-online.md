---
title: 許可ドメインの一覧からドメインを削除する
TOCTitle: 許可ドメインの一覧からドメインを削除する
ms:assetid: 04948582-363b-49bd-8305-166c4c1d0dd9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362766(v=OCS.15)
ms:contentKeyID: 56270046
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 許可ドメインの一覧からドメインを削除する

 

_**トピックの最終更新日:** 2015-06-22_

許可ドメインの一覧からドメインを削除するには、一連の手順が必要です。まず、現時点で一覧にあるすべてのドメインのコレクションを取得するために、次のようなコマンドを使用する必要があります。

    $x = (Get-CsTenantFederationConfiguration).AllowedDomains

続いて、次のコマンドを実行してこれらのドメインを確認します。

``` 
$x
```

削除するドメインの位置をメモします。ドメインが一覧の最初のドメインである場合、インデックス値は 0 です。ドメインが一覧の 2 番目のドメインである場合のインデックス値は 1、のようになります。

インデックス番号が判明した後、次のようなコマンドを使用して指定のドメインを削除しますが、必ず正しいインデックス番号を使用してください。次のコマンドにより、一覧の最初のドメイン (インデックス番号 0) が削除されます。

    $x.AllowedDomain.RemoveAt(0)

最後に、[Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) コマンドレットを呼び出して、変更を Skype for Business Online に書き込みます。

    Set-CsTenantFederationConfiguration -AllowedDomains $x

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

