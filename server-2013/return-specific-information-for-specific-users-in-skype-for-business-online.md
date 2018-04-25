---
title: 特定のユーザーの特定の情報の取得
TOCTitle: 特定のユーザーの特定の情報の取得
ms:assetid: bbee85bd-d8a7-4b28-90d7-45c43eee48f6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362838(v=OCS.15)
ms:contentKeyID: 56270138
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 特定のユーザーの特定の情報の取得

 

_**トピックの最終更新日:** 2015-06-22_

既定では、[Get-CsOnlineUser](get-csonlineuser.md) コマンドレットを実行すると Skype for Business Online ユーザー アカウントの非常に大量の情報が返されます。その情報のサブセットのみが必要な場合は、返されたデータを **Select-Object** コマンドレットにパイプ処理します。たとえば、次のコマンドを実行すると Ken Myer のすべてのデータが返され、**Select-Object** コマンドレットによって画面に表示される情報が Ken の Active Directory ドメイン サービスの表示名とダイヤル プランに限定されます。

    Get-CsOnlineUser -Identity "Ken Myer" | Select-Object DisplayName, DialPlan

次のコマンドを実行すると、すべてのユーザーの表示名とダイヤル プランが返されます。

    Get-CsOnlineUser | Select-Object DisplayName, DialPlan

Skype for Business Online ユーザー アカウントのプロパティを検索するには、次のコマンドを使用します。

    Get-CsOnlineUser | Get-Member

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

