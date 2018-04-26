---
title: ポリシーの管理
TOCTitle: ポリシーの管理
ms:assetid: 91372888-a96e-44db-a0dc-d08facbfce87
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362826(v=OCS.15)
ms:contentKeyID: 56270122
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# ポリシーの管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットで Skype for Business Online ポリシーを管理します。ポリシーによって、ユーザーと組織が使用できる Skype for Business Online 機能が全体的に決定されます。


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>コマンドレット</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="get-csclientpolicy.md">Get-CsClientPolicy</a><br />
<a href="grant-csclientpolicy.md">Grant-CsClientPolicy</a></p></td>
<td><p>クライアント ポリシーによって、ユーザーが使用できる Lync クライアント機能を決定します。たとえば、一部のユーザーだけファイル転送機能を使用できるようにします。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csconferencingpolicy.md">Get-CsConferencingPolicy</a><br />
<a href="grant-csconferencingpolicy.md">Grant-CsConferencingPolicy</a></p></td>
<td><p>会議ポリシーによって、会議で使用できる機能を決定します。これには、会議で IP 音声/ビデオを使用できるかどうかや、会議に出席できる最大人数など、すべての機能が含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csexternalaccesspolicy.md">Get-CsExternalAccessPolicy</a><br />
<a href="grant-csexternalaccesspolicy.md">Grant-CsExternalAccessPolicy</a></p></td>
<td><p>外部アクセス ポリシーによって、ユーザーがフェデレーション ドメインのユーザーや、パブリック IM プロバイダー (Windows Live や AOL など) のアカウントを持つユーザーと通信できるかどうかを決定します。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csvoicepolicy.md">Get-CsVoicePolicy</a><br />
<a href="grant-csvoicepolicy.md">Grant-CsVoicePolicy</a><br />
<a href="remove-csvoicepolicy.md">Remove-CsVoicePolicy</a></p></td>
<td><p>音声ポリシーによって、同時呼び出し (会社の電話への着信時に 2 番目の電話を鳴らす機能) や着信転送などのエンタープライズ VoIP 機能を管理します。</p></td>
</tr>
</tbody>
</table>


Skype for Business Online 管理センターによって、選んだ会議ポリシー設定を管理することもできます。

![Lync 管理センター、全般オプションのプロパティ](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync 管理センター、全般オプションのプロパティ")

また、Skype for Business Online 管理センターによって外部アクセス ポリシー設定を管理することもできます。

![管理センター外部通信オプション](images/Dn362826.e5cfb159-b096-463e-b1ef-2b42eb29168a(OCS.15).png "管理センター外部通信オプション")

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

