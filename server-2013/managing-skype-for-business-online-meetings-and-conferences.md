---
title: Lync Online のミーティングと会議の管理
TOCTitle: Lync Online のミーティングと会議の管理
ms:assetid: a4d0c070-4df2-47df-a1e2-6ce62600a287
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Dn362833(v=OCS.15)
ms:contentKeyID: 56270130
ms.date: 06/02/2017
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Lync Online のミーティングと会議の管理

 

_**トピックの最終更新日:** 2015-06-22_

次のコマンドレットを使用して、ミーティングや会議の設定を管理できます。


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
<td><p><a href="disable-csmeetingroom.md">Disable-CsMeetingRoom</a><br />
<a href="enable-csmeetingroom.md">Enable-CsMeetingRoom</a><br />
<a href="get-csmeetingroom.md">Get-CsMeetingRoom</a><br />
<a href="set-csmeetingroom.md">Set-CsMeetingRoom</a></p></td>
<td><p>ミーティング ルームのエンドポイント デバイスを管理します。</p>
<p>Skype for Business Online では、ミーティング ルームは会議室にインストールされている内蔵コンピューター アプライアンスであり、高度な会議機能が用意されています。これらの新しいエンドポイント デバイスを管理するには、まずデバイスの Exchange リソース メールボックス アカウントを作成して有効にし、次に Skype for Business Online でそのリソース アカウントを有効にする必要があります。</p></td>
</tr>
<tr class="even">
<td><p><a href="get-csaudioconferencingprovider.md">Get-CsAudioConferencingProvider</a></p></td>
<td><p>組織が契約している電話会議プロバイダーの情報が返されます。</p>
<p>電話会議プロバイダーとは、電話会議サービスを組織に提供するサード パーティの企業です。これらのサービスには、リアルタイム通訳、トランスクリプション、オペレーターによる各電話会議のリアルタイム サポートなどの、高度なサービスが含まれます。</p></td>
</tr>
<tr class="odd">
<td><p><a href="get-csmeetingconfiguration.md">Get-CsMeetingConfiguration</a><br />
<a href="set-csmeetingconfiguration.md">Set-CsMeetingConfiguration</a></p></td>
<td><p>ユーザーが作成できる会議の種類を制御し、会議での匿名ユーザーやダイヤルイン会議ユーザーの処理方法について決定します。</p>
<p>ミーティング (または会議とも呼ばれます) は、Skype for Business Online の重要部分です。たとえばこれらのコマンドレットを使用して、ダイヤルイン ユーザーに対して会議への参加を自動的に許可せず、会議ロビーへルーティングされるように会議を構成できます。これらのダイヤルイン ユーザーは、発表者から会議への参加を承認されるまで、保留のままロビーで待機します。</p></td>
</tr>
</tbody>
</table>


また、Skype for Business Online 管理センターを使用して、会議構成プロパティの小さいサブセットを管理することもできます。

![Lync 管理センター、全般オプションのプロパティ](images/Dn362833.acf90793-7ee4-4faf-b791-f149dd5df2a5(OCS.15).png "Lync 管理センター、全般オプションのプロパティ")

## 関連項目

#### 概念

[Lync Online のコマンドレット](the-skype-for-business-online-cmdlets.md)  
[クイック リファレンス: Windows PowerShell を使用した一般的な Lync Online の管理タスクの実行](quick-reference-using-windows-powershell-to-do-common-skype-for-business-online-management-tasks.md)

