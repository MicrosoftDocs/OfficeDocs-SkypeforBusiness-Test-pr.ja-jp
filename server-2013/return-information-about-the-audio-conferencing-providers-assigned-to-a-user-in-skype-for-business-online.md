---
title: ユーザーに割り当てられている電話会議プロバイダーに関する情報を返す
TOCTitle: ユーザーに割り当てられている電話会議プロバイダーに関する情報を返す
ms:assetid: 7fae822f-9f6c-4381-95c5-879661027925
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362814(v=OCS.15)
ms:contentKeyID: 56270110
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーに割り当てられている電話会議プロバイダーに関する情報を返す

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーに割り当てられた電話会議プロバイダーに関する情報を返すには、[Get-CsUserAcp](get-csuseracp.md) コマンドレットと次の構文を使用します。

    Get-CsUserAcp -Identity "Ken Myer" | Select-Object -ExpandProperty AcpInfo

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

