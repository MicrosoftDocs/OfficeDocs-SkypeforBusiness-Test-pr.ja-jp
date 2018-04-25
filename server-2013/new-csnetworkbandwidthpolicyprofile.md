---
title: New-CsNetworkBandwidthPolicyProfile
TOCTitle: New-CsNetworkBandwidthPolicyProfile
ms:assetid: 84940891-37a6-45fc-972d-05b95aa71ba9
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398675(v=OCS.15)
ms:contentKeyID: 48272763
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkBandwidthPolicyProfile

 

_**トピックの最終更新日:** 2015-03-09_

新しいネットワーク帯域幅ポリシーのプロファイルを作成します。このコマンドレットを使用して、プロファイル内で帯域幅ポリシーを設定することもできます。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-AudioBWLimit <String>] [-AudioBWSessionLimit <String>] [-BWPolicy <PSListModifier>] [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-VideoBWLimit <String>] [-VideoBWSessionLimit <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

例 1 では、LowBWLimits という名前の新しい帯域幅ポリシーのプロファイルを作成します。この新しいプロファイルには、オーディオ ポリシーとビデオ ポリシーという、2 つのポリシー (Lync Server で使用可能なポリシーはこの 2 つだけです) が割り当てられます。オーディオ ポリシーをプロファイルに追加するには、AudioBWLimit パラメーターを使用して、オーディオ接続全体に対して (この場合は) 2000 kbps の制限値を割り当て、AudioBWSessionLimit パラメーターを使用して個々のオーディオ セッションの制限値として 200 kbps を割り当てます。ビデオ セッションの制限も同様ですが、この場合に使用するのは VideoBWLimit パラメーターと VideoBWSessionLimit パラメーターです。

    New-CsNetworkBandwidthPolicyProfile -Identity LowBWLimits -AudioBWLimit 2000 -AudioBWSessionLimit 200 -VideoBWLimit 1400 -VideoBWSessionLimit 500

## 解説

帯域幅ポリシーは、通話受付管理 (CAC) の一部として、特定のモダリティの帯域幅制限を定義する際に使用します (Lync Server では、オーディオとビデオのモダリティのみに帯域幅の制限を割り当てることができます)。このコマンドレットを実行すると、これらのポリシーのコンテナー プロファイルが作成されます。コンテナー内の個別のポリシーを定義するには、このコマンドレットを呼び出すときにオーディオとビデオの帯域幅制限を指定します。

**New-CsNetworkSite** コマンドレットまたは **Set-CsNetworkSite** コマンドレットを呼び出すと、帯域幅ポリシーのプロファイルがネットワーク サイトに適用されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **New-CsNetworkBandwidthPolicyProfile** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkBandwidthPolicyProfile"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>ポリシーを一意に識別する文字列値です。帯域幅ポリシーのプロファイルは、すべてグローバル スコープで作成されます。したがって新しい帯域幅ポリシーのプロファイルを作成する際、スコープは黙示的であり、指定する必要があるのは一意の名前のみです。この値が、プロファイルの BWPolicyProfileID プロパティにも設定されるという点に注意してください。</p></td>
</tr>
<tr class="even">
<td><p><em>AudioBWLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>すべてのオーディオ接続に割り当てられる最大帯域幅です。1 つのオーディオ セッションでオーディオの帯域幅制限を超過するような場合は、このセッションを開始できません。</p>
<p>kbps で表されます。たとえば、値が 1000 の場合は 1000 kbps を表します。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。AudioBWSessionLimit パラメーターに値を指定し、AudioBWLimit には指定しない場合、AudioBWLimit は既定で 0 になります。</p></td>
</tr>
<tr class="odd">
<td><p><em>AudioBWSessionLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>オーディオ セッションごとに割り当てられる最大帯域幅です。kbps で表されます。この値は 40 以上である必要があります。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。AudioBWLimit パラメーターに値を指定し、AudioBWSessionLimit には指定しない場合、AudioBWSessionLimit は既定で 175 になります。</p></td>
</tr>
<tr class="even">
<td><p><em>BWPolicy</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.PSListModifier</p></td>
<td><p>帯域幅ポリシーのプロファイルを含むオブジェクトのリストです。リスト内の各オブジェクトは、帯域幅モダリティ (オーディオまたはビデオ)、帯域幅制限、および帯域幅のセッション制限です。</p>
<p>このパラメーターに値を指定すると、AudioBWLimit、AudioBWSessionLimit、VideoBWLimit、または VideoBWSessionLimit パラメーターに値を指定することができません。</p>
<p>一覧内のオブジェクトは、<strong>New-CsNetworkBWPolicy</strong> コマンドレットを呼び出して作成できます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>帯域幅ポリシーのプロファイルの説明です。たとえば、このパラメーターを使用してプロファイルの用途を明示することができます。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>InMemory</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>永続的な変更としてオブジェクトをコミットせずに、オブジェクト参照を作成します。このパラメーターを指定して呼び出したコマンドレットの出力を変数に割り当てる場合、オブジェクト参照のプロパティを変更し、コマンドレットに対応する Set- コマンドレットを呼び出してそれらの変更をコミットできます。</p></td>
</tr>
<tr class="odd">
<td><p><em>VideoBWLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>すべてのビデオ接続に割り当てられる最大帯域幅です。1 つのビデオ セッションでビデオの帯域幅制限を超過するような場合は、このセッションを開始できません。</p>
<p>kbps で表されます。たとえば、値が 1000 の場合は 1000 kbps を表します。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。VideoBWSessionLimit パラメーターに値を指定し、VideoBWLimit には指定しない場合、VideoBWLimit は既定で 0 になります。</p></td>
</tr>
<tr class="even">
<td><p><em>VideoBWSessionLimit</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>ビデオ セッションごとに割り当てられる最大帯域幅です。kbps で表されます。この値は 100 以上である必要があります。</p>
<p>このパラメーターに値を指定すると、BWPolicy パラメーターには値を指定できません。</p>
<p>既定値は次のとおりです。VideoBWLimit パラメーターに値を指定し、VideoBWSessionLimit には指定しない場合、VideoBWSessionLimit は既定で 700 になります。</p></td>
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

なし。

## 戻り値の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 型のオブジェクトを作成します。

## 関連項目

#### その他のリソース

[Remove-CsNetworkBandwidthPolicyProfile](remove-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkBWPolicy](new-csnetworkbwpolicy.md)

