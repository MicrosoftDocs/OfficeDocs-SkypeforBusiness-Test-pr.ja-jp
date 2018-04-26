---
title: Set-CsNetworkConfiguration
TOCTitle: Set-CsNetworkConfiguration
ms:assetid: d54dc154-c092-4be9-8656-f7fec3fbd835
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398927(v=OCS.15)
ms:contentKeyID: 48273766
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkConfiguration

 

_**トピックの最終更新日:** 2015-03-09_

ネットワーク構成の設定を変更します。このコマンドレットは、通話受付管理 (CAC) を有効または無効にする際に最も頻繁に使用されます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkConfiguration [-Identity <XdsIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkConfiguration [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-BWPolicyProfiles <PSListModifier>] [-Confirm [<SwitchParameter>]] [-EnableBandwidthPolicyCheck <$true | $false>] [-Force <SwitchParameter>] [-InterNetworkRegionRoutes <PSListModifier>] [-InterNetworkSitePolicies <PSListModifier>] [-MediaBypassSettings <MediaBypassSettingsType>] [-NetworkRegionLinks <PSListModifier>] [-NetworkRegions <PSListModifier>] [-NetworkSites <PSListModifier>] [-Subnets <PSListModifier>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例のコマンドを実行すると、CAC 構成全体に対して検証チェックが実行され、CAC が有効となります (有効となるかどうかは、戻される警告プロンプトへの応答によって変わります)。CAC が既に有効である (つまり EnableBandwidthPolicyCheck プロパティが True である) 場合にこのコマンドを実行すると、単に検証チェックが実行されます。

    Set-CsNetworkConfiguration -EnableBandwidthPolicyCheck $True

## 解説

ネットワーク構成オブジェクトには、Lync Server 展開内の CAC 構成全体に対するすべての設定と、メディア バイパス設定が含まれます。このコマンドレットを使用すると、CAC 構成の任意の部分を変更できます。また、メディア バイパス設定の変更が必要な場合には、このコマンドレットを使用する必要があります。ただし、ほとんどの CAC 構成設定を変更する際には、そのオブジェクト型に固有のコマンドレットを使用することをお勧めします。たとえば、ネットワーク領域に関する作業を行うには、このコマンドレットの NetworkRegions パラメーターを操作するのではなく、末尾に CsNetworkRegion という名詞の付いたコマンドレットを使用します。

このコマンドレットの主な用途は、CAC を有効 (または無効) にして、メディア バイパス設定を適用することです。構成に必要な各種コンポーネント (領域、サイト、サブネットなど) を設定した後、使用前に構成を有効にする必要があります。構成を有効にするには、単に EnableBandwidthPolicyCheck パラメーターを True に設定します。EnableBandwidthPolicyCheck を True に設定したままこのコマンドレットを実行すると、CAC がすぐには有効にならない点に注意してください。CAC を有効にする前に、設定が適切に構成されていることを確認するための一連の検証チェックが実行されます。設定にエラーや不一致がある場合は警告が表示され、問題があっても CAC を有効にするかどうかについての確認を求められます。(Enter キーまたは Y キーを押して) 続行を選択すると、検証が続行されます。別の問題が検出された場合は、再度確認を求められます。

警告が出るたびに続行を選択してすべての検証を終了すると、EnableBandwidthPolicyCheck が True に設定され、CAC が有効となります。ただし問題が解決されるまでは、予想どおりに機能しない可能性が高くなります。検証のいずれかの時点で (警告プロンプトで N キーを押して) 検証を停止すると、検証が終了して EnableBandwidthPolicyCheck が False (既定値) に設定されたままとなります。

EnableBandwidthPolicyCheck が既に True に設定されている場合は、**Set-CsNetworkConfiguration** コマンドレットを呼び出してパラメーター EnableBandwidthPolicyCheck に True の値を渡し、設定を変更せずに検証を実行することができます。また、EnableBandwidthPolicyCheck が True に設定されている場合は、**Set-CsNetworkConfiguration** コマンドレットを呼び出して変更を行おうとすると、検証チェックが再実行されます。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーは **Set-CsNetworkConfiguration** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkConfiguration"}

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
<th>必須かどうか</th>
<th>型</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BWPolicyProfiles</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>サイト、サイト間ポリシー、およびネットワーク地域リンクに割り当て可能なすべての帯域幅ポリシー プロファイルのコレクションです。各帯域幅ポリシー プロファイルには、オーディオ接続とビデオ接続のいずれかまたは両方の帯域幅制限 (全体の制限とセッションの制限) が含まれます。全部の帯域幅制限ポリシー プロファイルのリストは、<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>EnableBandwidthPolicyCheck</em></p></td>
<td><p>省略可能</p></td>
<td><p>Boolean</p></td>
<td><p>このパラメーターを True に設定すると、CAC 構成全体に対して検証チェックが実行されます。すべての検証チェックにパスするか、すべての警告を無視するよう選択すると、CAC が有効となります。検証チェックにパスしなかった場合、検証を停止することを選択できます。この場合、EnableBandwidthPolicyCheck の値は変更されません。検証チェックを実行する前に、ネットワーク地域の各ペア間の地域ルートを定義する必要があります。</p>
<p>この値を False に設定すると、CAC が無効となります。</p>
<p>既定値は次のとおりです。False</p></td>
</tr>
<tr class="even">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>このパラメーターによって値が取得されることはありません。このパラメーターを含めると、(構成の有効化を含む) 構成への変更はすべて警告や検証チェックなしで実行されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsIdentity</p></td>
<td><p>この値は常に Global となります。</p></td>
</tr>
<tr class="even">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>NetworkConfigurationSettings</p></td>
<td><p>ネットワーク構成オブジェクトへの参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings 型である必要があり、<strong>Get-CsNetworkConfiguration</strong> コマンドレットを呼び出すことで取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>InterNetworkRegionRoutes</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているすべてのネットワーク領域ルートのコレクションです。<strong>Get-CsNetworkInterRegionRoute</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>InterNetworkSitePolicies</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているネットワーク サイト間ポリシーのコレクションです。<strong>Get-CsNetworkInterSitePolicy</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>MediaBypassSettings</em></p></td>
<td><p>省略可能</p></td>
<td><p>MediaBypassSettingsType</p></td>
<td><p>CAC 構成のグローバル メディアのバイパス設定を定義するオブジェクトへの参照です。この値を設定すると、既存のメディア パイパス設定がすべて上書きされます。<strong>New-CsNetworkMediaBypassConfiguration</strong> コマンドレットを呼び出し、新しい構成設定を変数に割り当てることで、このオブジェクト参照を取得します。この変数を MediaBypassSettings パラメーターに渡して、グローバル メディアのバイパス設定を変更します。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinks</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているネットワーク地域リンクのコレクションです。各ネットワーク地域リンクによって、2 つの領域間に存在する接続と、この領域間の接続に適用する必要がある帯域幅制限を定義します。<strong>Get-CsNetworkRegionLink</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegions</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているネットワーク領域のコレクションです (各ネットワーク領域は、ネットワーク内のハブやバックボーンを表します)。<strong>Get-CsNetworkRegion</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkSites</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているネットワーク サイトのコレクションです (各ネットワーク サイトは、領域内のオフィスや場所を表します)。<strong>Get-CsNetworkSite</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Subnets</em></p></td>
<td><p>省略可能</p></td>
<td><p>PSListModifier</p></td>
<td><p>CAC 構成内で定義されているネットワーク サブネットのコレクションです (各ネットワーク サブネットで、エンドポイントとサイトが関連付けられています)。<strong>Get-CsNetworkSubnet</strong> コマンドレットを呼び出すことで、このコレクションのすべてのメンバーを取得できます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings オブジェクト。ネットワーク構成オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

**Set-CsNetworkConfiguration** コマンドレットは、値またはオブジェクトを戻しません。代わりに、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkConfigurationSettings オブジェクトのインスタンスが変更されます。

## 関連項目

#### その他のリソース

[Remove-CsNetworkConfiguration](remove-csnetworkconfiguration.md)  
[Get-CsNetworkConfiguration](get-csnetworkconfiguration.md)  
[Get-CsNetworkSite](get-csnetworksite.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkInterSitePolicy](get-csnetworkintersitepolicy.md)  
[Get-CsNetworkInterRegionRoute](get-csnetworkinterregionroute.md)  
[Get-CsNetworkRegion](get-csnetworkregion.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkMediaBypassConfiguration](new-csnetworkmediabypassconfiguration.md)

