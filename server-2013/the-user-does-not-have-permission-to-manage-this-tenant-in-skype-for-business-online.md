---
title: ユーザーにこのテナントを管理するためのアクセス許可がない
TOCTitle: ユーザーにこのテナントを管理するためのアクセス許可がない
ms:assetid: 714ccf81-9451-4585-b62d-979f2a606315
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362812(v=OCS.15)
ms:contentKeyID: 56270096
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーにこのテナントを管理するためのアクセス許可がない

 

_**トピックの最終更新日:** 2015-06-22_

テナント管理者グループのメンバーでない場合は、Skype for Business Online への Windows PowerShell のリモート接続を行うことはできません。このメンバーではない場合、接続試行は失敗し、次のエラー メッセージが表示されます。

    New-PSSession : [admin.vdomain.com] リモート サーバー admin.vdomain.com からのデータの処理に失敗し、次のエラー メッセージが返されました:ユーザー 'user@foo.com' はこのテナントを管理するための権限を持っていません。権限は、ユーザーを適切な RBAC 役割に割り当てることで付与できます。詳しくは、「about_Remote_Troubleshooting」のヘルプ トピックをご覧ください。.

ご自身がテナント管理者グループのメンバーであると判断される、またはメンバーであると想定されている場合は、Office 365 サポートに連絡する必要があります。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

