---
title: Set-CsNetworkSubnet
TOCTitle: Set-CsNetworkSubnet
ms:assetid: 9e85cdbb-b5fb-48d6-8f95-6e7cba9d9597
ms:mtpsurl: https://technet.microsoft.com/ja-jp/library/Gg412739(v=OCS.15)
ms:contentKeyID: 48273003
ms.date: 05/19/2016
mtps_version: v=OCS.15
ms.translationtype: HT
---

# Set-CsNetworkSubnet

 

_**トピックの最終更新日:** 2015-03-09_

既存のネットワーク サブネットを変更します。このコマンドレットは Lync Server 2010 で導入されました。

## 構文

    Set-CsNetworkSubnet [-Identity <XdsGlobalRelativeIdentity>] <COMMON PARAMETERS>

    Set-CsNetworkSubnet [-Instance <PSObject>] <COMMON PARAMETERS>

    COMMON PARAMETERS: [-Confirm [<SwitchParameter>]] [-Description <String>] [-Force <SwitchParameter>] [-MaskBits <Int32>] [-NetworkSiteID <String>] [-WhatIf [<SwitchParameter>]]

## 例

## 例 1

この例では ID (サブネット ID) が 172.11.15.0 のサブネットに変更を加えています。このサブネットは、新しい MaskBits 値 (25) と新しい NetworkSiteID (Chicago) に変更されます。

    Set-CsNetworkSubnet -Identity 172.11.15.0 -MaskBits 25 -NetworkSiteID Chicago

## 例 2

例 2 では、Vancouver サイト上のすべてのサブネットを Chicago サイトに移動しています。これを行うため、まず **Get-CsNetworkSubnet** コマンドレットを呼び出します。これにより Lync Server の展開内で定義されたすべてのサブネットのコレクションが取得されます。次に、このサブネットのコレクションを **Where-Object** コマンドレットにパイプ処理します。**Where-Object** コマンドレットはこのコレクションを取り込み、NetworkSiteID が Vancouver に等しい (-eq) サブネットのみに絞り込みます。これでコレクションは Vancouver サイトに関連付けられたサブネットのみから構成されるようになり、そのコレクションを **Set-CsNetworkSubnet** コマンドレットにパイプ処理します。**Set-CsNetworkSubnet** コマンドレットに 1 つのパラメーター NetworkSiteID を指定します。このパラメーターに Chicago という値を渡すことで、**Set-CsNetworkSubnet** コマンドレットにより、コレクションの各メンバーのネットワーク サイト ID が Chicago に変更されます。

    Get-CsNetworkSubnet | Where-Object {$_.NetworkSiteID -eq "Vancouver"} | Set-CsNetworkSubnet -NetworkSiteID Chicago

## 解説

所属するホストの地理的な位置がわかるようにするため、各サブネットにはネットワーク サイトとの関連付けが必要です。このコマンドレットを使用して、関連付けられるネットワーク サイト、サブネットの説明、またはサブネットのマスク ビットを変更します。

このコマンドレットを実行できるユーザー: 既定では、**Set-CsNetworkSubnet** コマンドレットをローカルで実行する権限があるのは、RTCUniversalServerAdmins グループのメンバーです。このコマンドレットが割り当てられているすべての役割ベースのアクセス制御 (RBAC) の役割の一覧 (自身が作成したカスタムの RBAC の役割を含む) を戻すには、Windows PowerShell プロンプトから次のコマンドを実行します。

Get-CsAdminRole | Where-Object {$\_.Cmdlets –match "Set-CsNetworkSubnet"}

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
<td><p><em>Confirm</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>コマンドの実行前に確認メッセージが表示されます。</p></td>
</tr>
<tr class="even">
<td><p><em>Description</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>変更するサブネットの説明です。</p></td>
</tr>
<tr class="odd">
<td><p><em>Force</em></p></td>
<td><p>省略可能</p></td>
<td><p>SwitchParameter</p></td>
<td><p>変更を行う前に表示されるように設定されているすべての確認メッセージを表示しないようにします。</p></td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>省略可能</p></td>
<td><p>XdsGlobalRelativeIdentity</p></td>
<td><p>変更するサブネットの、一意のサブネット ID です。この値は IP アドレス (174.11.12.0 など) か、http: や https: で始まる URL のどちらかです。</p></td>
</tr>
<tr class="odd">
<td><p><em>Instance</em></p></td>
<td><p>省略可能</p></td>
<td><p>SubnetType</p></td>
<td><p>変更するネットワーク サブネット オブジェクトへの参照です。このオブジェクトは、Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 型である必要があり、<strong>Get-CsNetworkSubnet</strong> コマンドレットを呼び出すことにより取得できます。</p></td>
</tr>
<tr class="even">
<td><p><em>MaskBits</em></p></td>
<td><p>省略可能</p></td>
<td><p>Int32</p></td>
<td><p>サブネットに適用するビットマスクです。</p></td>
</tr>
<tr class="odd">
<td><p><em>NetworkSiteID</em></p></td>
<td><p>省略可能</p></td>
<td><p>String</p></td>
<td><p>このサブネットが適用されるネットワーク サイトのサイト ID です。<strong>Get-CsNetworkSite</strong> コマンドレットを呼び出すことにより、展開のサイト ID を取得できます。</p></td>
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

Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType オブジェクトです。ネットワーク サブネット オブジェクトのパイプ処理による入力を受け入れます。

## 戻り値の種類

このコマンドレットには戻り値はありません。Microsoft.Rtc.Management.WritableConfig.Settings.NetworkConfiguration.SubnetType 型のオブジェクトを変更します。

## 関連項目

#### その他のリソース

[New-CsNetworkSubnet](new-csnetworksubnet.md)  
[Remove-CsNetworkSubnet](remove-csnetworksubnet.md)  
[Get-CsNetworkSubnet](get-csnetworksubnet.md)

