---
title: Set-CsNetworkSite
TOCTitle: Set-CsNetworkSite
ms:assetid: 221a099c-72c4-4eb0-8812-6b2b7639a9ee
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398295(v=OCS.15)
ms:contentKeyID: 48271560
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSite

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) または拡張 9-1-1 (E9-1-1) に定義されている、既存のネットワーク サイトを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkSite [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSite [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfileID <String>] [-BypassID <String>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-EnableLocationBasedRouting <$true | $false>] [-Force <SwitchParameter>] [-LocationPolicy <String>] [-NetworkRegionID <String>] [-VoiceRoutingPolicy <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、Vancouver という名前のネットワーク サイトが変更されます。変更されるサイトの名前は、Identity パラメーターの値として指定されます。Vancouver サイトは新しい領域に移動されますが、それには、NetworkRegionID パラメーターを変更する必要があります。この場合は、Canada という名前の領域に変更されます。NetworkRegionID が入力されていても、BypassID の値が指定されていないため、BypassID 値が自動的に生成されます。既存の BypassID はすべて上書きされます。

    Set-CsNetworkSite -Identity Vancouver -NetworkRegionID Canada

## 例 2

例 2 では、Vancouver サイトに関連付けられている帯域幅ポリシー プロファイルのみを変更します。サイト名は、Identity パラメーターの値として指定されます。次に、BWPolicyProfileID パラメーターに次の値を指定します。LowBWLimits。そのプロファイルに関連付けられているポリシーは、このサイトで使用されます。

    Set-CsNetworkSite -Identity Vancouver - BWPolicyProfileID LowBWLimits

## 解説

ネットワーク サイトは、CAC または E9-1-1 展開の各地域内で構成されるオフィスまたは拠点です。このコマンドレットは、既存のサイトの設定を変更します。これには、サイトが関連付けられている地域、サイトの説明、関連付けられている帯域ポリシー プロファイルなどを含めることができます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**Set-CsNetworkSite** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSite"}

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
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このサイトの制限事項を定義する帯域幅ポリシー プロファイルの ID。利用可能なプロファイルの一覧を取得するには、<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出します。</p>
<p>このパラメーターの値を指定する場合は、NetworkRegionID パラメーターの値も指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>BypassID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>グローバル一意識別子 (GUID)。この GUID を使用して、ネットワーク サイトを CAC または E9-1-1 ネットワーク構成内のメディア バイパスの設定にマップします (<strong>New-CsNetworkMediaBypassConfiguration</strong> コマンドレットを呼び出すときに、この BypassID の値を使用します)。</p>
<p>このパラメーターの値を指定する場合は、NetworkRegionID パラメーターの値も指定する必要があります。このパラメーターの値を指定しなくても、NetworkRegionID を指定すると、BypassID が自動的に生成されます。</p>
<p>値を明示的に指定する場合は、GUID の形式 (たとえば、3b24a047-dce6-48b2-9f20-9fbff17ed62a) で指定する必要があります。NetworkRegionID の値を入力して、BypassID 値が自動生成されるようにすることをお勧めします。値を手動で入力すると、値を自動生成しないことを確認する確認プロンプトが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>サイトの説明を示す文字列。このパラメーターを使用することにより、サイトの目的や存在する場所について、Identity だけで表現可能な情報よりも詳細な説明を入力することができます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableLocationBasedRouting</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>True に設定されている場合、音声ルーティングは、通話の発信および着信の両方の場所を考慮することによって管理します。既定値は False です。</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>変更するネットワーク サイトの一意の識別子。サイトはグローバル スコープでのみ作成されるため、スコープを指定する必要はありません。代わりに、ネットワーク サイト ID のみを指定する必要があります。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>DisplayNetworkSiteType</p></td>
<td><p>ネットワーク サイト オブジェクト (Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType タイプのオブジェクト) への参照。このオブジェクトを取得するには、<strong>Get-CsNetworkSite</strong> コマンドレットを呼び出します。</p></td>
</tr>
<tr class="odd">
<td><p><em>LocationPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このサイトに関連付けられている場所ポリシーの名前。場所のポリシーは、特定の E9-1-1 設定をサイトに割り当てます。場所のポリシーの一覧を取得するには、<strong>Get-CsLocationPolicy</strong> コマンドレットを呼び出します。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このサイトが関連付けられているネットワーク領域の ID。BypassID を (自動生成または手動で) 入力する場合、またはネットワーク構成の EnableBandwidthPolicyCheck プロパティが True の場合は、このパラメーターに値を指定する必要があります。ネットワーク構成の設定を取得するには、<strong>Get-CsNetworkConfiguration</strong> コマンドレットを呼び出します。</p>
<p>このサイトに BypassID が既に存在するときに BypassID パラメーターの値を指定しないと、既存の BypassID は自動生成された BypassID によって上書きされます。</p></td>
</tr>
<tr class="odd">
<td><p><em>VoiceRoutingPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>各ユーザーへの音声ルーティングがサイトに割り当てられます。次に例を示します。</p>
<p>-VoiceRoutingPolicy &quot;RedmondVoiceRouting”</p>
<p>ユーザーごとにポリシーを指定する必要があることに注意してください。VoiceRoutingPolicy パラメーターを使用しているサイトには、グローバル ポリシーやサイト ポリシーを割り当てることはできません。</p>
<p>このパラメーターは 2013 年 2 月 の Lync Server 2013 のリリース時に導入されました。</p></td>
</tr>
<tr class="even">
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType オブジェクト。ネットワーク サイト オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkSite](new-csnetworksite.md)  
[Remove-CsNetworkSite](remove-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)  
[Get-CsLocationPolicy](get-cslocationpolicy.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)

