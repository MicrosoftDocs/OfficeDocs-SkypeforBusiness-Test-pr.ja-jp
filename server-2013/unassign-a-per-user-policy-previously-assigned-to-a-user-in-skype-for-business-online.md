---
title: 以前にユーザーに割り当てられたユーザーごとのポリシーの割り当て解除
TOCTitle: 以前にユーザーに割り当てられたユーザーごとのポリシーの割り当て解除
ms:assetid: bdba1d22-28e4-4203-a109-a3fb408783d3
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362840(v=OCS.15)
ms:contentKeyID: 56270140
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 以前にユーザーに割り当てられたユーザーごとのポリシーの割り当て解除

 

_**トピックの最終更新日:** 2015-06-22_

以前ユーザーに割り当てられていたユーザーごとのポリシーの割り当てを解除したい場合は、該当する **Grant-Cs** コマンドレット (音声ポリシーの割り当て解除には [Grant-CsVoicePolicy](grant-csvoicepolicy.md) コマンドレットなど) を再実行し、PolicyName パラメーターを NULL 値 ($Null) に設定します。

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName $Null

すべてのユーザーの音声ポリシーを割り当て解除するには、次のコマンドを使用します。

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName $Null

ユーザーからポリシーが割り当て解除されると、そのユーザーはグローバル ポリシーで管理されるようになります。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

