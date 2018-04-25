---
title: ユーザーにユーザーごとのポリシーを割り当てる
TOCTitle: ユーザーにユーザーごとのポリシーを割り当てる
ms:assetid: 37e07da7-6391-4d6d-a428-c70272897039
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362779(v=OCS.15)
ms:contentKeyID: 56270063
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ユーザーにユーザーごとのポリシーを割り当てる

 

_**トピックの最終更新日:** 2015-06-22_

ユーザーごとのポリシーをユーザーに割り当てるには、まず適切な **Grant-Cs** コマンドレット (たとえば、ユーザーごとの音声ポリシーを割り当てる場合は [Grant-CsVoicePolicy](grant-csvoicepolicy.md)) を選ぶ必要があります。コマンドレットを実行し、必ず、ポリシーを割り当てるユーザーの Identity と割り当てるポリシーの名前の両方を指定します。

    Grant-CsVoicePolicy -Identity "Ken Myer" -PolicyName "RedmondVoicePolicy"

すべてのユーザーに同じポリシーを割り当てる場合は、次の構文を使用します。

    Get-CsOnlineUser | Grant-CsVoicePolicy -PolicyName "RedmondVoicePolicy"

ライセンス契約と国/地域の制限の違いにより、一部の会議ポリシー、外部アクセス ポリシー、またはモビリティ ポリシーを特定のユーザーに割り当てることはできません。特定のユーザー (kenmyer@litwareinc.com など) に実際に割り当てることができるユーザーごとのポリシーを確認するには、必要に応じて次のいずれかのコマンド (および ApplicableTo パラメーター) を使用します。

    Get-CsConferencingPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsExternalAccessPolicy -ApplicableTo "kenmyer@litwareinc.com"
    Get-CsMobilityPolicy -ApplicableTo "kenmyer@litwareinc.com"

上記の構文は、Ken Myer に実際に割り当てることができるユーザーごとのポリシーのみを返します。

## 関連項目

#### 概念

[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

