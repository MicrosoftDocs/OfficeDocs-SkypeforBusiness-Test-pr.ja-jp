---
title: Remove-CsNetworkSubnet
TOCTitle: Remove-CsNetworkSubnet
ms:assetid: 251ddb5c-4837-4810-b46f-d276f9535653
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg425726(v=OCS.15)
ms:contentKeyID: 48271577
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Remove-CsNetworkSubnet

 

_**トピックの最終更新日:** 2015-03-09_

既存のネットワーク サブネットを削除します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Remove-CsNetworkSubnet -Identity <XdsGlobalRelativeIdentity> [-Confirm [<SwitchParameter>]] [-Force <SwitchParameter>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では、ID (サブネット ID) が 172.11.15.0 のサブネットを削除します。

    Remove-CsNetworkSubnet -Identity 172.11.15.0

## 例 2

例 2 では、Vancouver サイトに関連付けられているすべてのサブネットを削除します。これを行うために、まず **Get-CsNetworkSubnet** コマンドレットを呼び出します。このコマンドレットは、Lync Server の展開内で定義されているすべてのサブネットのコレクションを取得します。次に、このサブネットのコレクションは **Where-Object** コマンドレットにパイプ処理されます。**Where-Object** コマンドレットはこのコレクションを取得して、NetworkSiteID が Vancouver に等しい (-eq) サブネットのみに絞り込みます。これで、コレクションが Vancouver サイトに関連付けられているサブネットのみで構成されるようになります。このコレクションを **Remove-CsNetworkSubnet** コマンドレットにパイプ処理して、コレクション内のすべての項目を削除します。

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Remove-CsNetworkSubnet

## 解説

各サブネットは、このサブネットに所属するホストの地理的な場所を判別するために、ネットワーク サイトに関連付けられている必要があります。このコマンドレットを使用して、ネットワーク サブネットを削除します。

このコマンドレットを実行できるメンバー。既定では、次のグループのメンバーが、**Remove-CsNetworkSubnet** コマンドレットをローカルで実行することを承認されています。RTCUniversalServerAdmins。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Remove-CsNetworkSubnet"}

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
<td><p>削除するサブネットの一意のサブネット ID。この値は IP アドレス (174.11.12.0) となります。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType オブジェクト。ネットワーク サブネット オブジェクトのパイプ処理された入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 型のオブジェクトを削除します。

## 関連項目

#### その他のリソース

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Set-CsNetworkSubnet](set-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

