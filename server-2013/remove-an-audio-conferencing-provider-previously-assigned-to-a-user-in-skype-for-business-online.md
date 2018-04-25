---
title: 以前にユーザーに割り当てられた電話会議プロバイダーの削除
TOCTitle: 以前にユーザーに割り当てられた電話会議プロバイダーの削除
ms:assetid: 85d59e6c-d646-4908-9767-adb48763f6de
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362808(v=OCS.15)
ms:contentKeyID: 56270121
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 以前にユーザーに割り当てられた電話会議プロバイダーの削除

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーに割り当てられている電話会議プロバイダーをすべて削除するには、パラメーターなしで [Remove-CsUserAcp](remove-csuseracp.md) コマンドレットを実行します (対象のユーザーを示す Identity パラメーターは除きます)。

    Remove-CsUserAcp -Identity "Ken Myer"

ユーザーに複数の電話会議プロバイダーが割り当てられている場合は、Name パラメーターの後に削除対象のプロバイダー名を追加すると 1 つのプロバイダーを削除できます。

    Remove-CsUserAcp -Identity "Ken Myer" -Name "Contoso ACP"

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

