---
title: 電話会議プロバイダーに関する情報の取得
TOCTitle: 電話会議プロバイダーに関する情報の取得
ms:assetid: df9c8fc0-8bb6-4416-a5cc-aa9b1601a688
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362848(v=OCS.15)
ms:contentKeyID: 56270148
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 電話会議プロバイダーに関する情報の取得

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーに割り当てられている電話会議プロバイダーに関する情報を取得するには、[Get-CsUserAcp](get-csuseracp.md) コマンドレットと次の構文を使用します。

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

