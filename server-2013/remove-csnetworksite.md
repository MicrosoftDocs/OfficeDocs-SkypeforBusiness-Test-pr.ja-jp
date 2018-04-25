---
title: Remove-CsNetworkSite
TOCTitle: Remove-CsNetworkSite
ms:assetid: 07b543a6-3aa0-4fce-85f9-9ddc75d7b14f
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg398135(v=OCS.15)
ms:contentKeyID: 48271157
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSite

 

_**トピックの最終更新日:** 2015-03-09_

通話受付管理 (CAC) または Enhanced 9-1-1 (E9-1-1) 用に定義されたネットワーク サイトを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkSite -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、CAC または E9-1-1 構成から Vancouver という Identity を持つサイトを削除します。

    Remove-CsNetworkSite -Identity Vancouver

## 例 2

例 2 では、CAC または E9-1-1 構成から LowBWProfile という名前の帯域幅ポリシー プロファイルを使用しているすべてのサイトを削除します。この例では、まず **Get-CsNetworkSite** コマンドレットを呼び出して、すべてのネットワーク サイトを取得します。このサイトのコレクションが **Where-Object** コマンドレットにパイプ処理され、BWPolicyProfileID が LowBWProfile と等しい (-eq) サイトのみに絞り込まれます。この新しいコレクションが **Remove-CsNetworkSite** コマンドレットにパイプ処理され、これらのサイトが削除されます。

    Get-CsNetworkSite | Where-Object {$_.BWPolicyProfileID -eq "LowBWProfile"} | Remove-CsNetworkSite

## 解説

ネットワーク サイトは、CAC または E9-1-1 展開の各地域内で構成されるオフィスまたは拠点です。このコマンドレットを実行すると、CAC または E9-1-1 構成からサイトが削除されます。

このコマンドレットを実行できるユーザー: 既定では、次のグループのメンバーが、**Remove-CsNetworkSite** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSite"}

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
<td><p>削除するネットワーク サイトの一意の識別子。サイトはグローバル スコープでのみ作成されるため、スコープを指定する必要はありません。代わりに、サイト ID のみを指定する必要があります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType オブジェクト。ネットワーク サイト オブジェクトのパイプライン処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。このコマンドレットを実行すると、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.DisplayNetworkSiteType 型のオフジェクトが削除されます。

## 関連項目

#### その他のリソース

[New-CsNetworkSite](new-csnetworksite.md)  
[Set-CsNetworkSite](set-csnetworksite.md)  
[Get-CsNetworkSite](get-csnetworksite.md)

