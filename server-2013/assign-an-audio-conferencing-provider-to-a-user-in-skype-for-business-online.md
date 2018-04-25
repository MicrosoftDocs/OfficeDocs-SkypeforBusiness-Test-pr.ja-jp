---
title: ユーザーに電話会議プロバイダーを割り当てる
TOCTitle: ユーザーに電話会議プロバイダーを割り当てる
ms:assetid: 60db6896-9c5c-4d64-ab7e-10d91748587c
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362791(v=OCS.15)
ms:contentKeyID: 56270085
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーに電話会議プロバイダーを割り当てる

 

_**トピックの最終更新日:** 2015-06-22_

[Set-CsUserAcp](set-csuseracp.md) コマンドレットは、ユーザーに音声会議プロバイダーを割り当てる手段を提供します。

    Set-CsUserAcp -Identity "Ken Myer" -TollNumber "12065551219" -TollFreeNumbers "18005550712" -ParticipantPasscode "p@ssw0rd" -Domain "sip.contoso.com" -Name "Contoso ACP"

まだ指定のプロバイダーと契約していない場合は、この割り当ては無意味になります。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

