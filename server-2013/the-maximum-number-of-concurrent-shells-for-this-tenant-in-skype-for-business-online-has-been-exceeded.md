---
title: このテナントの同時シェルの最大数の超過
TOCTitle: このテナントの同時シェルの最大数の超過
ms:assetid: a4c91ffa-fdcc-414c-b941-a0d36c906825
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362832(v=OCS.15)
ms:contentKeyID: 56270129
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# このテナントの同時シェルの最大数の超過

 

_**トピックの最終更新日:** 2015-06-22_

各管理者が Skype for Business Online テナントに対して許可されている同時接続の最大数は 3 ですが、1 つのテナントで許可されている同時接続の最大数は 9 です。たとえば、3 人の管理者がそれぞれ 3 つのオープン セッションを持っているとします。4 人目の管理者が接続しようとする (同時接続の総数が 10 になる) と、この操作は失敗し、次のエラー メッセージが表示されます。

    New-PSSession : [admin.vdomain.com] リモート サーバー admin.vdomain.com への接続に失敗し、次のエラー メッセージが返されました:WS-Management サービスは要求を処理できません。このテナントの同時シェルの最大数を超えました。既存のシェルを閉じるか、このテナントのクォータを増やしてください。詳しくは、「about_Remote_Troubleshooting」のヘルプ トピックをご覧ください。.

この問題を解決する唯一の方法は、前の接続を 1 つ以上閉じることです。Skype for Business Online セッションでの作業を終了したら、**Remove-PSSession** コマンドレットを使用してこのセッションを終了することをお勧めします。この操作により、この問題を回避できます。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

