---
title: Remove-CsNetworkBandwidthPolicyProfile
TOCTitle: Remove-CsNetworkBandwidthPolicyProfile
ms:assetid: 7b1f3c8d-486c-4a7e-aa40-57893f249f66
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398609(v=OCS.15)
ms:contentKeyID: 48272617
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkBandwidthPolicyProfile

 

_**トピックの最終更新日:** 2015-03-09_

ネットワーク帯域幅のポリシー プロファイルを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkBandwidthPolicyProfile -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、Identity が LowBWProfile の帯域幅ポリシー プロファイルを削除します。Identity は一意である必要があるため、最大で 1 つのプロファイルのみが削除されます。

    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 例 2

例 2 では、Identity が LowBWProfile である帯域幅ポリシー プロファイルへのすべての参照を、割り当て先であるすべてのサイトから削除し、その後、そのプロファイルを削除します。この例の最初の行ではまず、**Get-CsNetworkSite** コマンドレットを呼び出して、通話受付管理 (CAC) が構成されたすべてのサイトを取得します。次に、サイトのこのコレクションは **Where-Object** コマンドレットにパイプ処理され、それにより、BWPolicyProfileID が LowBWProfile に等しい (-eq) サイトのみが検索されます。この絞り込まれたコレクションには、BWPolicyProfileID 値が LowBWProfile であるサイトのみが含まれ、**Set-CSNetworkSite** コマンドレットにパイプ処理されます。この処理により、これらの各サイトの BWPolicyProfileID が Null ($null) に変更されます。ここまでの処理で、BWPolicyProfileID が LowBWProfile であるすべてのサイトを検出して、その値を Null に設定しました。この時点で、LowBWProfile プロファイルを使用するサイトは存在しなくなります。プロファイル LowBWProfile がどのサイトでも使用されていないことがわかっているので、このプロファイルに対して **Remove-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出して、削除できます。

ネットワーク構成のどの部分においてもプロファイルが使用されていないことを確認するには、サイト間ポリシーとネットワーク地域リンクに対して、1 行目と同じステップを実行します。

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Set-CsNetworkSite -BWPolicyProfileID $null
    Remove-CsNetworkBandwidthPolicyProfile -Identity LowBWProfile

## 解説

帯域幅ポリシーは、通話受付管理 (CAC) の一部として、特定のモダリティの帯域幅制限を定義する際に使用します (Lync Server では、オーディオとビデオのモダリティのみに帯域幅の制限を割り当てることができます)。このコマンドレットは、これらのポリシーのコンテナー プロファイルを削除します。

重要: プロファイルが、サイトに割り当てられている場合 (**New-CsNetworkSite** コマンドレットまたは **Set-CsNetworkSite** コマンドレットを使用)、サイト間ポリシーに割り当てられている場合 (**New-CsNetworkInterSitePolicy** コマンドレットまたは **Set-CsNetworkInterSitePolicy** コマンドレットを使用)、またはネットワーク地域リンクに割り当てられている場合 (**New-CsNetworkRegionLink** コマンドレットまたは **Set-CsNetworkRegionLink** コマンドレットを使用)、プロファイルを削除することはできません。**Remove-CsNetworkBandwidthPolicyProfile** コマンドレットを呼び出してプロファイルを削除しようとすると、エラーが送信されます。プロファイルを削除するには、まず、すべてのサイト、サイト間ポリシー、およびネットワーク地域リンクからプロファイルを削除する必要があります。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが **Remove-CsNetworkBandwidthPolicyProfile** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkBandwidthPolicyProfile"}

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
<td><p>削除する帯域幅ポリシー プロファイルを一意に定義する文字列値。Identity を指定すると、最大 1 つのプロファイルのみが削除されます。</p></td>
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
<td><p><em>WhatIf</em></p></td>
<td><p>省略可能</p></td>
<td><p>System.Management.Automation.SwitchParameter</p></td>
<td><p>実際にコマンドを実行しなくてもコマンドの実行結果がわかります。</p></td>
</tr>
</tbody>
</table>


## 入力の種類

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType オブジェクト。パイプライン処理されたネットワーク帯域ポリシー プロファイル オブジェクトの入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.BWPolicyProfileType 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsNetworkBandwidthPolicyProfile](new-csnetworkbandwidthpolicyprofile.md)  
[Set-CsNetworkBandwidthPolicyProfile](set-csnetworkbandwidthpolicyprofile.md)  
[Get-CsNetworkBandwidthPolicyProfile](get-csnetworkbandwidthpolicyprofile.md)

