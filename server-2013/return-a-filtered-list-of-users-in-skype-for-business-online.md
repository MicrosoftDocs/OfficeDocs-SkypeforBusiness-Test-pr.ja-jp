---
title: フィルタリングされたユーザー リストの取得
TOCTitle: フィルタリングされたユーザー リストの取得
ms:assetid: f2c4d13b-8601-4192-8b94-e9a57969da11
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362858(v=OCS.15)
ms:contentKeyID: 56270159
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# フィルタリングされたユーザー リストの取得

 

_**トピックの最終更新日:** 2015-06-22_

[Get-CsOnlineUser](get-csonlineuser.md) コマンドレットと、LdapFilter パラメーターか Filter パラメーターを使用すると、対象のユーザー群に関する情報を簡単に取得できます。たとえば、次のコマンドを実行すると財務部門に属するすべてのユーザーが返されます。

    Get-CsOnlineUser -LdapFilter "department=Finance"

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

