---
title: New-CsNetworkRegionLink
TOCTitle: New-CsNetworkRegionLink
ms:assetid: 61a6a7be-8078-4d59-a78a-2f241f6bf800
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398437(v=OCS.15)
ms:contentKeyID: 48272301
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# New-CsNetworkRegionLink

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 用に構成された 2 つの地域間のリンクを作成します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    New-CsNetworkRegionLink -NetworkRegionLinkID <String> <COMMON PARAMETERS>

    New-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> <COMMON PARAMETERS>

    COMMON PARAMETERS: -NetworkRegionID1 <String> -NetworkRegionID2 <String> [-BWPolicyProfileID <String>] [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-InMemory <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、地域 NorthAmerica と EMEA をリンクする、NA\_EMEA という名前の新しいネットワーク地域リンクを作成します。この地域リンク名は、Identity パラメーターの値として指定します (これは自動的に、NetworkRegionLinkID の値として割り当てられます)。リンクされた 2 つのネットワーク地域は、リンク作成のための必須パラメーターです。この場合は、NorthAmerica と EMEA という地域名がその必須パラメーターに該当します。この例では、BWPolicyProfile パラメーターにも値を割り当てています。その結果、その帯域幅ポリシー プロファイル (LowBWLimits) で定義した帯域幅制限が、2 つの地域間の接続に割り当てられます。BWPolicyProfileID が指定されない場合、これらの 2 地域間の接続に帯域幅制限はありません (それでも、サイト間に制限が課せられている場合があります。詳細については、**New-CsNetworkSite** コマンドレットのヘルプ トピックを参照してください)。

    New-CsNetworkRegionLink -Identity NA_EMEA -NetworkRegionID1 NorthAmerica -NetworkRegionID2 EMEA -BWPolicyProfileID LowBWLimits

## 解説

ネットワーク内の地域は、物理的な WAN 接続でリンクされています。このコマンドレットは、2 つの地域間のリンクを定義し、これらの地域間のオーディオ接続とビデオ接続に帯域幅制限を設定します。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **New-CsNetworkRegionLink** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "New-CsNetworkRegionLink"}

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
<td><p>新しく作成されたネットワーク地域リンクの一意の識別子。ネットワーク地域リンクは、グローバル スコープのみで作成されるため、この識別子ではスコープを指定する必要はありません。代わりに、そのリンクを特定する一意の名前を示す文字列が含まれています。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionID1</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>NetworkRegionID2 パラメーターによって識別される地域にリンクされた地域の Identity (NetworkRegionID)。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkRegionID2</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>NetworkRegionID1 パラメーターによって識別される地域にリンクされた地域の Identity (NetworkRegionID)。</p></td>
</tr>
<tr class="even">
<td><p><em>NetworkRegionLinkID</em></p></td>
<td><p>必須</p></td>
<td><p>System.String</p></td>
<td><p>この値は Identity と同じです。Identity と NetworkRegionLinkID の両方を指定することはできません。いずれかに入力された値が自動的に、両方で使用されます。</p></td>
</tr>
<tr class="odd">
<td><p><em>BWPolicyProfileID</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.String</p></td>
<td><p>このリンクの帯域幅制限を定義する帯域幅ポリシー プロファイルの Identity。利用可能なプロファイルの一覧は、<strong>Get-CsNetworkBandwidthPolicyProfile</strong> コマンドレットを呼び出すことにより取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
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

このコマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 型のオブジェクトが作成されます。

## 関連項目

#### その他のリソース

[Remove-CsNetworkRegionLink](remove-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)  
[New-CsNetworkSite](new-csnetworksite.md)

