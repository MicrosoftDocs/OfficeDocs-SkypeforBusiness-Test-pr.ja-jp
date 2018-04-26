---
title: 特定のユーザーに関する情報を返す
TOCTitle: 特定のユーザーに関する情報を返す
ms:assetid: 6c8c2190-8e62-4f92-bbe9-4f692bd7ebf5
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362803(v=OCS.15)
ms:contentKeyID: 56270099
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 特定のユーザーに関する情報を返す

 

_**トピックの最終更新日:** 2015-06-22_

[Get-CsOnlineUser](get-csonlineuser.md) コマンドレットを呼び出す際に特定のユーザー アカウントを参照するには複数の方法があります。ユーザーの Active Directory ドメイン サービスの表示名を使用できます。

    Get-CsOnlineUser -Identity "Ken Myer"

ユーザーの SIP アドレスを使用できます。

    Get-CsOnlineUser -Identity "sip:kenmyer@litwareinc.com"

ユーザーのユーザー プリンシパル名 (UPN) を使用できます。

    Get-CsOnlineUser -Identity "kenmyer@litwareinc.com"

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

