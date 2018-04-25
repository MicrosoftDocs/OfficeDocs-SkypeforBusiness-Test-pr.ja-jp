---
title: Lync Online テナントに関する情報を取得する
TOCTitle: Lync Online テナントに関する情報を取得する
ms:assetid: 06467515-9114-45bb-8d09-26a915c3fc4d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362768(v=OCS.15)
ms:contentKeyID: 56270050
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online テナントに関する情報を取得する

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online テナントに関する情報を返すには、追加パラメーターなしで [Get-CsTenant](get-cstenant.md) コマンドレットを呼び出します。

    Get-CsTenant

テナント名と ID (TenantID パラメーターの値は、[Set-CsTenantPublicProvider](set-cstenantpublicprovider.md) や [Set-CsTenantFederationConfiguration](set-cstenantfederationconfiguration.md) などのコマンドレットの実行時に必要) のみを返すには、次のコマンドを使用します。

    Get-CsTenant | Select-Object Name, TenantID

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

