---
title: 会議の記録の有効化/無効化
TOCTitle: 会議の記録の有効化/無効化
ms:assetid: f6c5afab-081c-495c-97f7-135dcc2f6085
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362857(v=OCS.15)
ms:contentKeyID: 56270160
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 会議の記録の有効化/無効化

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーにオンライン会議を記録させたくない場合は、[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) コマンドレットを使用して AllowConferenceRecording パラメーターの値を False ($False) に設定します。

    Set-CsMeetingConfiguration -AllowConferenceRecording $False

オンライン会議を記録できるように設定を戻したい場合は、AllowConferenceRecording パラメーターの値を True ($True) に設定します。

    Set-CsMeetingConfiguration -AllowConferenceRecording $True

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

