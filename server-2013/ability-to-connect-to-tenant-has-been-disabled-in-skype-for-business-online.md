---
title: テナントに接続する機能が無効化されている
TOCTitle: テナントに接続する機能が無効化されている
ms:assetid: 7365d31b-173e-4339-b0a3-98ab73a9558f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362820(v=OCS.15)
ms:contentKeyID: 56270102
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# テナントに接続する機能が無効化されている

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online を管理するために Windows PowerShell を使用するには、テナントの Windows PowerShell ポリシーの EnableRemotePowerShellAccess プロパティを True に設定する必要があります。このように設定しないと、接続は失敗し、次のエラー メッセージが表示されます。

    New-PSSession : [admin.vdomain.com] リモート サーバー admin.vdomain.com からのデータの処理に失敗し、次のエラー メッセージが返されました:リモート PowerShell セッションを使ってこのテナントに接続する機能は無効になっています。このテナントのテナント PowerShell ポリシーを確認するには、Lync ヘルプにお問い合わせください。詳しくは、「about_Remote_Troubleshooting」のヘルプ トピックをご覧ください。.

このエラー メッセージが表示された場合は、Office 365 サポートに連絡して、Windows PowerShell のリモート アクセスを有効にするよう依頼する必要があります。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

