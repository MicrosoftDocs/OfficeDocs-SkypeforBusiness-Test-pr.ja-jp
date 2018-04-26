---
title: このユーザーの同時シェルの最大数の超過
TOCTitle: このユーザーの同時シェルの最大数の超過
ms:assetid: b309efe8-a214-41ea-a345-93e6a36e0cb1
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362837(v=OCS.15)
ms:contentKeyID: 56270133
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# このユーザーの同時シェルの最大数の超過

 

_**トピックの最終更新日:** 2015-06-22_

管理者ごとに、Skype for Business Online への同時リモート接続が 3 つまで許可されています。Windows PowerShell への 3 つのリモート接続を実行している場合に、4 番目の同時接続を実行しようとすると、次のエラー メッセージが表示されて失敗します。

    New-PSSession : [admin.vdomain.com] リモート サーバー admin.vdomain.com への接続に失敗し、次のエラー メッセージが返されました:WS-Management サービスは要求を処理できません。このユーザーが同時に実行できるシェルの最大数を超過しています。既に実行中のシェルを終了するか、このユーザーのクォータを増やしてください。詳しくは、「about_Remote_Troubleshooting」ヘルプ トピックをご覧ください。

この問題を解決する唯一の方法は、前の接続を 1 つ以上閉じることです。Skype for Business Online セッションを終了したら、**Remove-PSSession** コマンドレットを使用してこのセッションを終了することをお勧めします。この操作を実行すれば、この問題を回避できます。

## 関連項目

#### 概念

[Lync Online との接続の問題の診断と解決](diagnosing-and-resolving-connection-problems-with-skype-for-business-online.md)

