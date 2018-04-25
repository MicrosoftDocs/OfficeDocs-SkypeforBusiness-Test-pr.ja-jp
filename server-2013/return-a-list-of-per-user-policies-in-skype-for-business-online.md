---
title: ユーザーごとのポリシーのリストの取得
TOCTitle: ユーザーごとのポリシーのリストの取得
ms:assetid: e95a2755-3501-40cc-a704-5ecd01839d76
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362856(v=OCS.15)
ms:contentKeyID: 56270156
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーごとのポリシーのリストの取得

 

_**トピックの最終更新日:** 2015-06-22_

使用可能なユーザーごとのポリシーのリストを返すには、まず適切な **Get-Cs** コマンドレット (ユーザーごとの音声ポリシーを返したい場合は [Get-CsVoicePolicy](get-csvoicepolicy.md) コマンドレットなど) を選びます。次に、以下の構文を使用してユーザーごとの各ポリシーの ID を返します。

    Get-CsVoicePolicy -Filter "tag:*" | Select-Object Identity

ライセンス契約や、国/地域による制限事項はさまざまであるため、特定のユーザーに対して特定の会議ポリシー、外部アクセス ポリシー、モビリティ ポリシーなどを割り当てられない場合があります。所定のユーザー (jun@example.com など) に実際に割り当てられるユーザーごとのポリシーを確認するには、必要に応じて次のいずれかのコマンド (および ApplicableTo パラメーター) を使用します。

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

上記の構文では、Ken Myer に実際に割り当てられるユーザーごとのポリシーのみが返されます。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

