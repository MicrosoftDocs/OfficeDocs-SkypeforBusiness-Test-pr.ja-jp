---
title: 許可ドメインの一覧でドメインを表示する
TOCTitle: 許可ドメインの一覧でドメインを表示する
ms:assetid: 13bceaba-5c4f-431f-864f-9e374cafa986
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362772(v=OCS.15)
ms:contentKeyID: 56270053
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 許可ドメインの一覧でドメインを表示する

 

_**トピックの最終更新日:** 2015-06-22_

許可ドメインの一覧上のすべてのドメインを表示するには、[Get-CsTenantFederationConfiguration](get-cstenantfederationconfiguration.md) と次の構文を使用します。

    Get-CsTenantFederationConfiguration | Select-Object -ExpandProperty AllowedDomains | Select-Object AllowedDomain

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

