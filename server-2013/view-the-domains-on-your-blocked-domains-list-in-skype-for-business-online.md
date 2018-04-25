---
title: 禁止ドメインの一覧でドメインを表示する
TOCTitle: 禁止ドメインの一覧でドメインを表示する
ms:assetid: 67c65dbf-1a68-4c77-aabd-bed5001b4267
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362797(v=OCS.15)
ms:contentKeyID: 56270091
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 禁止ドメインの一覧でドメインを表示する

 

_**トピックの最終更新日:** 2015-06-22_

禁止ドメインの一覧上のすべてのドメインを表示するには、[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) コマンドレットを呼び出し、返されたデータを **Select-Object** コマンドレットにパイプ処理します。

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty BlockedDomains

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

