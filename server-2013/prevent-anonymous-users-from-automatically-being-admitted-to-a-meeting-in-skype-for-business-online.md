---
title: 匿名ユーザーが自動的に会議に承認されないようにする
TOCTitle: 匿名ユーザーが自動的に会議に承認されないようにする
ms:assetid: 23f120d2-4c39-4509-aa1f-4d186a525075
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362775(v=OCS.15)
ms:contentKeyID: 56270058
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# 匿名ユーザーが自動的に会議に承認されないようにする

 

_**トピックの最終更新日:** 2015-06-22_

匿名ユーザーが自動的にオンライン会議に承認されることを禁止するには、[Set-CsMeetingConfiguration](set-csmeetingconfiguration.md) コマンドレットを使用し、AdmitAnonymousUsersByDefault プロパティを False ($False) に設定します。

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $False

自動的な承認を有効にするには、AdmitAnonymousUsersByDefault プロパティを True ($True) に設定して戻します。

    Set-CsMeetingConfiguration -AdmitAnonymousUsersByDefault $True

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

