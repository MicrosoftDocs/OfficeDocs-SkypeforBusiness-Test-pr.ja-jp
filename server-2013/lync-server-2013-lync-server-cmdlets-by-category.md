---
title: カテゴリ別の Lync Server 2013 のコマンドレット
TOCTitle: カテゴリ別の Lync Server 2013 のコマンドレット
ms:assetid: 4ce274d7-b0ec-40b8-b85e-9a0613916ffb
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398306(v=OCS.15)
ms:contentKeyID: 48272026
ms.date: 12/10/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# カテゴリ別の Lync Server 2013 のコマンドレット

 

_**トピックの最終更新日:** 2016-12-08_

Microsoft Lync Server 2013 には、管理者がコマンド ラインから Lync Server を管理できるようにするために特別に設計されたコマンドレットが約 550 個含まれます。コマンドレットには、Lync Server 管理シェルからアクセスします。以下のようなコマンドを入力すると、コマンドレットに関するヘルプをコマンド ラインから直接取得できます。

    Get-Help New-CsVoicePolicy -Full

上記のコマンドは、**New-CsVoicePolicy** コマンドレットで使用できるすべてのヘルプを取得します。**New-CsVoicePolicy** の部分を、ヘルプを取得したいコマンドレットの名前に置き換えます。

Microsoft Lync Server 2013 の管理に使用できるすべてのコマンドレットの一覧を取得するには、Lync Server 管理シェル コマンド プロンプトで以下の内容を入力します。

    Get-Command * -Module Lync -CommandType cmdlet

必要なコマンドレットが不明な場合は、カテゴリ別のコマンドレットの一覧およびそのヘルプ トピックもあります。複数のカテゴリに表示されるコマンドレットもあります。これは、そのようなコマンドレットが製品の複数の領域に適用されるためです。以下はカテゴリの一覧です。

## このセクション中


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><a href="lync-server-2013-user-management-cmdlets.md">ユーザー管理のコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-voice-application-cmdlets.md">VoIP アプリケーションのコマンドレット</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-client-management-cmdlets.md">クライアント管理のコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-advanced-enterprise-voice-cmdlets.md">高度なエンタープライズ VoIP のコマンドレット</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-im-and-presence-cmdlets.md">IM およびプレゼンスのコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-pstn-connectivity-cmdlets.md">PSTN 接続のコマンドレット</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-conferencing-cmdlets.md">会議のコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-phones-and-devices-cmdlets.md">電話およびデバイスのコマンドレット</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-infrastructure-and-deployment-cmdlets.md">インフラストラクチャおよび展開のコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-migration-and-coexistence-cmdlets.md">移行および共存のコマンドレット</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-security-cmdlets.md">セキュリティのコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-lync-server-management-shell-configuration-cmdlets.md">Lync Server 管理シェルの構成のコマンドレット</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-server-roles-and-services-cmdlets.md">サーバーの役割およびサービスのコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-mobility-cmdlets.md">モビリティ コマンドレット</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-application-management-cmdlets.md">アプリケーション管理のコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-persistent-chat-server-cmdlets.md">常設チャット サーバーのコマンドレット</a></p></td>
</tr>
<tr class="odd">
<td><p><a href="lync-server-2013-federation-and-external-access-cmdlets.md">Lync Server 2013 でのフェデレーションおよび外部アクセスのコマンドレット</a></p></td>
<td><p><a href="lync-server-2013-centralized-logging-cmdlets.md">集中ログ コマンドレット</a></p></td>
</tr>
<tr class="even">
<td><p><a href="lync-server-2013-enterprise-voice-cmdlets.md">エンタープライズ VoIP のコマンドレット</a></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## 関連項目

#### その他のリソース

[Lync Server PowerShell ブログ](http://go.microsoft.com/fwlink/?linkid=203150%26clcid=0x411)

