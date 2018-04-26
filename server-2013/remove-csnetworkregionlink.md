---
title: Remove-CsNetworkRegionLink
TOCTitle: Remove-CsNetworkRegionLink
ms:assetid: f26cde90-e789-44a7-a304-695c85e64403
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg413012(v=OCS.15)
ms:contentKeyID: 48274083
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkRegionLink

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) 用に構成された 2 つの地域間のリンクを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkRegionLink -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この最初の例では、NA\_EMEA の ID を持つネットワーク地域リンクを削除します。

    Remove-CsNetworkRegionLink -Identity NA_EMEA

## 例 2

例 2 では、HighBWLimits という名前の帯域幅ポリシーのプロファイルを使用しているすべてのネットワーク地域リンクを削除します。この例で最初に呼び出されるコマンドレットは **Get-CsNetworkRegionLink** コマンドレット (パラメーターなし) で、これによってすべての地域リンクが取得されます。次に、このリンクのコレクションは **Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットはコレクションの各メンバーを 1 つずつ調べ、BWPolicyProfileID プロパティの値をチェックします。このプロパティが HighBWLimits と等しい (-eq) 場合、**Remove-CsNetworkRegionLink** コマンドレットにそのメンバーをパイプ処理します。これにより、リンクが削除されます。

    Get-CsNetworkRegionLink | Where-Object {$_.BWPolicyProfileID -eq "HighBWLimits"} | Remove-CsNetworkRegionLink

## 解説

ネットワーク内の地域は、物理的な WAN 接続を経由してリンクされます。このコマンドレットによって物理接続は影響を受けませんが、CAC 構成からリンクが削除されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsNetworkRegionLink** コマンドレットのローカル実行を承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkRegionLink"}

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
<td><p><em>Identity</em></p></td>
<td><p>必須</p></td>
<td><p>Microsoft.Rtc.Management.Xds.XdsGlobalRelativeIdentity</p></td>
<td><p>削除するネットワーク地域リンクの一意の識別子です。ネットワーク地域リンクはグローバル スコープでのみ作成されるので、この識別子ではスコープを指定する必要はありません。代わりに、リンクを識別する一意の名前の文字列が含まれます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType オブジェクト。ネットワーク地域リンク オブジェクトのパイプライン入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.NetworkRegionLinkType 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsNetworkRegionLink](new-csnetworkregionlink.md)  
[Set-CsNetworkRegionLink](set-csnetworkregionlink.md)  
[Get-CsNetworkRegionLink](get-csnetworkregionlink.md)

