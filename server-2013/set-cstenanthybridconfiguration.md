---
title: Set-CsTenantHybridConfiguration
TOCTitle: Set-CsTenantHybridConfiguration
ms:assetid: 805ac9ee-df40-40e1-baaa-adffb6bd8cf6
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/JJ994046(v=OCS.15)
ms:contentKeyID: 52056635
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsTenantHybridConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

ハイブリッド シナリオで使用され、Microsoft Lync Online に所属するユーザーに、メディア バイパス、Enhanced 9-1-1、コール パークなどの社内エンタープライズ VoIP 機能へのアクセスを付与します。ハイブリッド シナリオ (別名、分割ドメインのシナリオ) は、社内に所属するアカウントを所有するユーザーと Lync Online に所属するアカウントを所有するユーザーが存在する Lync Server の展開です。

このコマンドレットは、Skype for Business Online のみで使用できます。

## 構文

    Set-CsTenantHybridConfiguration [[-Identity] <XdsIdentity>] [-Tenant <guid>] [-PeerDestination <string>] [-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]Set-CsTenantHybridConfiguration [-Tenant <guid>] [-PeerDestination <string>][-HybridConfigServiceInternalUrl <string>] [-HybridConfigServiceExternalUrl <string>] [-Instance <psobject>] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

## 例

## 例 1

例 1 に示すコマンドは、テナント ハイブリッド構成設定のグローバル コレクションの内部サービスの URL を設定します。グローバル設定を構成するには、パラメーター値 "global" と共に Identity パラメーターを含めます。

    Set-CsTenantHybridConfiguration -Identity "global" - HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## 例 2

例 2 では、内部サービスの URL が特定のテナントに対して構成されています。この例では、テナントには TenantID "bf19b7db-6960-41e5-a139-2aa373474354" が割り当てられています。個々のテナントにプロパティ値が明示的に割り当てられている場合、テナントは、グローバル設定ではなく、その個々のテナント ハイブリッド構成設定により管理されます。

    Set-CsTenantHybridConfiguration -Tenant "bf19b7db-6960-41e5-a139-2aa373474354" HybridConfigServiceInternalUrl "https://internal.litwareinc.com"

## 例 3

例 3 に示すコマンドは、組織のテナントすべての内部サービスの URL を構成します。そのために、コマンドではまず **Get-CsTenant** コマンドレットを使用して、すべての使用可能なテナントのコレクションを返します。次にそのコレクションは **ForEach-Object** コマンドレットに対してパイプライン処理されます。さらに、**ForEach-Object** コマンドレットはコレクション内の各テナントに対して **Set-CsTenantHybridConfiguration** コマンドレットを実行し、これらの各テナントの内部サービスの URL を "https://internal.litwareinc.com" に設定します。

    Get-CsTenant | ForEach-Object {Set-CsTenantHybridConfiguration -Tenant $_.TenantID -HybridConfigServiceInternalUrl "https://internal.litwareinc.com"}

## 解説

ハイブリッド展開、つまり "分割ドメイン" 展開では、組織には Lync Online に所属するアカウントを所有するユーザーと同時に Lync Server に所属するアカウントを所有するユーザーが存在します。既定では、Lync Online に所属するユーザーはエンタープライズ VoIP により提供される機能の全範囲にはアクセスできません。これは、Lync Online サーバーが、内部設置型の Lync Server 展開とネットワーク構成情報に直接アクセスすることができないためです。特に、Lync Online のユーザーは、次のような機能に既定ではアクセスできません。

  - Enhanced 9-1-1。緊急通話を行うために使用される Lync Server のサービスです。

  - コール パーク。ユーザーが電話 A の通話を保留にして、電話 B からその通話を取得できるようにする Lync Server のサービスです。

  - メディア バイパス。公衆交換電話網 (PSTN) との間の通話が仲介サーバーをバイパスできるようにして、コード変換とネットワーク遅延を最小限にするのに役立ちます。

  - PSTN 会議のダイヤルインおよびダイヤルアウト。ユーザーが任意の PSTN 電話またはモバイル デバイスを使用してオンライン会議の音声部分に参加できるようにします。

  - 応答グループ アプリケーション。ヘルプ デスクや顧客サポート ラインなどのエンティティに通話を自動的にルーティングする手段です。既定では、Lync Online のユーザーには応答グループのエージェントの役割がありません。

Lync Online のユーザーにエンタープライズ VoIP 機能へのアクセスを提供するには、管理者は、内部および外部 Web サービスの URL や組織のアクセス エッジ サーバーの完全修飾ドメイン名などのハイブリット構成設定に、適切な値を割り当てる必要があります。これらの値は、**Set-CsTenantHybridConfiguration** コマンドレットを使用した場合にのみ構成できますが、これらの高度なエンタープライズ VoIP 機能を使用するために必要な情報を Lync Online サーバーに提供します。

## パラメーター


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>必須</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p></p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンド実行中に発生する可能性のある、致命的ではないすべてのエラー メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>HybridConfigServiceExternalUrl</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>外部 Web サービスの URL</p></td>
</tr>
<tr class="even">
<td><p><em>HybridConfigServiceInternalUrl</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>内部 Web サービスの URL</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsIdentity</p></td>
<td><p>変更するテナント ハイブリッド構成設定の一意の識別子。ユーザーはハイブリット構成設定の 1 つのグローバル コレクションに制限されているため、Identity パラメーターを使用して変更できる唯一のコレクションはグローバル コレクションです。</p>
<p>-Identity global</p>
<p>個々のテナントの設定を変更するには、Identity パラメーターではなく Tenant パラメーターを使用します。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSObject</p></td>
<td><p>個々のパラメーター値を設定せずに、コマンドレットにオブジェクトへの参照を渡せます。</p></td>
</tr>
<tr class="odd">
<td><p><em>PeerDestination</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>内部設置型アクセス エッジ サーバーの完全修飾ドメイン名。</p></td>
</tr>
<tr class="even">
<td><p><em>Tenant</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Guid</p></td>
<td><p>変更されるハイブリッド構成設定を所有するテナント アカウントのグローバル一意識別子 (GUID)。次に例を示します。</p>
<p>-Tenant &quot;38aad667-af54-4397-aaa7-e94c79ec2308&quot;</p>
<p>次のコマンドを実行することにより、テナントの各々についてテナント ID を返すことができます。</p>
<p>Get-CsTenant | Select-Object DisplayName, TenantID</p>
<p>Windows PowerShell のリモート セッションを使用していて、Skype for Business Online のみに接続されている場合は、Tenant パラメーターを含める必要はありません。代わりに、接続情報に基づいて自動的にテナント ID が入力されます。Tenant パラメーターは主にハイブリッド展開で使用します。</p></td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

なし。**Set-CsTenantHybridConfiguration** コマンドレットはパイプライン処理された入力を受け入れません。

## 戻り値の種類

なし。代わりに、**Set-CsTenantHybridConfiguration** コマンドレットは、Microsoft.Rtc.Management.WritableConfig.Settings.HybridConfiguration.TenantHybridConfiguration オブジェクトの既存のインスタンスを変更します。

## 関連項目

#### その他のリソース

[Get-CsTenantHybridConfiguration](get-cstenanthybridconfiguration.md)

