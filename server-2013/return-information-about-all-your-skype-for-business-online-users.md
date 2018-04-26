---
title: すべての Lync Online ユーザーに関する情報を返す
TOCTitle: すべての Lync Online ユーザーに関する情報を返す
ms:assetid: 0b59fadf-67e6-48ea-86f1-2efef500ebdf
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362769(v=OCS.15)
ms:contentKeyID: 56270049
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# すべての Lync Online ユーザーに関する情報を返す

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online で有効になっているすべてのユーザーに関する情報を返すには、パラメーターを追加せずに [Get-CsOnlineUser](get-csonlineuser.md) コマンドレットを呼び出します。

    Get-CsOnlineUser

ランダムに選択した 1 人のユーザーに関する情報を返す (たとえば、テスト目的にこのアカウントを使用する) には、**Get-CsOnlineUser** コマンドレットを呼び出して ResultSize パラメーターを 1 に設定します。

    Get-CsOnlineUser -ResultSize 1

このようにすると、**Get-CsOnlineUser** コマンドレットにより、組織内のユーザーの数に関係なく、1 人のユーザーのみに関する情報が返されます。5 人のユーザーに関する情報を返すには、ResultSize パラメーターの値を 5 に設定します。

    Get-CsOnlineUser -ResultSize 5

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

