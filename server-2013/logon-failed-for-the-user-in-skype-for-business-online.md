---
title: ユーザーのログオン エラー
TOCTitle: ユーザーのログオン エラー
ms:assetid: 006020cd-34d0-4a78-b5b4-e382d95ef04d
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn329053(v=OCS.15)
ms:contentKeyID: 56270044
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーのログオン エラー

 

_**トピックの最終更新日:** 2015-06-22_

Skype for Business Online へのリモート接続を試行するときには、有効な Skype for Business Online ユーザー アカウントのユーザー名とパスワードを指定する必要があります。指定しないと、以下のようなエラー メッセージが表示されてログオンが失敗します。

    Get-CsWebTicket : ユーザー 'kenmyer@litwareinc.com' のログオンに失敗しました。正しいユーザー名とパスワードが使用されていることを確認し、新しい PSCredential オブジェクトを作成してください。.

有効なユーザー アカウントを使用していて、パスワードが正しいと考えられる場合は、ログオンを再試行します。再試行が失敗した場合は、同じ資格情報を使用して <https://login.microsoftonline.com/> でログオンを試行します。この場所でもログオンできない場合は、Office 365 サポートにお問い合わせください。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

